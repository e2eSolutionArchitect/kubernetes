

<img width="1505" alt="image" src="https://github.com/e2eSolutionArchitect/kubernetes/assets/62712515/280183bd-57bc-4182-ba82-3ac60c3d9064">

## Create  EKS Cluster with Fargate profile
- Please refer here for the [AWS Cloudformation template](https://github.com/e2eSolutionArchitect/scripts/blob/main/aws/cloudformation/cf-eks-fargate.yml) to provision EKS cluster with Fargate profile

# ***** Attention *****
To avoid few eks errors please make sure you keep below pointers in mind before creating eks cluster
- Fargate profile 'Namespace' should match with pod 'Namespace'
- Multiple fargate profile can be created for hosting different apps separated by namespaces
- Private Subnet is required for Fargate profile. Make sure you have private subnet available
- pods will be created under fargate profile which is in private subnet. It will not have internet gateway. If you are pulling an image from public repository, please make sure you have NAT gateway properly configured. 
- After nginx deployment, if pods are not running because of cloudwatch log group, please check the troubleshooting reference below.
- The 'pod selector' in fargate-profile and pod deployment yml must match. in this case it is "app:nginx" 

## Create an EC2 to manage and configure cluster from there
- Please refer here for the [AWS Cloudformation template](https://github.com/e2eSolutionArchitect/scripts/blob/main/aws/cloudformation/cf-ec2-kubectl.yml) to create an EC2 with AWS CLI and kubectl installed. 

## Install kubectl ( If not installed already using above CF template)
- click [here](https://github.com/e2eSolutionArchitect/kubernetes/blob/main/docs/install-kubectl.md)

## Please refer Troubleshoot [here](https://github.com/e2eSolutionArchitect/kubernetes/blob/main/eks/troubleshoot.md) when needed

## Configure AWS
```
aws configure
```

## Install eksctl 
- [click here](https://github.com/e2eSolutionArchitect/kubernetes/blob/main/docs/install-eksctl.md)

## Verify the user configured via aws configure
```
aws sts get-caller-identity
```
output
```
ubuntu@ip-172-20-0-52:~$ aws sts get-caller-identity
{
    "UserId": "############",
    "Account": "11111111111111",
    "Arn": "arn:aws:iam::11111111111111:user/myuser"
}
```


## Create or update a kubeconfig file for your cluster

```
aws eks update-kubeconfig --region us-east-1 --name eks-cluster
```

An alternative way pass role and profile but while updating configMap I would recommend using the above single liner command 
```
aws eks update-kubeconfig \
    --region us-east-1 \
    --name eks-cluster \
    --role-arn arn:aws:iam::1111111111:role/myrole
    --profile default

aws eks update-kubeconfig --region us-east-1 --name eks-cluster --role-arn arn:aws:iam::1111111111:role/myrole --profile default
```

## Check kubectl config
```
kubectl config view --minify
```

## Get config file for eks full access
```
wget https://s3.us-west-2.amazonaws.com/amazon-eks/docs/eks-console-full-access.yaml
```

## Please make sure you have AWS CLI configured in the system
```
kubectl apply -f eks-console-full-access.yaml
```

Troubleshoot [click here](https://github.com/e2eSolutionArchitect/troubleshoot/tree/main/aws/eks) , if you receive any of the following errors
- [is not authorized to perform: sts:AssumeRole on resource](https://github.com/e2eSolutionArchitect/troubleshoot/blob/main/aws/is%20not%20authorized%20to%20perform%20sts%20AssumeRole%20on%20resource.md)
- [couldn't get current server API group list: the server has asked for the client to provide credentials](https://github.com/e2eSolutionArchitect/troubleshoot/blob/main/aws/eks/the%20server%20has%20asked%20for%20the%20client%20to%20provide%20credentials.md)

## Output

```
ubuntu@ip-172-31-47-155:~$ ls
eks-console-full-access.yaml
ubuntu@ip-172-31-47-155:~$ aws eks --region us-east-1 update-kubeconfig --name e2esa-demo-eks-cluster
Added new context arn:aws:eks:us-east-1:<accountno>:cluster/e2esa-demo-eks-cluster to /home/ubuntu/.kube/config
ubuntu@ip-172-31-47-155:~$ kubectl apply -f eks-console-full-access.yaml
error: You must be logged in to the server (the server has asked for the client to provide credentials)
ubuntu@ip-172-31-47-155:~$ aws configure
AWS Access Key ID [None]: #########
AWS Secret Access Key [None]: ########
Default region name [None]: 
Default output format [None]: 
ubuntu@ip-172-31-47-155:~$ kubectl apply -f eks-console-full-access.yaml
clusterrole.rbac.authorization.k8s.io/eks-console-dashboard-full-access-clusterrole created
clusterrolebinding.rbac.authorization.k8s.io/eks-console-dashboard-full-access-binding created
ubuntu@ip-172-31-47-155:~$ kubectl edit configmap aws-auth -n kube-system
configmap/aws-auth edited
ubuntu@ip-172-31-47-155:~$ eksctl get clusters --region us-east-1
NAME                    REGION          EKSCTL CREATED
e2esa-demo-eks-cluster  us-east-1       False
ubuntu@ip-172-31-47-155:~$ kubectl get nodes -o wide
NAME                           STATUS   ROLES    AGE   VERSION               INTERNAL-IP    EXTERNAL-IP     OS-IMAGE         KERNEL-VERSION                 CONTAINER-RUNTIME
ip-172-31-8-166.ec2.internal   Ready    <none>   24m   v1.23.9-eks-ba74326   172.31.8.166   100.26.149.66   Amazon Linux 2   5.4.209-116.367.amzn2.x86_64   docker://20.10.17
ip-172-31-84-68.ec2.internal   Ready    <none>   24m   v1.23.9-eks-ba74326   172.31.84.68   54.163.177.23   Amazon Linux 2   5.4.209-116.367.amzn2.x86_64   docker://20.10.17
ubuntu@ip-172-31-47-155:~$
```

## Update ConfigMap 
```
kubectl edit configmap aws-auth -n kube-system
```

configmap to allow an ec2 bastion host to connect to cluster by role "e2esa-ec2-profile-bastion-role". Goal is to allow any user who connects through bastion host should be able to connect eks clsuter without using user's aws creds
```
apiVersion: v1
data:
  mapRoles: |
    - groups:
      - system:bootstrappers
      - system:nodes
      rolearn: arn:aws:iam::<aws-acc-no>:role/e2esa-eks-nodegroup-role
      username: system:node:{{EC2PrivateDNSName}}
    - rolearn: arn:aws:iam::<aws-acc-no>:role/e2esa-eks-cluster-access-role
      username: eksadmin
      groups:
      - system:masters
    - rolearn: arn:aws:iam::<aws-acc-no>:role/e2esa-ec2-profile-bastion-role
      username: ec2bastionusr
      groups:
      - system:masters
  mapUsers: |
    - userarn: arn:aws:iam::<aws-acc-no>:user/<iam-user-name>
      username: <iam-user-name>
      groups:
      - system:bootstrappers
      - system:nodes
      - system:masters
      - eks-console-dashboard-full-access-group
kind: ConfigMap
metadata:
  creationTimestamp: "2022-11-02T19:37:33Z"
  name: aws-auth
  namespace: kube-system
  resourceVersion: "730"
  uid: 1cghhtf0-bgh3-4ed1-b7df-e9dd7310oj7fd
```

multiple users can be added like below with diffferent set of groups for permissions
```
    mapUsers: |
    - userarn: arn:aws:iam::<aws-acc-no>:user/<iam-user-name>
      username: <iam-user-name1>
      groups:
      - system:bootstrappers
      - system:masters
      - system:nodes
      - eks-console-dashboard-full-access-group
    - userarn: arn:aws:iam::<aws-acc-no>:user/<iam-user-name>
      username: <iam-user-name2>
      groups:
      - system:bootstrappers
      - system:masters
      - system:nodes
      - eks-console-dashboard-full-access-group

```
## Make sure the role associated with the user has trust relationship for sts:AssumeRole 
EKS role Trust Relationship [check here](https://github.com/e2eSolutionArchitect/scripts/blob/main/aws/iam/policies/e2esa-eks-demo.json)

## Get cluster details
```
kubectl get svc
```

# Get cluster details
```
eksctl get clusters --region us-east-1
```

## Execute deployment yml - refer template [here](https://github.com/e2eSolutionArchitect/kubernetes/blob/main/eks/deployments/deployment-nginx-eks-fargate.yml)
```
kubectl apply -f deployment.yml
```

## Get all resources
```
kubectl get pods --all-namespaces

kubectl get all -n <namespace>
kubectl get all -n eks-sample-app
```

[![HELPLINE](https://github.com/e2eSolutionArchitect/academy/assets/8308302/3b85acaf-50f5-4a4f-850d-46216de108af)](Helpline)(https://e2esolutionarchitect.com/helpline/)

***[Click here](https://e2esolutionarchitect.eventbrite.com)*** for list of upcoming trainings.

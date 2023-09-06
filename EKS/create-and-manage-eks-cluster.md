
## Create  EKS Cluster with Fargate profile
- Please refer here for the [AWS Cloudformation template](https://github.com/e2eSolutionArchitect/scripts/blob/main/aws/cloudformation/cf-eks-fargate.yml) to provision EKS cluster with Fargate profile

## Create an EC2 to manage and configure cluster from there
- Please refer here for the [AWS Cloudformation template](https://github.com/e2eSolutionArchitect/scripts/blob/main/aws/cloudformation/cf-ec2-kubectl.yml) to create an EC2 with AWS CLI and kubectl installed. 

## Install kubectl ( If not installed already using above CF template)
- click [here](https://github.com/e2eSolutionArchitect/kubernetes/blob/main/docs/install-kubectl.md)

## Verify the user configured via aws configure
```
aws sts get-caller-identity
```

## Create or update a kubeconfig file for your cluster
```
aws eks update-kubeconfig \
    --region us-east-1 \
    --name eks-cluster \
    --role-arn arn:aws:iam::1111111111:role/myrole
    --profile default
```

## Check kubectl config
```
kubectl config view --minify
```

Troubleshoot [click here](https://github.com/e2eSolutionArchitect/troubleshoot/tree/main/aws/eks) , if you receive any of the following errors
- is not authorized to perform: sts:AssumeRole on resource
- couldn't get current server API group list: the server has asked for the client to provide credentials

## Get cluster details
```
kubectl get svc
```


[![e2eSA Talent Development Programs](https://user-images.githubusercontent.com/62712515/212548238-92365832-fe03-47c7-8c06-701834a67ebf.png)](https://github.com/e2eSolutionArchitect/academy)
***[Click here](https://e2esolutionarchitect.eventbrite.com)*** for list of upcoming trainings.

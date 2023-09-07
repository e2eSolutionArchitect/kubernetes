# EKS Kubernetes 

## EKS Kubernetes architecture
- Master node resides under "EKS Control plane". 
- EKS Control plane belows to AWS public network. It is not in our AWS vpc nor in aws account. 
- Worker nodes reside under "EKS Managed Mode Group"
  
EKS is managed service. Users need to focus on Application workload design and deploy. Don't need to worry about HA, maintenance etc in any nodes. 

![image](https://user-images.githubusercontent.com/62712515/200024539-70044eb4-b262-4985-9f05-531cb3a0c041.png)

![image](https://user-images.githubusercontent.com/62712515/200707166-2c706320-1978-4eb9-b3b3-717819608562.png)

## How to access the deployed app ?

- After you have created kubernetes service and deployment from this yaml [click here](https://raw.githubusercontent.com/e2eSolutionArchitect/scripts/main/kubernetes/deployment/deployment-nginx.yaml)

```
kubectl apply -f https://raw.githubusercontent.com/e2eSolutionArchitect/scripts/main/kubernetes/deployment/deployment-nginx.yaml
```
- check node external IP
```
kubectl get nodes -o wide --namespace=e2esa-webapp01-ns
```

- check the NodePort from service, here it is 30317 in below output
```
kubectl get services --namespace=e2esa-webapp01-ns

NAME                             TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
service/e2esa-webapp01-service   NodePort   172.20.115.11   <none>        80:30317/TCP   57m
```

- IMPORTANT: Make sure you have this nodeport (30317) allowed to internet in cluster security group. 
- to verify that, go to Security groups > search for the security group name like 'eks-cluster-<your-cluster-name>' . e.g, eks-cluster-sg-e2esa-demo-eks-cluster
- add inbound rule for Custom TCP for port NodePort and open it to 0.0.0.0 (as we are deploying publickly accessible app)

- Now the url to access app will be http://node-external-ip:nodeport. for above example it is http://node-external-ip:30317, http://34.200.232.10:30317 or http://ec2-34-200-232-10.compute-1.amazonaws.com:30317/
  
  - Create an ALB and target group to point to the nodegroup instances. and access through ALB DNS link
  - You can add ALB in Route53 with a domain name

[![e2eSA Talent Development Programs](https://user-images.githubusercontent.com/62712515/212548238-92365832-fe03-47c7-8c06-701834a67ebf.png)](https://github.com/e2eSolutionArchitect/academy)
***[Click here](https://e2esolutionarchitect.eventbrite.com)*** for list of upcoming trainings.

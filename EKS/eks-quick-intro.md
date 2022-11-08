# EKS Kubernetes 

## EKS Kubernetes architecture
- Master node resides under "EKS Control plane". 
- EKS Control plane belows to AWS public network. It is not in our AWS vpc nor in aws account. 
- Worker nodes reside under "EKS Managed Mode Group"
  
EKS is managed service. Users need to focus on Application workload design and deploy. Don't need to worry about HA, maintenance etc in any nodes. 

![image](https://user-images.githubusercontent.com/62712515/200024539-70044eb4-b262-4985-9f05-531cb3a0c041.png)

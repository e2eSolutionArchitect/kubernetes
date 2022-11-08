## What is Kubernetes?
Kubernetes is a portable, extensible, opensource platform for managing containerized workloads

## Features:
- Service discovery and load balancing
- Storage orchestration
- Automated rollouts and rollback
- Automatic bin packing
- Self-healing
- Secret and configuration management

## High level K8s architecture
- A k8s custer has a Master and one or more Worker Nodes
- Every nodes have container runtime installed. (container runtime such as docker, rkt, container-d etc)

![image](https://user-images.githubusercontent.com/62712515/199984106-df45a310-a431-45d6-836d-3f431fbf177c.png)
[reference](https://www.cncf.io/blog/2019/08/19/how-kubernetes-works/)

## Conponents in Master node
- Contrainer runtime ( such as Docker )
- ### etcd > 
  is a key-value store. stores master and node information. Also used as k8s backend store for all cluster data.
  
- ### kube-scheduler > 
  It is responsible for distributing containers across across multiple worker nodes. It finds unassigned pod and assign node to it. 
  
- ### kube-apiserver > 
  It exposes k8s APIs. everyone, clitool kubectl, Users and masters components like scheduler, controller manager, etcd, worker node components like 'kubelet', everyone talk with API server. 
  
- ### kube-controller-manager >
  Basically a watcher for resiliency. If any container, node or endpoint goes down then it brings up new  container, node or endpoint . 
    - Node controller >
    - Replication Controller >
    - Endpoint Controller >
    - Service Account & Token Controller > 

- ### cloud-controller-manager >
   Cloud specific controll logic in k8s control plane. controller specific to cloud providers.

## Conponents in Worker node
- Contrainer runtime ( such as Docker )
- ### kubelet > 
  An agent to assure that the containers are running in a Pod on a Node
  
- ### kube-proxy > 
  A network proxy which runs on each node in the k8s cluster. maintain network ruls on nodes. Allows network comminucation with pods from network inside and outside of the cluster.
  
  
  ## Kubernetes Cluster
  ![image](https://user-images.githubusercontent.com/62712515/199985304-8adc7dcb-71c1-4101-8735-47db71333b80.png)
[Reference](https://kubernetes.io/docs/concepts/overview/components/)
  
 Please check k8s scripts [here](https://github.com/e2eSolutionArchitect/scripts/tree/main/kubernetes)
 
 ## Pod
 - A SINGLE INSTANCE of an application. 
 - The smallest object in k8s. 
 - K8s DOESN'T deploy container directly on nodes. Container is encapsulated into POD (k8s object)
 - pod generally has one-to-one relationship with containers. we do scale up or scale down for pods. not containers. 
 - there can be more than one container in a single pod but it is NOT recommended. 
 - In multi-container pod case , when we need a helper container/side car container for data puller/data pusher then only we use multi-container. 
 
 ```
### nodePort:31961 - node port
### port:81 - service port
### targetPort: 80 -  this is container port or application port
```
## URL to access your app externally 
```
http://<node-public-ip>:<NodePort>/<contextpath>
http://57.156.89.23:31961/hello
```
 ## ReplicaSet
 Responsible for maintaining a stable set of replica pods running at a given time. Assures the availability of a specified number of identical pods
 ReplicaSet provides following features
 - High availability and reliabilit
 - Scaling
 - Load balancing
 - Labels & Selectors
  
 ## Deployment
 A deployment runs multiple replicas of application and automatically replaces any instances that fail or become unresponsive. Deployment does Rollout & rollback changes changes to applications. 
 
- Create a deployment to rollout a ReplicaSet
- Updating the Deployment
- Rolling back a Deployment
- Scalling a Deployment 
- Pausing and Resuming a deployment 
- Deployment Status
- Cleanup Policy

 
 ## Service
 Service sits infront of a pod and acts as a load balancer. It provides a vertual IP and creates an abstruction for number of pods. 

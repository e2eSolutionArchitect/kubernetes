Please refer the [reference here](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

## Get commands with basic output
```
 # List all services in the namespace
kubectl get services

# List all pods in all namespaces        
kubectl get pods --all-namespaces    

# List all pods in the current namespace, with more details
kubectl get pods -o wide

# List a particular deployment                     
kubectl get deployment my-dep                 

# List all pods in the namespace
kubectl get pods                              

# Get a pod's YAML
kubectl get pod my-pod -o yaml                
```

## Describe commands with verbose output

```
kubectl describe nodes my-node

kubectl describe pods my-pod
```

## List Services Sorted by Name

```
kubectl get services --sort-by=.metadata.name
```

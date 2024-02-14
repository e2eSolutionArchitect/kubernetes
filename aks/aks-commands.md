
### Azure login by tenant and set subscriptions
```
az login --tenant <tenant_name>
az account set --subscription <subscription_id>
```

'kubelogin' is not recognized as an internal or external command - [click here](https://github.com/e2eSolutionArchitect/troubleshoot/blob/main/azure/aks/kubelogin%20is%20not%20recognized%20as%20an%20internal%20or%20external%20command.md)

```
# Connect to cluster
az aks get-credentials --resource-group <Resource-Group-Name> --name <Cluster-Name>

# List Kubernetes Worker Nodes
kubectl get nodes 
kubectl get nodes -o wide


# List Namespaces
kubectl get namespaces
kubectl get ns

# Get pods for namespace dev
kubectl get pods -n dev

# List Pods from all namespaces
kubectl get pods --all-namespaces

# List all k8s objects from Cluster Control plane
kubectl get all --all-namespaces

```

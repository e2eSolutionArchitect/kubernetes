

```
# Connect to cluster
az aks get-credentials --resource-group <Resource-Group-Name> --name <Cluster-Name>

# List Kubernetes Worker Nodes
kubectl get nodes 
kubectl get nodes -o wide


# List Namespaces
kubectl get namespaces
kubectl get ns

# List Pods from all namespaces
kubectl get pods --all-namespaces

# List all k8s objects from Cluster Control plane
kubectl get all --all-namespaces

```

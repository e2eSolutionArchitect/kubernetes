# Deploy NGINX controller for Ingress

### Create a separate namespace for Ingress
```
kubectl create ns ingress
```

### Install ingress-nginx using HELM in 'ingress' namespace
```
helm install my-ingress ingress-nginx/ingress-nginx -n ingress
```

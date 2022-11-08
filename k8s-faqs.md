
## How to link a Deployment with a Service
Please check the mapping of 'k8s-service-01' in below code for Deployment and Service. 
```
Under Deployment template specification. 

appVersion: apps/v1
kind: Deployment
....
spec:
....
  template:
   metadata:
    labels:
     app: k8s-service-01
     
 ----------------------------
 Under Service specification. 
 
appVersion: v1
kind: Service
....
spec:
 type:
 selector:
   app: k8s-service-01
....
 
 
 
```


## Create  EKS Cluster with Fargate profile
- Please refer here for the [AWS Cloudformation template](https://github.com/e2eSolutionArchitect/scripts/tree/main/aws/cloudformation) to provision EKS cluster with Fargate profile

## Create an EC2 to manage and configure cluster from there
- Please refer here for the [AWS Cloudformation template](https://github.com/e2eSolutionArchitect/scripts/tree/main/aws/cloudformation) to create an EC2 with AWS CLI and kubectl installed. 

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

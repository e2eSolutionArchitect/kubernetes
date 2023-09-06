
Please refer [here](https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html) for AWS documentation

Steps

Check kubectl version
```
kubectl version --short --client
```

Download kubectl Binary. e.g, version 1.27.4

```
curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/<version>/2023-08-16/bin/linux/amd64/kubectl
curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.27.4/2023-08-16/bin/linux/amd64/kubectl
```

Allow permission and set PATH
```
chmod +x ./kubectl
mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$HOME/bin:$PATH

```



## Subnets showing disabled while configuring Fargate profile for Amazon EKS
Fix [refer](https://github.com/e2eSolutionArchitect/troubleshoot/blob/main/aws/eks/subnets-disabled-configure-eks-fargate-profile.md)

## Disabled logging because aws-logging configmap was not found. configmap "aws-logging" not found
Fix [refer](https://github.com/e2eSolutionArchitect/troubleshoot/blob/main/aws/eks/Disabled%20logging%20because%20aws-logging%20configmap%20was%20not%20found.%20configmap%20aws-logging%20not%20found.md)

## Pods are not running. still showing pending
Fargate profile is hosted in private subnet. make sure you are not expecting to connect/pull (images) from public internet. If so then then make sure you have NAT Gateway enabled. Natgateway should be created in PUBLIC subnet and natgw should be attached to the PRIVATE RouteTable. 

```
  NATGateway:
    Type: AWS::EC2::NatGateway
    Properties:
        AllocationId: !GetAtt NATGatewayEIP.AllocationId
        SubnetId: !Ref PublicSubnet
        Tags:
        - Key: env
          Value: dev
  NATGatewayEIP:
    Type: AWS::EC2::EIP
    Properties:
        Domain: vpc
  RouteNATGateway:
    DependsOn: NATGateway
    Type: AWS::EC2::Route
    Properties:
        RouteTableId: !Ref PrivateRouteTable
        DestinationCidrBlock: '0.0.0.0/0'
        NatGatewayId: !Ref NATGateway

```

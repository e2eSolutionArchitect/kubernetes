

## Prerequisites
- az aks get-versions --location eastus --output table
- az aks get-upgrades --resource-group aksdemo --name askdemo 

## Version upgrade

[major].[minor].[patch] e.g 1.15.x

### Minor version upgrade 
1.15.x > 1.16.x

1.15.x could be upgraded to 1.16.x but not to 1.17.x. Because it has to upgrade by one minor version at a time. 
tO upgrade to 1.17.x, first 1.15.x  to 1.16.x then to 1.17.x

For patch version you can move to 1.15.2 to 1.15.9 skipping 1.15.7.

### Patch version upgrade 
1.15.2 > 1.16.9

***Check End of life*** of a version [here](https://learn.microsoft.com/en-us/azure/aks/supported-kubernetes-versions?tabs=azure-cli)


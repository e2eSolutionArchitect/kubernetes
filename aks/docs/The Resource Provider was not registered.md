# Error:
The Resource Provider was not registered while provisioning Azure Managed Grafa using Terraform

│ Error: creating Grafana (Subscription: "bf793555-a4bc-42e3-a520-49d84c859f19"
│ Resource Group Name: "rg-us-east-aks"
│ Grafana Name: "grafasa-dash"): performing GrafanaCreate: Put "https://management.azure.com/subscriptions/bf793555-a4bc-42e3-a520-49d84c859f19/resourceGroups/rg-us-east-aks/providers/Microsoft.Dashboard/grafana/grafasa-dash?api-version=2023-09-01": The Resource Provider was not registered

# Resolution:
```
az provider register --namespace "Microsoft.Dashboard"
```

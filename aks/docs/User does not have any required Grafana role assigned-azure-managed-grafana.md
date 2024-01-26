# Error

While opening the endpoint of Azure managed grafana dashboard ( https://grafasa-dash-dfg34tfgdfg.eus.grafana.azure.com ), receiving the below error. 

# Error details
```
The user does not have any required Grafana role assigned. They must be given at least Grafana Viewer permission in order to access a Grafana instance. Note: For newly created instances, roles may take up to an hour to propagate. Trace ID: 00-d922a7frty564rtrtyryte6-d6cc72f6f6c88ff5-00
Please check the documentation for further details.
The user does not have any required Grafana role assigned. They must be given at least Grafana Viewer permission in order to access a Grafana instance. Note: For newly created instances, roles may take up to an hour to propagate. Trace ID: 00-d922a7frty564rtrtyryte6-d6cc72f6f6c88ff5-00
Please check the documentation for further details.
https://learn.microsoft.com/en-us/azure/managed-grafana/
```

# Resolution
Navigate to 
- Azure Managed Grafana > Access Control (IAM)
- View my access. You need to have Grafana Admin role.
- Add Role Assignment > Assign the 'Grafana Admin' role to your user. and save.
- Retry the dashboard URL

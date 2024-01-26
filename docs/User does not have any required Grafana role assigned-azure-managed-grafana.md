# Error

While opening endpoin of azure managed grafana dashboard ( https://grafasa-dash-dfg34tfgdfg.eus.grafana.azure.com ) , receiving below error. 

# Error details
```
User does not have any required Grafana role assigned.They must be given at least Grafana Viewer permission in order to access a Grafana instance. Note: For newly created instances, roles may take up to an hour to propagate. Trace ID: 00-d922a7f88eebc154edbbcde040ec99e6-d6cc72f6f6c88ff5-00
Please check the documentation for further details.
User does not have any required Grafana role assigned.They must be given at least Grafana Viewer permission in order to access a Grafana instance. Note: For newly created instances, roles may take up to an hour to propagate. Trace ID: 00-d922a7f88eebc154edbbcde040ec99e6-d6cc72f6f6c88ff5-00
Please check the documentation for further details.
https://learn.microsoft.com/en-us/azure/managed-grafana/
```

# Resolution
Navigate to Azure Managed Grafana > Access Control (IAM) > Add Role Assignment > assigned 'Grafana Admin' role to your user. and save.
retry the dashboard url

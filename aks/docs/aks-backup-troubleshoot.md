

## Subscription does not enable EncryptionAtHost

https://learn.microsoft.com/en-us/answers/questions/1377548/unable-to-enable-encryption-at-host-for-azure-vm

```
Register-AzProviderFeature -FeatureName "EncryptionAtHost" -ProviderNamespace "Microsoft.Compute"
Get-AzProviderFeature -FeatureName "EncryptionAtHost" -ProviderNamespace "Microsoft.Compute"
```

https://stackoverflow.com/questions/64787022/the-term-register-azresourceprovider-is-not-recognized-as-the-name-of-a-cmdlet

az provider register --namespace "Microsoft.KubernetesConfiguration"
az provider show -n Microsoft.KubernetesConfiguration

## Protection Error UserErrorInvalidLabelSelector: Invalid label selector provided.

kubernetes.azure.com/cluster:MC_rg-aks-backup_e2eSA-Dev-cluster-57359_eastus
kubernetes.azure.com/node-image-version:AKSUbuntu-2204gen2containerd-202403.25.0

https://learn.microsoft.com/en-us/answers/questions/599385/cannot-delete-backup-vault
You can't delete a vault that contains backup data in the soft deleted state.
Cannot delete Backup Policy as it is associated with soft deleted items
Select backup valut > select 'Backup policy' > Datasource Type = 'Kubernetes Services' (by default is it not selected). It should show the backup policy and delete the backup policy manually. 
Recovery Services vault cannot be deleted as there are backup items in soft deleted state in the vault. The soft deleted items are permanently deleted after 14 days of delete operation.

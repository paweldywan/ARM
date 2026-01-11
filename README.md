# Azure Storage Account ARM Template

This repository contains an Azure Resource Manager (ARM) template for deploying a Storage Account.

## Resources Deployed

- **Storage Account** (`Microsoft.Storage/storageAccounts`)
  - Name: `sapd123`
  - Kind: StorageV2
  - SKU: Standard_LRS (Locally Redundant Storage)
  - Location: Resource Group location

## Prerequisites

- Azure subscription
- Azure PowerShell module installed
- Appropriate permissions to create resources in the target resource group

## Deployment

### Using Azure PowerShell

```powershell
$templateFile = "azuredeploy.json"
$today = Get-Date -Format "MM-dd-yyyy"
$deploymentName = "addstorage-" + "$today"
New-AzResourceGroupDeployment -Name $deploymentName -TemplateFile $templateFile
```

### Using Azure CLI

```bash
az deployment group create \
  --name addstorage-$(date +%m-%d-%Y) \
  --template-file azuredeploy.json
```

## Template Structure

- **Schema**: Uses ARM template schema version 2019-04-01
- **Parameters**: None currently defined
- **Variables**: None currently defined
- **Resources**: Single Storage Account
- **Outputs**: None currently defined

## Notes

- The storage account name must be globally unique across Azure
- The template uses the resource group's location for the storage account
- Standard_LRS provides locally redundant storage with good performance at the lowest cost

## Next Steps

Consider enhancing this template by:
- Adding parameters for storage account name, SKU, and kind
- Adding outputs to return the storage account connection string
- Adding variables for reusable values
- Implementing proper naming conventions with uniqueString()

# Azure Storage Account ARM Template

This repository contains an Azure Resource Manager (ARM) template for deploying a Storage Account with parameterized configuration.

## Resources Deployed

- **Storage Account** (`Microsoft.Storage/storageAccounts`)
  - Kind: StorageV2
  - Location: Resource Group location
  - Configurable name and SKU via parameters

## Parameters

| Parameter | Type | Description | Default | Allowed Values |
|-----------|------|-------------|---------|----------------|
| `storageName` | string | Name of the Azure storage account (3-24 characters) | *Required* | - |
| `storageSKU` | string | SKU for the storage account | `Standard_LRS` | Standard_LRS, Standard_GRS, Standard_RAGRS, Standard_ZRS, Premium_LRS, Premium_ZRS, Standard_GZRS, Standard_RAGZRS |

## Outputs

- **storageEndpoint**: Returns the primary endpoints object for the storage account, including blob, file, queue, and table endpoints

## Prerequisites

- Azure subscription
- Azure PowerShell module installed or Azure CLI
- Appropriate permissions to create resources in the target resource group

## Deployment

### Using Azure PowerShell

```powershell
$templateFile = "azuredeploy.json"
$today = Get-Date -Format "MM-dd-yyyy"
$deploymentName = "addOutputs-" + "$today"
New-AzResourceGroupDeployment `
  -Name $deploymentName `
  -TemplateFile $templateFile `
  -storageName "sapd123" `
  -storageSKU "Standard_LRS"
```

### Using Azure CLI

```bash
az deployment group create \
  --name addOutputs-$(date +%m-%d-%Y) \
  --template-file azuredeploy.json \
  --parameters storageName=sapd123 storageSKU=Standard_LRS
```

## Template Structure

- **Schema**: ARM template schema version 2019-04-01
- **Parameters**: 2 parameters (storageName, storageSKU)
- **Variables**: None
- **Resources**: Single Storage Account with parameterized configuration
- **Outputs**: Storage account primary endpoints

## Notes

- The storage account name must be globally unique across Azure (3-24 characters, lowercase letters and numbers only)
- The template uses the resource group's location for the storage account
- SKU determines the replication and performance characteristics:
  - **Standard_LRS**: Locally redundant storage (lowest cost)
  - **Standard_GRS**: Geo-redundant storage (replicated to secondary region)
  - **Standard_RAGRS**: Read-access geo-redundant storage
  - **Standard_ZRS**: Zone-redundant storage
  - **Premium_LRS/ZRS**: Premium performance (SSD-based)
  - **Standard_GZRS/RAGZRS**: Geo-zone-redundant storage

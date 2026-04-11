# Question (Day 20)

You are tasked with modifying an ARM template for deploying a virtual network. The current template is located in the /root/arm-templates directory under the filename vnet-deployment-template.json. You need to make the following changes to the template:
Change the name and displayName tag of the virtual network to arm-vnet-xfusion.
Update the addressPrefixes to 192.168.0.0/16.
Add one more tag named Environment with value KKE-xfusion.
After making these changes, you need to deploy the ARM template using the Azure CLI.

Use the following command to find out the resource group to use:
az group list --query '[].name' --output table | grep '

# Solution

```
~ ➜  cd arm-templates/

~/arm-templates ➜  ls
vnet-deployment-template.json

~/arm-templates ➜  cat vnet-deployment-template.json 
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "functions": [],
    "variables": {},
    "resources": [
        {
            "name": "virtualNetwork1",
            "type": "Microsoft.Network/virtualNetworks",
            "apiVersion": "2023-11-01",
            "location": "[resourceGroup().location]",
            "tags": {
                "displayName": "virtualNetwork1"
            },
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "10.10.10.0/24"
                    ]
                }
            }
        }
    ],
    "outputs": {
    }
}
~/arm-templates ➜  vi vnet-deployment-template.json 

~/arm-templates ➜  cat vnet-deployment-template.json 
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "functions": [],
    "variables": {},
    "resources": [
        {
            "name": "arm-vnet-xfusion",
            "type": "Microsoft.Network/virtualNetworks",
            "apiVersion": "2023-11-01",
            "location": "[resourceGroup().location]",
            "tags": {
                "displayName": "arm-vnet-xfusion",
                "Environment": "KKE-xfusion"
            },
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "192.168.0.0/16"
                    ]
                }
            }
        }
    ],
    "outputs": {
    }
}

~/arm-templates ➜  az group list --query '[].name' --output table | grep 'kml'
kml_rg_main-92f689a8be444bcf

~/arm-templates ➜  az deployment group create \
> --resource-group kml_rg_main-92f689a8be444bcf \
> --name arm-vnet-xfusion \
> --template-file vnet-deployment-template.json
{
  "id": "/subscriptions/f0c3bcdd-5ce2-4fa0-8cf3-41559747512b/resourceGroups/kml_rg_main-92f689a8be444bcf/providers/Microsoft.Resources/deployments/arm-vnet-xfusion",
  "location": null,
  "name": "arm-vnet-xfusion",
  "properties": {
    "correlationId": "53575dac-673b-4edf-91c9-3689d02d0dd9",
    "debugSetting": null,
    "dependencies": [],
    "duration": "PT3.8509536S",
    "error": null,
    "mode": "Incremental",
    "onErrorDeployment": null,
    "outputResources": [
      {
        "id": "/subscriptions/f0c3bcdd-5ce2-4fa0-8cf3-41559747512b/resourceGroups/kml_rg_main-92f689a8be444bcf/providers/Microsoft.Network/virtualNetworks/arm-vnet-xfusion",
        "resourceGroup": "kml_rg_main-92f689a8be444bcf"
      }
    ],
    "outputs": {},
    "parameters": {},
    "parametersLink": null,
    "providers": [
      {
        "id": null,
        "namespace": "Microsoft.Network",
        "providerAuthorizationConsentState": null,
        "registrationPolicy": null,
        "registrationState": null,
        "resourceTypes": [
          {
            "aliases": null,
            "apiProfiles": null,
            "apiVersions": null,
            "capabilities": null,
            "defaultApiVersion": null,
            "locationMappings": null,
            "locations": [
              "eastus"
            ],
            "properties": null,
            "resourceType": "virtualNetworks",
            "zoneMappings": null
          }
        ]
      }
    ],
    "provisioningState": "Succeeded",
    "templateHash": "8087580872373422853",
    "templateLink": null,
    "timestamp": "2026-04-09T13:45:49.955328+00:00",
    "validatedResources": null
  },
  "resourceGroup": "kml_rg_main-92f689a8be444bcf",
  "tags": null,
  "type": "Microsoft.Resources/deployments"
}

~/arm-templates ➜

```
```

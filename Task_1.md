# Question

The Nautilus DevOps team is in the process of migrating some of their workloads to Azure. One of the tasks involves creating a new Virtual Machine (VM) using the Azure CLI. The team does not have access to the Azure portal but can manage Azure resources via the azure-client host (the landing host for this lab).

1) Create a new Azure Virtual Machine named devops-vm using the Azure CLI.
2) Use the Ubuntu2204 image and set the VM size to Standard_B2s.
3) Make sure the admin username is set to azureuser and SSH keys are generated for secure access.
4) Use Standard_LRS storage account, disk size must be 30GB and ensure the VM devops-vm is in the running state after creation.

# Solution

```
~ ➜  az vm create \
  --resource-group kml_rg_main-38c1622c080b4447 \
  --name devops-vm \
  --image Ubuntu2204 \
  --size Standard_B2s \
  --admin-username azureuser \
  --os-disk-size-gb 30 \
  --storage-sku Standard_LRS \
  --generate-ssh-keys
SSH key files '/root/.ssh/id_rsa' and '/root/.ssh/id_rsa.pub' have been generated under ~/.ssh to allow SSH access to the VM. If using machines without permanent storage, back up your keys to a safe location.
{
  "fqdns": "",
  "id": "/subscriptions/f0c3bcdd-5ce2-4fa0-8cf3-41559747512b/resourceGroups/kml_rg_main-38c1622c080b4447/providers/Microsoft.Compute/virtualMachines/devops-vm",
  "location": "eastus",
  "macAddress": "7C-1E-52-59-35-19",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "20.25.47.245",
  "resourceGroup": "kml_rg_main-38c1622c080b4447",
  "zones": ""
}
```

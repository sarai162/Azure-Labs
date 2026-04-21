# Question (Azure Day 20)

The Nautilus DevOps Team has received a new request from the Development Team to set up a new Azure Virtual Machine (VM). This VM will be used to host a new application that requires a stable public IP address. To ensure that the VM has a consistent public IP, a Static Public IP address needs to be associated with it. The VM will be named xfusion-vm, and the Static Public IP will be named xfusion-pip. This setup will help the Development Team to have a reliable and consistent access point for their application.

Create an Azure VM named xfusion-vm using any available Ubuntu image, with the VM size Standard_B1s.
Generate an SSH public key on the azure-client host and associate it with the VM for SSH access.
Associate a Static Public IP address named xfusion-pip with this VM.
Ensure the VM is accessible via SSH using the generated public key.

# Solution

```
~ ➜  ssh-keygen -t rsa -b 2048 -f ~/.ssh/nautilus-vm-key -N ""
Generating public/private rsa key pair.
Your identification has been saved in /root/.ssh/nautilus-vm-key
Your public key has been saved in /root/.ssh/nautilus-vm-key.pub
The key fingerprint is:
SHA256:oY14VM77ymTeAjGDSYPXAGJwEF8Sv6tH7Lt6IiJ/R8c root@azure-client
The key's randomart image is:
+---[RSA 2048]----+
|*+=+oo  .        |
|.+.++ .+         |
|  .o.+. +        |
|    o+++ o       |
|   .o +=S        |
|    ooo E.       |
|   o.. oo .      |
|+ ..= .=.o       |
|oo+*o+  +..      |
+----[SHA256]-----+

~ ➜  az group list --output table
Name                          Location    Status
----------------------------  ----------  ---------
kml_rg_main-05a3309e5ca64729  eastus      Succeeded

~ ➜  chmod 600 ~/.ssh/nautilus-vm-key
chmod 644 ~/.ssh/nautilus-vm-key.pub

~ ➜  az network public-ip create \
  --resource-group kml_rg_main-05a3309e5ca64729 \
  --name nautilus-pip \
  --sku Standard \
  --allocation-method Static
[Coming breaking change] In the coming release, the default behavior will be changed as follows when sku is Standard and zone is not provided: For zonal regions, you will get a zone-redundant IP indicated by zones:["1","2","3"]; For non-zonal regions, you will get a non zone-redundant IP indicated by zones:null.
{
  "publicIp": {
    "ddosSettings": {
      "protectionMode": "VirtualNetworkInherited"
    },
    "etag": "W/\"682179ce-929c-43a7-904e-0e78e59e1075\"",
    "id": "/subscriptions/f0c3bcdd-5ce2-4fa0-8cf3-41559747512b/resourceGroups/kml_rg_main-05a3309e5ca64729/providers/Microsoft.Network/publicIPAddresses/nautilus-pip",
    "idleTimeoutInMinutes": 4,
    "ipAddress": "4.157.250.213",
    "ipTags": [],
    "location": "eastus",
    "name": "nautilus-pip",
    "provisioningState": "Succeeded",
    "publicIPAddressVersion": "IPv4",
    "publicIPAllocationMethod": "Static",
    "resourceGroup": "kml_rg_main-05a3309e5ca64729",
    "resourceGuid": "c9050994-bbcb-492c-bba8-22514fa39bd9",
    "sku": {
      "name": "Standard",
      "tier": "Regional"
    },
    "type": "Microsoft.Network/publicIPAddresses"
  }
}

~ ➜  az vm create \
  --resource-group kml_rg_main-05a3309e5ca64729 \
  --name nautilus-vm \
  --image Ubuntu2204 \
  --size Standard_B1s \
  --admin-username azureuser \
  --ssh-key-values ~/.ssh/nautilus-vm-key.pub \
  --public-ip-address nautilus-pip \
  --storage-sku Standard_LRS
{
  "fqdns": "",
  "id": "/subscriptions/f0c3bcdd-5ce2-4fa0-8cf3-41559747512b/resourceGroups/kml_rg_main-05a3309e5ca64729/providers/Microsoft.Compute/virtualMachines/nautilus-vm",
  "location": "eastus",
  "macAddress": "7C-1E-52-81-FC-69",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "4.157.250.213",
  "resourceGroup": "kml_rg_main-05a3309e5ca64729",
  "zones": ""
}

~ ➜  az network public-ip show \
  --resource-group kml_rg_main-05a3309e5ca64729 \
  --name nautilus-pip \
  --query ipAddress \
  -o tsv
4.157.250.213

~ ➜  ssh -i ~/.ssh/nautilus-vm-key azureuser@4.157.250.213
The authenticity of host '4.157.250.213 (4.157.250.213)' can't be established.
ECDSA key fingerprint is SHA256:VWbjp/klYW0JLZ0dnlnQtttOjenrRchlgiXRSiK2soU.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '4.157.250.213' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.8.0-1051-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Wed Apr 15 13:40:41 UTC 2026

  System load:  0.29              Processes:             107
  Usage of /:   5.6% of 28.89GB   Users logged in:       0
  Memory usage: 32%               IPv4 address for eth0: 10.0.0.4
  Swap usage:   0%

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@nautilus-vm:~$

```

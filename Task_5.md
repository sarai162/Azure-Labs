Question (Azure Day 21)

The Nautilus DevOps Team has received a new request from the Development Team to set up a new Azure Virtual Machine (VM). This VM will be used to host a new application that requires a stable public IP address. To ensure that the VM has a consistent public IP, a Static Public IP address needs to be associated with it. The VM will be named devops-vm, and the Static Public IP will be named devops-pip. This setup will help the Development Team to have a reliable and consistent access point for their application.

Create an Azure VM named devops-vm using any available Ubuntu image, with the VM size Standard_B1s.
Generate an SSH public key on the azure-client host and associate it with the VM for SSH access.
Associate a Static Public IP address named devops-pip with this VM.
Ensure the VM is accessible via SSH using the generated public key.

Solution

Azure Client Terminal 

```

~ ➜  ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /root/.ssh/id_rsa
Your public key has been saved in /root/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:UhloCmgIR7zeTuvpluaUaULd+EmOvOLL1MPVM2f/CLg root@azure-client
The key's randomart image is:
+---[RSA 3072]----+
|++o    ..        |
|ooo   o  o       |
|.  o o  o        |
|  ...o o         |
| ...o = S o      |
| ..+oO o * .     |
|  oo@o+ . . .    |
| o.+*+   . . o   |
| .+O*   E   . .  |
+----[SHA256]-----+

~ ➜  cat /root/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDTVQn1Uj/ioJpkD55ykVJThQM7RVQn3sWu8+FdfDBqsDXRrZ6O83f9AYFFmGHaywexhauaKUY4yrw8iSFzza9g7OwzNtE4SbXDC0AZf+9GMubaplu2XvYAfm6oI5k6oZ7ir75ttz5WVtCru5leMnsRVbUHnPDCrIZcQNGsRkt50zh6pttXYLJMn5rpAGbnMhtBa3U7L0RxEbRiS+dNcL+a6z3s+msNl2jakk9soOFED+BQaVVUpyuFEZTzBOg9C1V8DwHb9i9Jrej/7dDCYqpy55mzUaWBolhA/EEnChBZ7Kt/2GzUg87et8DtG/WqBFrWBXoDUlwDaXdT8wOhHCxwMB5VstBoDBaN3gJ3zAOypQ8bej8ya/rUJFOUZ4BEYnB1yhNsFkZYbVtD+8sPWyV+uyE7N87kfB/l/HUmDaqwmLVUVmyJ0Sm3DG/XZB+E89Z6lx0V/k1lQa7T9aCxjmvL3IouaP8XSdzn3UcmF2eVY+1uzcbZkHv0xRdNHafry48= root@azure-client

~ ➜ ssh azureuser@20.221.75.239
The authenticity of host '20.221.75.239 (20.221.75.239)' can't be established.
ECDSA key fingerprint is SHA256:D+p3XZSxcpHa1NmUu/fVaMzbPVj3ptMOGfio0wjnGUE.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '20.221.75.239' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 24.04.4 LTS (GNU/Linux 6.17.0-1015-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Sun May 24 07:15:01 UTC 2026

  System load:  0.38              Processes:             115
  Usage of /:   5.8% of 28.02GB   Users logged in:       0
  Memory usage: 29%               IPv4 address for eth0: 10.0.0.4
  Swap usage:   0%

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@devops-vm:~$ 

```

Steps

```
Open the Azure Portal and go to Virtual Machines.
Click Create to start creating a new VM.
Choose an Ubuntu image.
Select the VM size required for the task.
Give the VM the required name.
In the authentication section, choose SSH public key.
Generate an SSH key pair on the client machine and use the public key during VM creation.
In the networking section, create or assign a static public IP.
Make sure the VM is configured to allow SSH access.
Review the settings and create the VM.
Wait until the VM is fully deployed.
Test SSH connectivity to confirm the VM is accessible using the generated key
```

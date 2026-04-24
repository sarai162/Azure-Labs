# Question

The Nautilus DevOps Team is working on setting up a new web server for a critical application. The team lead has requested you to create an EC2 instance that will serve as a web server using Nginx. This instance will be part of the initial infrastructure setup for the Nautilus project. Ensuring that the server is correctly configured and accessible from the internet is crucial for the upcoming deployment phase.
As a member of the Nautilus DevOps Team, your task is to create an EC2 instance with the following specifications:

Instance Name: The EC2 instance must be named devops-ec2.
AMI: Use any available Ubuntu AMI to create this instance.
User Data Script: Configure the instance to run a user data script during its launch. This script should:
Install the Nginx package.
Start the Nginx service.
Security Group: Ensure that the instance allows HTTP traffic on port 80 from the internet.

# Solution

Open the EC2 service in the AWS Console.  
Click Launch instance.   
Select an appropriate Linux AMI.  
Choose an instance type.  
Configure the network and security group.  
Add an inbound rule to allow HTTP traffic on port 80 from the internet.  
Add a user data script that:  
updates the package list  
installs Nginx  
starts the Nginx service  
enables it on boot  
  
```
#!/bin/bash
apt update -y
apt install nginx -y
systemctl start nginx
systemctl enable nginx
```
  
Review the settings and launch the instance.  
Wait until the instance is running.  
Open the instance’s public IP in a browser to confirm the web server is accessible.  


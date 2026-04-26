# Question (AWS Day 27)

The Nautilus DevOps Team has received a request from the Networking Team to set up a new public VPC to support a set of public-facing services. This VPC will host various resources that need to be accessible over the internet. As part of this setup, you need to ensure the VPC has public subnets with automatic IP assignment for resources. Additionally, a new EC2 instance will be launched within this VPC to host public applications that require SSH access. This setup will enable the Networking Team to deploy and manage public-facing applications.
Create a public VPC named nautilus-pub-vpc, and a subnet named nautilus-pub-subnet under the same, make sure public IP is being auto assigned to resources under this subnet. Further, create an EC2 instance named nautilus-pub-ec2 under this VPC with instance type t2.micro. Make sure SSH port 22 is open for this instance and accessible over the internet.

# Solution

```
Create a VPC

Create and attach an Internet Gateway

Create a subnet in the VPC

Enable auto-assign public IP on the subnet

Add a route to the Internet Gateway in the route table

Associate the route table with the subnet

Create a security group allowing SSH (port 22)

Launch a t2.micro EC2 instance in that subnet

```

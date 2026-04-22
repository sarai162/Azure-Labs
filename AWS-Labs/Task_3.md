# Question (AWS Day 24)

The Nautilus DevOps team is currently working on setting up a simple application on the AWS cloud. They aim to establish an Application Load Balancer (ALB) in front of an EC2 instance where an Nginx server is currently running. While the Nginx server currently serves a sample page, the team plans to deploy the actual application later.

Set up an Application Load Balancer named nautilus-alb.
Create a target group named nautilus-tg.
Create a security group named nautilus-sg to open port 80 for the public.
Attach this security group to the ALB.
The ALB should route traffic on port 80 to port 80 of the nautilus-ec2 instance.
Make appropriate changes in the default security group attached to the EC2 instance if necessary.

# Solution

```
1. Open EC2 console and switch to the required region.

2. Identify the EC2 instance:
Note its VPC
Note its subnet(s)
Note the security group attached to it

3. Create a security group for the ALB:
Allow inbound HTTP (port 80) from 0.0.0.0/0
Attach this SG to the ALB later

4. Create a target group:
Type: Instances
Protocol: HTTP
Port: 80
VPC: same as the EC2 instance
Register the EC2 instance as the target on port 80

5. Update the EC2 security group if needed:
Allow inbound HTTP (port 80)
Source should be the ALB security group, not the public internet

6. Create the Application Load Balancer:
Type: Application Load Balancer
Scheme: Internet-facing
Choose the same VPC
Select at least two subnets in different AZs
Attach the ALB security group
Add listener on HTTP port 80
Forward traffic to the target group

7. Verify health:
Check that the target becomes healthy
Open the ALB DNS name in a browser

```

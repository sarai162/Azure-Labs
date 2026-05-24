# Question (AWS Day 31)

The Nautilus Development Team is working on a new application feature that requires a reliable and scalable database solution. To facilitate development and testing, they need a new private RDS instance. This instance will be used to store critical application data and must be provisioned using the AWS free tier to minimize costs during the initial development phase. The team has chosen MySQL as the database engine due to its compatibility with their existing systems. The DevOps team has been tasked with setting up this RDS instance, ensuring that it is correctly configured and available for use by the development team.

As a member of the Nautilus DevOps Team, your task is to perform the following:

Provision a Private RDS Instance: Create a new private RDS instance named xfusion-rds using the Full configuration database creation method, and select the Free tier template. Further, it must be a db.t3.micro type instance.
Engine Configuration: Use the MySQL engine with version 8.4.x.
Enable Storage Autoscaling: Enable storage autoscaling and set the threshold value to 50GB. Keep the rest of the configurations as default.
Instance Availability: Ensure the instance is in the available state before submitting this task.

# Solution

```
1. Log in to the AWS Console and open the RDS service.
2. Click Create database.
3. Choose the standard/full configuration option.
4. Select the Free tier template.
5. Pick MySQL as the database engine and choose the required version.
6. Set the instance type to the micro class.
7. Enable storage autoscaling and set the threshold to 50 GB.
8. Leave the rest of the settings at their default values.

Create the database and wait until its status changes to available.

```

# Question

The Nautilus DevOps team needs to set up a new EC2 instance that can be accessed securely from their landing host (aws-client). The instance should be of type t2.micro and named xfusion-ec2. A new SSH key with name id_rsa should be created on the aws-client host under the/root/.ssh/ folder, if it doesn't already exist. This key should then be added to the root user's authorised keys on the EC2 instance, allowing passwordless SSH access from the aws-client host.

# Solution 

## 1. aws-client terminal 

```
~ on ☁️  (us-east-1) ➜  ls -l /root/.ssh/id_rsa /root/.ssh/id_rsa.pub
ls: cannot access '/root/.ssh/id_rsa': No such file or directory
ls: cannot access '/root/.ssh/id_rsa.pub': No such file or directory

~ on ☁️  (us-east-1) ✖ mkdir -p /root/.ssh

~ on ☁️  (us-east-1) ➜  ssh-keygen -t rsa -b 2048 -f /root/.ssh/id_rsa -N ""
Generating public/private rsa key pair.
Your identification has been saved in /root/.ssh/id_rsa
Your public key has been saved in /root/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:F7YVk/l3lQvA+rJBCSOcHuuyPVBhBkvf55Ii9dmEH0I root@aws-client
The key's randomart image is:
+---[RSA 2048]----+
|   oo .E  ..+o  .|
|  . oOoo.  .o+ ..|
|   .+o=+o+= ... o|
|    .+. X=.+  ..o|
|   .o. =S++    ..|
|   o... .+ .     |
|    =     +      |
|   . o   .       |
|      .          |
+----[SHA256]-----+

~ on ☁️  (us-east-1) ➜  chmod 600 /root/.ssh/id_rsa

~ on ☁️  (us-east-1) ➜  chmod 644 /root/.ssh/id_rsa.pub

~ on ☁️  (us-east-1) ➜  cat /root/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDqttEQi9Dy1H5z+UJ/RTTxhlA+hiq6whnBihQdhZ/N60skuLqEvqfBXFaMOSpdY/glS1yLcz3llJsovIO4Ei+3sKtr/gxs2r2ZA9iYQOT0UyjAM9zCavm+wqjpH2fpT+rBfVJLmHui7Np/y0Qcy4AtrHVjiP7SUK7OMCs9CEm3QMrAh97u1ZGRgdk403j74fMMuZOkuCKt6DFBdV35QP2Du5I7En9tNQtclbKxXOvkjjiX+B6aw5x4u228OqFSclWEiyQBgmTI3pLJWvFBgsEWlyDOnKo80ReR3+08mi76q0DGlVCYe0kDfTeUuIQwlwZINFtPb/EE3EWQDFLW6I6t root@aws-client

~ on ☁️  (us-east-1) ➜  ssh -i /root/.ssh/id_rsa root@54.175.143.78
The authenticity of host '54.175.143.78 (54.175.143.78)' can't be established.
ECDSA key fingerprint is SHA256:5OT/xsa1jdd0MlNYkR2yv7pOFx066vhoLH94ijoXpBg.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '54.175.143.78' (ECDSA) to the list of known hosts.
   ,     #_
   ~\_  ####_        Amazon Linux 2023
  ~~  \_#####\
  ~~     \###|
  ~~       \#/ ___   https://aws.amazon.com/linux/amazon-linux-2023
   ~~       V~' '->
    ~~~         /
      ~~._.   _/
         _/ _/
       _/m/'
[root@ip-172-31-40-202 ~]# hostname
ip-172-31-40-202.ec2.internal
[root@ip-172-31-40-202 ~]#
```

## 2. ec-2 instance terminal

```
   ,     #_
   ~\_  ####_        Amazon Linux 2023
  ~~  \_#####\
  ~~     \###|
  ~~       \#/ ___   https://aws.amazon.com/linux/amazon-linux-2023
   ~~       V~' '->
    ~~~         /
      ~~._.   _/
         _/ _/
       _/m/'
Last login: Tue Apr 14 07:51:41 2026 from 18.206.107.29
[ec2-user@ip-172-31-40-202 ~]$ sudo -i
[root@ip-172-31-40-202 ~]# mkdir -p /root/.ssh
[root@ip-172-31-40-202 ~]# chmod 700 /root/.ssh
[root@ip-172-31-40-202 ~]# echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDqttEQi9Dy1H5z+UJ/RTTxhlA+hiq6whnBihQdhZ/N60skuLqEvqfBXFaMOSpdY/glS1yLcz3llJsovIO4Ei+3sKtr/gxs2r2ZA9iYQOT0UyjAM9zCavm+wqjpH2fpT+rBfVJLmHui7Np/y0Qcy4AtrHVjiP7SUK7OMCs9CEm3QMrAh97u1ZGRgdk403j74fMMuZOkuCKt6DFBdV35QP2Du5I7En9tNQtclbKxXOvkjjiX+B6aw5x4u228OqFSclWEiyQBgmTI3pLJWvFBgsEWlyDOnKo80ReR3+08mi76q0DGlVCYe0kDfTeUuIQwlwZINFtPb/EE3EWQDFLW6I6t root@aws-client" >> /root/.ssh/authorized_keys
[root@ip-172-31-40-202 ~]# chmod 600 /root/.ssh/authorized_keys
[root@ip-172-31-40-202 ~]# hostname
ip-172-31-40-202.ec2.internal
[root@ip-172-31-40-202 ~]# 
```

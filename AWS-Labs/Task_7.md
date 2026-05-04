# Question (AWS Day 29)

The Nautilus DevOps team has been tasked with demonstrating the use of VPC Peering to enable communication between two VPCs. One VPC will be a private VPC that contains a private EC2 instance, while the other will be the default public VPC containing a publicly accessible EC2 instance.

1) There is already an existing EC2 instance in the public vpc/subnet:

Name: devops-public-ec2
2) There is already an existing Private VPC:

Name: devops-private-vpc
CIDR: 10.1.0.0/16
3) There is already an existing Subnet in devops-private-vpc:

Name: devops-private-subnet
CIDR: 10.1.1.0/24
4) There is already an existing EC2 instance in the private subnet:

Name: devops-private-ec2
5) Create a Peering Connection between the Default VPC and the Private VPC:

VPC Peering Connection Name: devops-vpc-peering
6) Configure Route Tables to enable communication between the two VPCs.

Ensure the private EC2 instance is accessible from the public EC2 instance.
7) Test the Connection:

Add /root/.ssh/id_rsa.pub public key to the public EC2 instance's ec2-user's authorized_keys to make sure we are able to ssh into this instance from AWS client host. You may also need to update the security group of the private EC2 instance to allow ICMP traffic from the public/default VPC CIDR. This will enable you to ping the private instance from the public instance.
SSH into the public EC2 instance and ensure that you can ping the private EC2 instance.

# Solution

AWS Client 

```
aws-client ~ ➜  cat /root/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCuxAZ7/0lxWNyub6WdLgZ/bObiiM+hXYEkdwSIIe18l/lIBvTUL01IUiqjX22AWMW4IH/pl9hUJgz1w4q6m/v61N0zfyYxP2rpk2tU7ybDde2Q9XqxUYEeGjRmzdJzB0KTUZo6OYLoKRtLnxjnQpXSHbIgiTTrnzrQB5c231sU2RT5MfZaixcv6sWZGaJooSgvVQSAftbXZVA1ifZ8Q2F1UVL3TaQINPMCi4Cvj0uFB/owm2z8FyrMs4V49xmyy9y8ZAEHrejMUfUOcCDk0m0EKiAgXsQD6Jt9sQKTmM7faUfnmtUciXpTVJxjoVDinAZxGWrmozGVMKvl6QRqRyCh root@aws-client

aws-client ~ ➜  ssh ec2-user@44.223.17.191
The authenticity of host '44.223.17.191 (44.223.17.191)' can't be established.
ECDSA key fingerprint is SHA256:pd+9lxcc6g2ytciBlEDQCAHl8CE3XOzKIKhCxrkhQi4.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '44.223.17.191' (ECDSA) to the list of known hosts.

A newer release of "Amazon Linux" is available.
  Version 2023.10.20260105:
  Version 2023.10.20260120:
  Version 2023.10.20260202:
  Version 2023.10.20260216:
  Version 2023.10.20260302:
  Version 2023.10.20260325:
  Version 2023.10.20260330:
  Version 2023.11.20260406:
  Version 2023.11.20260413:
  Version 2023.5.20241001:
  Version 2023.6.20241010:
  Version 2023.6.20241028:
  Version 2023.6.20241031:
  Version 2023.6.20241111:
  Version 2023.6.20241121:
  Version 2023.6.20241212:
  Version 2023.6.20250107:
  Version 2023.6.20250115:
  Version 2023.6.20250123:
  Version 2023.6.20250128:
  Version 2023.6.20250203:
  Version 2023.6.20250211:
  Version 2023.6.20250218:
  Version 2023.6.20250303:
  Version 2023.6.20250317:
  Version 2023.7.20250331:
  Version 2023.7.20250414:
  Version 2023.7.20250428:
  Version 2023.7.20250512:
  Version 2023.7.20250527:
  Version 2023.7.20250609:
  Version 2023.7.20250623:
  Version 2023.8.20250707:
  Version 2023.8.20250715:
  Version 2023.8.20250721:
  Version 2023.8.20250808:
  Version 2023.8.20250818:
  Version 2023.8.20250908:
  Version 2023.8.20250915:
  Version 2023.9.20250929:
  Version 2023.9.20251014:
  Version 2023.9.20251020:
  Version 2023.9.20251027:
  Version 2023.9.20251105:
  Version 2023.9.20251110:
  Version 2023.9.20251117:
  Version 2023.9.20251208:
Run "/usr/bin/dnf check-release-update" for full release and version update info
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
Last login: Mon Apr 27 12:43:01 2026 from 18.206.107.28
[ec2-user@ip-172-31-29-151 ~]$ ping 10.1.1.206
PING 10.1.1.206 (10.1.1.206) 56(84) bytes of data.
64 bytes from 10.1.1.206: icmp_seq=1 ttl=127 time=1.94 ms
64 bytes from 10.1.1.206: icmp_seq=2 ttl=127 time=1.17 ms
64 bytes from 10.1.1.206: icmp_seq=3 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=4 ttl=127 time=1.09 ms
64 bytes from 10.1.1.206: icmp_seq=5 ttl=127 time=1.12 ms
64 bytes from 10.1.1.206: icmp_seq=6 ttl=127 time=1.20 ms
64 bytes from 10.1.1.206: icmp_seq=7 ttl=127 time=1.14 ms
64 bytes from 10.1.1.206: icmp_seq=8 ttl=127 time=1.17 ms
64 bytes from 10.1.1.206: icmp_seq=9 ttl=127 time=1.14 ms
64 bytes from 10.1.1.206: icmp_seq=10 ttl=127 time=1.13 ms
64 bytes from 10.1.1.206: icmp_seq=11 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=12 ttl=127 time=1.21 ms
64 bytes from 10.1.1.206: icmp_seq=13 ttl=127 time=1.14 ms
64 bytes from 10.1.1.206: icmp_seq=14 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=15 ttl=127 time=1.14 ms
64 bytes from 10.1.1.206: icmp_seq=16 ttl=127 time=1.18 ms
64 bytes from 10.1.1.206: icmp_seq=17 ttl=127 time=1.09 ms
64 bytes from 10.1.1.206: icmp_seq=18 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=19 ttl=127 time=1.17 ms
64 bytes from 10.1.1.206: icmp_seq=20 ttl=127 time=1.04 ms
64 bytes from 10.1.1.206: icmp_seq=21 ttl=127 time=1.15 ms
64 bytes from 10.1.1.206: icmp_seq=22 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=23 ttl=127 time=0.981 ms
64 bytes from 10.1.1.206: icmp_seq=24 ttl=127 time=1.03 ms
64 bytes from 10.1.1.206: icmp_seq=25 ttl=127 time=1.02 ms
64 bytes from 10.1.1.206: icmp_seq=26 ttl=127 time=1.04 ms
64 bytes from 10.1.1.206: icmp_seq=27 ttl=127 time=1.06 ms
64 bytes from 10.1.1.206: icmp_seq=28 ttl=127 time=1.04 ms
64 bytes from 10.1.1.206: icmp_seq=29 ttl=127 time=1.03 ms
64 bytes from 10.1.1.206: icmp_seq=30 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=31 ttl=127 time=1.15 ms
64 bytes from 10.1.1.206: icmp_seq=32 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=33 ttl=127 time=1.17 ms
64 bytes from 10.1.1.206: icmp_seq=34 ttl=127 time=1.69 ms
64 bytes from 10.1.1.206: icmp_seq=35 ttl=127 time=1.15 ms
64 bytes from 10.1.1.206: icmp_seq=36 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=37 ttl=127 time=1.11 ms
64 bytes from 10.1.1.206: icmp_seq=38 ttl=127 time=1.06 ms
64 bytes from 10.1.1.206: icmp_seq=39 ttl=127 time=1.05 ms
64 bytes from 10.1.1.206: icmp_seq=40 ttl=127 time=1.09 ms
64 bytes from 10.1.1.206: icmp_seq=41 ttl=127 time=1.06 ms
64 bytes from 10.1.1.206: icmp_seq=42 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=43 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=44 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=45 ttl=127 time=1.05 ms
64 bytes from 10.1.1.206: icmp_seq=46 ttl=127 time=1.09 ms
64 bytes from 10.1.1.206: icmp_seq=47 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=48 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=49 ttl=127 time=1.16 ms
64 bytes from 10.1.1.206: icmp_seq=50 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=51 ttl=127 time=1.04 ms
64 bytes from 10.1.1.206: icmp_seq=52 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=53 ttl=127 time=1.04 ms
64 bytes from 10.1.1.206: icmp_seq=54 ttl=127 time=1.15 ms
64 bytes from 10.1.1.206: icmp_seq=55 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=56 ttl=127 time=1.06 ms
64 bytes from 10.1.1.206: icmp_seq=57 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=58 ttl=127 time=1.04 ms
64 bytes from 10.1.1.206: icmp_seq=59 ttl=127 time=1.09 ms
64 bytes from 10.1.1.206: icmp_seq=60 ttl=127 time=1.17 ms
64 bytes from 10.1.1.206: icmp_seq=61 ttl=127 time=1.06 ms
64 bytes from 10.1.1.206: icmp_seq=62 ttl=127 time=1.09 ms
64 bytes from 10.1.1.206: icmp_seq=63 ttl=127 time=1.06 ms
64 bytes from 10.1.1.206: icmp_seq=64 ttl=127 time=1.06 ms
64 bytes from 10.1.1.206: icmp_seq=65 ttl=127 time=1.13 ms
64 bytes from 10.1.1.206: icmp_seq=66 ttl=127 time=1.11 ms
64 bytes from 10.1.1.206: icmp_seq=67 ttl=127 time=1.12 ms
64 bytes from 10.1.1.206: icmp_seq=68 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=69 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=70 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=71 ttl=127 time=1.12 ms
64 bytes from 10.1.1.206: icmp_seq=72 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=73 ttl=127 time=1.09 ms
64 bytes from 10.1.1.206: icmp_seq=74 ttl=127 time=1.04 ms
64 bytes from 10.1.1.206: icmp_seq=75 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=76 ttl=127 time=1.09 ms
64 bytes from 10.1.1.206: icmp_seq=77 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=78 ttl=127 time=1.11 ms
64 bytes from 10.1.1.206: icmp_seq=79 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=80 ttl=127 time=1.19 ms
64 bytes from 10.1.1.206: icmp_seq=81 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=82 ttl=127 time=1.05 ms
64 bytes from 10.1.1.206: icmp_seq=83 ttl=127 time=1.09 ms
64 bytes from 10.1.1.206: icmp_seq=84 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=85 ttl=127 time=1.18 ms
64 bytes from 10.1.1.206: icmp_seq=86 ttl=127 time=1.12 ms
64 bytes from 10.1.1.206: icmp_seq=87 ttl=127 time=1.14 ms
64 bytes from 10.1.1.206: icmp_seq=88 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=89 ttl=127 time=1.14 ms
64 bytes from 10.1.1.206: icmp_seq=90 ttl=127 time=1.11 ms
64 bytes from 10.1.1.206: icmp_seq=91 ttl=127 time=1.16 ms
64 bytes from 10.1.1.206: icmp_seq=92 ttl=127 time=1.14 ms
64 bytes from 10.1.1.206: icmp_seq=93 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=94 ttl=127 time=1.11 ms
64 bytes from 10.1.1.206: icmp_seq=95 ttl=127 time=1.14 ms
64 bytes from 10.1.1.206: icmp_seq=96 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=97 ttl=127 time=1.14 ms
64 bytes from 10.1.1.206: icmp_seq=98 ttl=127 time=1.06 ms
64 bytes from 10.1.1.206: icmp_seq=99 ttl=127 time=1.13 ms
64 bytes from 10.1.1.206: icmp_seq=100 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=101 ttl=127 time=1.04 ms
64 bytes from 10.1.1.206: icmp_seq=102 ttl=127 time=1.05 ms
64 bytes from 10.1.1.206: icmp_seq=103 ttl=127 time=1.09 ms
64 bytes from 10.1.1.206: icmp_seq=104 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=105 ttl=127 time=1.11 ms
64 bytes from 10.1.1.206: icmp_seq=106 ttl=127 time=1.11 ms
64 bytes from 10.1.1.206: icmp_seq=107 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=108 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=109 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=110 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=111 ttl=127 time=1.06 ms
64 bytes from 10.1.1.206: icmp_seq=112 ttl=127 time=1.05 ms
64 bytes from 10.1.1.206: icmp_seq=113 ttl=127 time=1.06 ms
64 bytes from 10.1.1.206: icmp_seq=114 ttl=127 time=1.21 ms
64 bytes from 10.1.1.206: icmp_seq=115 ttl=127 time=1.42 ms
64 bytes from 10.1.1.206: icmp_seq=116 ttl=127 time=1.06 ms
64 bytes from 10.1.1.206: icmp_seq=117 ttl=127 time=1.12 ms
64 bytes from 10.1.1.206: icmp_seq=118 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=119 ttl=127 time=1.02 ms
64 bytes from 10.1.1.206: icmp_seq=120 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=121 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=122 ttl=127 time=1.09 ms
64 bytes from 10.1.1.206: icmp_seq=123 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=124 ttl=127 time=1.05 ms
64 bytes from 10.1.1.206: icmp_seq=125 ttl=127 time=1.13 ms
64 bytes from 10.1.1.206: icmp_seq=126 ttl=127 time=1.67 ms
64 bytes from 10.1.1.206: icmp_seq=127 ttl=127 time=1.12 ms
64 bytes from 10.1.1.206: icmp_seq=128 ttl=127 time=1.09 ms
64 bytes from 10.1.1.206: icmp_seq=129 ttl=127 time=1.15 ms
64 bytes from 10.1.1.206: icmp_seq=130 ttl=127 time=1.09 ms
64 bytes from 10.1.1.206: icmp_seq=131 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=132 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=133 ttl=127 time=1.09 ms
64 bytes from 10.1.1.206: icmp_seq=134 ttl=127 time=1.15 ms
64 bytes from 10.1.1.206: icmp_seq=135 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=136 ttl=127 time=1.19 ms
64 bytes from 10.1.1.206: icmp_seq=137 ttl=127 time=1.11 ms
64 bytes from 10.1.1.206: icmp_seq=138 ttl=127 time=1.09 ms
64 bytes from 10.1.1.206: icmp_seq=139 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=140 ttl=127 time=1.15 ms
64 bytes from 10.1.1.206: icmp_seq=141 ttl=127 time=1.12 ms
64 bytes from 10.1.1.206: icmp_seq=142 ttl=127 time=1.22 ms
64 bytes from 10.1.1.206: icmp_seq=143 ttl=127 time=1.12 ms
64 bytes from 10.1.1.206: icmp_seq=144 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=145 ttl=127 time=1.02 ms
64 bytes from 10.1.1.206: icmp_seq=146 ttl=127 time=1.04 ms
64 bytes from 10.1.1.206: icmp_seq=147 ttl=127 time=1.11 ms
64 bytes from 10.1.1.206: icmp_seq=148 ttl=127 time=1.04 ms
64 bytes from 10.1.1.206: icmp_seq=149 ttl=127 time=1.11 ms
64 bytes from 10.1.1.206: icmp_seq=150 ttl=127 time=1.05 ms
64 bytes from 10.1.1.206: icmp_seq=151 ttl=127 time=1.19 ms
64 bytes from 10.1.1.206: icmp_seq=152 ttl=127 time=1.02 ms
64 bytes from 10.1.1.206: icmp_seq=153 ttl=127 time=1.12 ms
64 bytes from 10.1.1.206: icmp_seq=154 ttl=127 time=1.15 ms
64 bytes from 10.1.1.206: icmp_seq=155 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=156 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=157 ttl=127 time=1.11 ms
64 bytes from 10.1.1.206: icmp_seq=158 ttl=127 time=1.09 ms
64 bytes from 10.1.1.206: icmp_seq=159 ttl=127 time=1.18 ms
64 bytes from 10.1.1.206: icmp_seq=160 ttl=127 time=1.09 ms
64 bytes from 10.1.1.206: icmp_seq=161 ttl=127 time=1.16 ms
64 bytes from 10.1.1.206: icmp_seq=162 ttl=127 time=1.16 ms
64 bytes from 10.1.1.206: icmp_seq=163 ttl=127 time=1.17 ms
64 bytes from 10.1.1.206: icmp_seq=164 ttl=127 time=1.18 ms
64 bytes from 10.1.1.206: icmp_seq=165 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=166 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=167 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=168 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=169 ttl=127 time=1.12 ms
64 bytes from 10.1.1.206: icmp_seq=170 ttl=127 time=1.06 ms
64 bytes from 10.1.1.206: icmp_seq=171 ttl=127 time=1.12 ms
64 bytes from 10.1.1.206: icmp_seq=172 ttl=127 time=1.13 ms
64 bytes from 10.1.1.206: icmp_seq=173 ttl=127 time=1.05 ms
64 bytes from 10.1.1.206: icmp_seq=174 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=175 ttl=127 time=1.14 ms
64 bytes from 10.1.1.206: icmp_seq=176 ttl=127 time=1.17 ms
64 bytes from 10.1.1.206: icmp_seq=177 ttl=127 time=1.12 ms
64 bytes from 10.1.1.206: icmp_seq=178 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=179 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=180 ttl=127 time=1.23 ms
64 bytes from 10.1.1.206: icmp_seq=181 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=182 ttl=127 time=1.06 ms
64 bytes from 10.1.1.206: icmp_seq=183 ttl=127 time=1.04 ms
64 bytes from 10.1.1.206: icmp_seq=184 ttl=127 time=1.11 ms
64 bytes from 10.1.1.206: icmp_seq=185 ttl=127 time=1.11 ms
64 bytes from 10.1.1.206: icmp_seq=186 ttl=127 time=1.11 ms
64 bytes from 10.1.1.206: icmp_seq=187 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=188 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=189 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=190 ttl=127 time=2.87 ms
64 bytes from 10.1.1.206: icmp_seq=191 ttl=127 time=1.06 ms
64 bytes from 10.1.1.206: icmp_seq=192 ttl=127 time=1.06 ms
64 bytes from 10.1.1.206: icmp_seq=193 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=194 ttl=127 time=1.04 ms
64 bytes from 10.1.1.206: icmp_seq=195 ttl=127 time=1.06 ms
64 bytes from 10.1.1.206: icmp_seq=196 ttl=127 time=1.04 ms
64 bytes from 10.1.1.206: icmp_seq=197 ttl=127 time=1.13 ms
64 bytes from 10.1.1.206: icmp_seq=198 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=199 ttl=127 time=1.12 ms
64 bytes from 10.1.1.206: icmp_seq=200 ttl=127 time=1.14 ms
64 bytes from 10.1.1.206: icmp_seq=201 ttl=127 time=1.06 ms
64 bytes from 10.1.1.206: icmp_seq=202 ttl=127 time=1.11 ms
64 bytes from 10.1.1.206: icmp_seq=203 ttl=127 time=1.15 ms
64 bytes from 10.1.1.206: icmp_seq=204 ttl=127 time=1.14 ms
64 bytes from 10.1.1.206: icmp_seq=205 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=206 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=207 ttl=127 time=1.13 ms
64 bytes from 10.1.1.206: icmp_seq=208 ttl=127 time=1.12 ms
64 bytes from 10.1.1.206: icmp_seq=209 ttl=127 time=1.05 ms
64 bytes from 10.1.1.206: icmp_seq=210 ttl=127 time=1.09 ms
64 bytes from 10.1.1.206: icmp_seq=211 ttl=127 time=1.13 ms
64 bytes from 10.1.1.206: icmp_seq=212 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=213 ttl=127 time=1.18 ms
64 bytes from 10.1.1.206: icmp_seq=214 ttl=127 time=1.09 ms
64 bytes from 10.1.1.206: icmp_seq=215 ttl=127 time=1.09 ms
64 bytes from 10.1.1.206: icmp_seq=216 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=217 ttl=127 time=1.15 ms
64 bytes from 10.1.1.206: icmp_seq=218 ttl=127 time=1.06 ms
64 bytes from 10.1.1.206: icmp_seq=219 ttl=127 time=1.12 ms
64 bytes from 10.1.1.206: icmp_seq=220 ttl=127 time=1.13 ms
64 bytes from 10.1.1.206: icmp_seq=221 ttl=127 time=1.12 ms
64 bytes from 10.1.1.206: icmp_seq=222 ttl=127 time=1.02 ms
64 bytes from 10.1.1.206: icmp_seq=223 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=224 ttl=127 time=1.04 ms
64 bytes from 10.1.1.206: icmp_seq=225 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=226 ttl=127 time=1.13 ms
64 bytes from 10.1.1.206: icmp_seq=227 ttl=127 time=4.90 ms
64 bytes from 10.1.1.206: icmp_seq=228 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=229 ttl=127 time=1.12 ms
64 bytes from 10.1.1.206: icmp_seq=230 ttl=127 time=1.14 ms
64 bytes from 10.1.1.206: icmp_seq=231 ttl=127 time=1.12 ms
64 bytes from 10.1.1.206: icmp_seq=232 ttl=127 time=1.14 ms
64 bytes from 10.1.1.206: icmp_seq=233 ttl=127 time=1.03 ms
64 bytes from 10.1.1.206: icmp_seq=234 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=235 ttl=127 time=1.06 ms
64 bytes from 10.1.1.206: icmp_seq=236 ttl=127 time=1.05 ms
64 bytes from 10.1.1.206: icmp_seq=237 ttl=127 time=1.14 ms
64 bytes from 10.1.1.206: icmp_seq=238 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=239 ttl=127 time=1.07 ms
64 bytes from 10.1.1.206: icmp_seq=240 ttl=127 time=1.10 ms
64 bytes from 10.1.1.206: icmp_seq=241 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=242 ttl=127 time=1.05 ms
64 bytes from 10.1.1.206: icmp_seq=243 ttl=127 time=1.06 ms
64 bytes from 10.1.1.206: icmp_seq=244 ttl=127 time=1.05 ms
64 bytes from 10.1.1.206: icmp_seq=245 ttl=127 time=1.84 ms
64 bytes from 10.1.1.206: icmp_seq=246 ttl=127 time=1.08 ms
64 bytes from 10.1.1.206: icmp_seq=247 ttl=127 time=1.09 ms
^C
--- 10.1.1.206 ping statistics ---
247 packets transmitted, 247 received, 0% packet loss, time 246325ms
rtt min/avg/max/mdev = 0.981/1.132/4.898/0.282 ms
[ec2-user@ip-172-31-29-151 ~]$ ^C
[ec2-user@ip-172-31-29-151 ~]$ 
```

EC2 Instance (Public)

```
[ec2-user@ip-172-31-29-151 ~]$ sudo mkdir -p /home/ec2-user/.ssh
sudo chmod 700 /home/ec2-user/.ssh
sudo chown -R ec2-user:ec2-user /home/ec2-user/.ssh
echo 'ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCuxAZ7/0lxWNyub6WdLgZ/bObiiM+hXYEkdwSIIe18l/lIBvTUL01IUiqjX22AWMW4IH/pl9hUJgz1w4q6m/v61N0zfyYxP2rpk2tU7ybDde2Q9XqxUYEeGjRmzdJzB0KTUZo6OYLoKRtLnxjnQpXSHbIgiTTrnzrQB5c231sU2RT5MfZaixcv6sWZGaJooSgvVQSAftbXZVA1ifZ8Q2F1UVL3TaQINPMCi4Cvj0uFB/owm2z8FyrMs4V49xmyy9y8ZAEHrejMUfUOcCDk0m0EKiAgXsQD6Jt9sQKTmM7faUfnmtUciXpTVJxjoVDinAZxWGrmozGVMKvl6QRqRyCh root@aws-client' | sudo tee -a /home/ec2-user/.ssh/authorized_keys >/dev/null
sudo chmod 600 /home/ec2-user/.ssh/authorized_keys
sudo chown ec2-user:ec2-user /home/ec2-user/.ssh/authorized_keys
cat /home/ec2-user/.ssh/authorized_keys
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCuxAZ7/0lxWNyub6WdLgZ/bObiiM+hXYEkdwSIIe18l/lIBvTUL01IUiqjX22AWMW4IH/pl9hUJgz1w4q6m/v61N0zfyYxP2rpk2tU7ybDde2Q9XqxUYEeGjRmzdJzB0KTUZo6OYLoKRtLnxjnQpXSHbIgiTTrnzrQB5c231sU2RT5MfZaixcv6sWZGaJooSgvVQSAftbXZVA1ifZ8Q2F1UVL3TaQINPMCi4Cvj0uFB/owm2z8FyrMs4V49xmyy9y8ZAEHrejMUfUOcCDk0m0EKiAgXsQD6Jt9sQKTmM7faUfnmtUciXpTVJxjoVDinAZxGWrmozGVMKvl6QRqRyCh root@aws-client
```

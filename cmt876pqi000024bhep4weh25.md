---
title: "AWS Day 49: Centralized Audit Logging with VPC Peering"
seoTitle: "AWS Day 49: Centralized Audit Logging with VPC Peering"
seoDescription: "AWS Day 49: Centralized Audit Logging with VPC Peering"
datePublished: 2026-08-25T05:00:00.000Z
cuid: cmt876pqi000024bhep4weh25
slug: aws-day-49-centralized-audit-logging-with-vpc-peering
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/7bc49f6a-6a29-47d2-81a9-6f26c31f6c47.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/779c272b-b987-496a-ade6-20e2a81311e9.png
tags: aws, s3, vpc, kodekloud, anand-raval

---

Continuing my **KodeKloud 100 Days of Cloud** journey, Day 49 focused on building a simple **centralized logging architecture using Amazon VPC, VPC Peering, EC2, IAM, S3, and Linux cron jobs**.

The goal was to take a log file from an EC2 instance inside a private VPC, transfer it securely to an EC2 instance in a public VPC, and finally upload it to an S3 bucket.

The overall flow was:

```plaintext
Private EC2
    |
    | SCP
    v
Public EC2
    |
    | AWS CLI
    v
Private S3 Bucket
```

## Step 1: Create the Public VPC

I created a new VPC named:

```plaintext
datacenter-pub-vpc
```

with the CIDR:

```plaintext
10.0.0.0/24
```

The existing private VPC was using:

```plaintext
10.10.0.0/16
```

Using different CIDR ranges is important because the two VPCs need non-overlapping address spaces for VPC Peering.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/4347e143-e79b-44ce-928f-ffedf104ff84.png align="center")

## Step 2: Create the Public Subnet

Inside the new VPC, I created:

```plaintext
datacenter-pub-subnet
```

with:

```plaintext
10.0.0.0/25
```

This subnet was used for the public EC2 instance.

I also created the route table:

```plaintext
datacenter-pub-rt
```

and associated it with the public subnet.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/035ad164-1e99-40fd-81e8-46dc0b546436.png align="center")

## Step 3: Configure Internet Gateway

To provide internet connectivity to the public subnet, I created:

```plaintext
datacenter-pub-ig
```

and attached it to:

```plaintext
datacenter-pub-vpc
```

Then I added the default internet route:

```plaintext
0.0.0.0/0
    |
    v
Internet Gateway
```

This allows the EC2 instance in the public subnet to communicate with the internet.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/997d6f81-4270-4ea1-a519-a0a6c98ee31a.png align="center")

## Step 4: Launch the Public EC2 Instance

I launched an Ubuntu EC2 instance named:

```plaintext
datacenter-pub-ec2
```

inside the public subnet.

The same SSH key pair used by the private instance was used so that I could establish connectivity between the two instances.

The basic connectivity path was:

```plaintext
datacenter-priv-ec2
        |
        | VPC Peering
        v
datacenter-pub-ec2
```

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/58b6264a-c55a-4e38-abdd-91d5bdf70636.png align="center")

## Step 5: Create the IAM Role for S3

Next, I created the IAM role:

```plaintext
datacenter-s3-role
```

The role was attached to the public EC2 instance.

The purpose of this role is to allow the EC2 instance to upload logs to S3 without storing AWS access keys directly on the server.

The required permission is essentially:

```plaintext
s3:PutObject
```

for the required S3 bucket.

This is a better approach than putting an AWS access key and secret key inside a script or cron job.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/8d09e883-f554-4afb-951e-4a111d15c3a7.png align="center")

## Step 6: Create the S3 Bucket

I created the private S3 bucket:

```plaintext
datacenter-s3-logs-18106
```

The bucket is used as the final centralized destination for the logs.

The required object path is:

```plaintext
datacenter-priv-vpc/boot/boots.log
```

So the final structure looks like:

```plaintext
datacenter-s3-logs-18106
└── datacenter-priv-vpc
    └── boot
        └── boots.log
```

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/47850677-aa80-43f4-868b-db527a34656e.png align="center")

## Step 7: Configure VPC Peering

To allow private and public VPC resources to communicate, I created:

```plaintext
datacenter-vpc-peering
```

between:

```plaintext
datacenter-priv-vpc
```

and:

```plaintext
datacenter-pub-vpc
```

The important part is that VPC Peering itself does not automatically add routes.

Both route tables need routes for the opposite VPC CIDR.

For the private route table:

```plaintext
Destination: 10.0.0.0/24
Target: VPC Peering Connection
```

For the public route table:

```plaintext
Destination: 10.10.0.0/16
Target: VPC Peering Connection
```

This allows traffic between the two VPCs through the peering connection.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/fde5c4e9-36d5-4ad6-8ef1-c7c0b047e7e7.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/8345c979-2887-499c-a48f-413e70c10356.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/f36f436e-592c-4043-b4b4-9978ed09d150.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/bf8a73f6-865e-48b9-a4c9-24084b5a4f35.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/daa7aa6d-e5d3-4b98-bb84-2e363af70953.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/48689b26-a379-4a59-b143-03ff621ea216.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/a58b6876-e4ca-46f3-bf1a-c0449dd8b6d0.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/602b1ca3-e051-43c4-bea1-db2837a14328.png align="center")

## Step 8: Test SSH Connectivity

After configuring the peering connection and routes, I tested connectivity from the private instance to the public instance.

I used the existing SSH key:

```plaintext
ssh -i datacenter-key.pem ubuntu@10.10.1.12
```

The first connection prompted for host verification, after which the host was added to `known_hosts`.

The important point here was that communication between the instances was happening through **private IP addresses and VPC Peering**, rather than sending the traffic over the public internet.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/f583a077-03d2-487f-9439-4b83276f66d9.png align="center")

## Step 9: Configure Cron on the Private Instance

The private instance contains the log file:

```plaintext
/var/log/boots.log
```

I configured a cron job to periodically copy this file to the public EC2 instance using `scp`.

Example:

```plaintext
* * * * * scp -i /root/datacenter-key.pem /var/log/boots.log ubuntu@10.0.0.4:/tmp/boots.log
```

The important part is the flow:

```plaintext
Private EC2
    |
    | SCP over private IP
    v
Public EC2
```

This avoids exposing the private instance directly to the internet.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/9dcac1c4-e169-441c-89fa-db839fa53305.png align="center")

## Step 10: Configure Cron on the Public Instance

Once the log reaches the public EC2 instance, another cron job uploads it to S3.

For example:

```plaintext
* * * * * aws s3 cp /tmp/boots.log s3://datacenter-s3-logs-18106/datacenter-priv-vpc/boot/boots.log
```

Because the EC2 instance has the appropriate IAM role, the AWS CLI can use the instance role credentials automatically.

No static AWS credentials are required in the cron job.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/bce29df0-a7b7-48a4-a9df-4bb98e532ed7.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/a50b88ad-30a9-4b88-ab4c-e01c07911b12.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/0f511f08-9012-433f-8b86-fae763d034dd.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/8da549d5-b6eb-4fe4-a0da-3aa58f44c029.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/918720fe-4649-4bae-a336-f125e6edcee0.png align="center")

## Conclusion

AWS Day 49 was a practical exercise in connecting **AWS networking, security, storage, and Linux automation**.

The most useful part was seeing the complete flow from a log generated on a private EC2 instance to centralized storage in S3:

```plaintext
Private EC2 → VPC Peering → Public EC2 → S3
```

It was another hands-on step in understanding how **AWS networking and DevOps automation** can be combined to build a reliable logging workflow.
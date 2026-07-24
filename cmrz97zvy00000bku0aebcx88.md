---
title: "AWS Day 37: Managing EC2 Access with S3 Role-based Permissions | KodeKloud 100 Days of Cloud"
seoTitle: "Day 37: Managing EC2 Access with S3 Role-based Permissions"
seoDescription: "Learn how to securely grant an EC2 instance access to Amazon S3 using IAM Roles and Policies. This guide covers S3 bucket creation, IAM Policy"
datePublished: 2026-07-24T18:08:59.041Z
cuid: cmrz97zvy00000bku0aebcx88
slug: aws-day-37-managing-ec2-access-with-s3-role-based-permissions-kodekloud-100-days-of-cloud
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/7cab0b8c-c12c-473f-936d-250a6c7eeca2.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/5f3f30ae-68b9-4b67-b1c3-c15587393766.png
tags: aws, s3, iam, kodekloud, anand-raval

---

On **Day 37** of the **KodeKloud 100 Days of Cloud Challenge**, I explored one of the AWS security best practices—granting an EC2 instance access to Amazon S3 using **IAM Roles** instead of storing AWS credentials on the server.

In this lab, I created a private S3 bucket, configured an IAM policy with least-privilege permissions, created an IAM role, attached it to an EC2 instance, and verified secure access by uploading and listing files using the AWS CLI.

## Why Use IAM Roles for EC2?

Instead of storing AWS Access Keys on an EC2 instance, AWS recommends using **IAM Roles**.

Benefits include:

*   No hardcoded AWS credentials
    
*   Automatic temporary credential rotation
    
*   Improved security
    
*   Least-privilege access
    
*   Easier permission management
    
*   Better compliance with AWS security best practices
    

When an IAM Role is attached to an EC2 instance, temporary credentials are automatically provided through the **Instance Metadata Service (IMDS)**.

## Lab Objective

The goal of this lab was to:

*   Generate SSH keys on the aws-client host
    
*   Enable password-less SSH access to the EC2 instance
    
*   Create a private S3 bucket
    
*   Create an IAM policy with S3 permissions
    
*   Create an IAM role
    
*   Attach the IAM role to the EC2 instance
    
*   Upload a file to Amazon S3 using the AWS CLI
    
*   Verify access by listing bucket contents
    

## Architecture Overview

The completed architecture is shown below.

```plaintext
                +----------------------+
                |      AWS S3 Bucket   |
                |  devops-s3-959313683568 |
                +----------▲-----------+
                           │
                  IAM Role Permissions
                           │
                +----------▼-----------+
                |     EC2 Instance     |
                |     devops-ec2       |
                +----------▲-----------+
                           │
                     SSH Access
                           │
                     aws-client Host
```

The EC2 instance securely communicates with Amazon S3 using temporary credentials obtained from the attached IAM Role.

## Step 1: Generate SSH Keys

The first task was generating a new SSH key pair on the **aws-client** host.

```shell
ssh-keygen
```

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/bcff0ea1-4017-4b26-a1c6-925678550096.png align="center")

This generated:

```plaintext
/root/.ssh/id_rsa
/root/.ssh/id_rsa.pub
```

The public key was then copied to the EC2 instance.

```plaintext
cat ~/.ssh/id_rsa.pub
```

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/f2a762cf-e266-420c-be53-8d3b53597fb0.png align="center")

On the EC2 instance:

```plaintext
cat >> ~/.ssh/authorized_keys
```

This enabled password-less SSH authentication.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/6b719a9e-0db7-4d3d-8f94-f966d0b5413e.png align="center")

## Step 2: Create a Private Amazon S3 Bucket

Next, I created a private Amazon S3 bucket.

Configuration:

| Setting | Value |
| --- | --- |
| Bucket Name | devops-s3-959313683568 |
| Bucket Type | General Purpose |
| Access | Private |
| Region | us-east-1 |

No public access was enabled, keeping the bucket secure.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/0a77989c-9bbd-4153-87a4-374461781979.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/e07ad085-e7df-464e-8432-2dc549920dae.png align="center")

## Step 3: Create an IAM Policy

I created a custom IAM policy that grants only the required permissions for the S3 bucket.

Allowed Actions:

*   s3:ListBucket
    
*   s3:GetObject
    
*   s3:PutObject
    

The policy was restricted to:

```plaintext
devops-s3-959313683568
```

This follows the AWS **Least Privilege Principle**, allowing access only to the required bucket.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/7122d90a-5b89-4210-89c9-29be4efb1ee6.png align="center")

## Step 4: Create an IAM Role

Next, I created an IAM Role for Amazon EC2.

Configuration:

| Setting | Value |
| --- | --- |
| Trusted Service | EC2 |
| Role Name | devops-role |

The custom S3 policy was attached to this role.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/f182e52b-094c-44d9-8488-b84ac2cb2491.png align="center")

## Step 5: Attach the IAM Role to EC2

The IAM Role was then attached to the existing EC2 instance.

Instance:

```plaintext
devops-ec2
```

Attached Role:

```plaintext
devops-role
```

Once attached, the EC2 instance automatically received temporary AWS credentials through the Instance Metadata Service (IMDS).

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/75725727-1cc5-43b6-b6e8-58bbfdec26f4.png align="center")

## Step 6: Upload a File to Amazon S3

After connecting to the EC2 instance through SSH, I tested access by uploading a sample file.

```plaintext
aws s3 cp test.txt s3://devops-s3-959313683568/
```

The upload completed successfully without configuring any AWS Access Keys on the instance.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/2810d104-c6c9-41a3-aa06-1665a951ae67.png align="center")

## Step 7: Verify Bucket Access

Finally, I verified the upload by listing the bucket contents.

```plaintext
aws s3 ls s3://devops-s3-959313683568/
```

Output:

```plaintext
2026-07-08 17:49:04        13 test.txt
```

This confirmed that:

*   The IAM Role was attached correctly.
    
*   The IAM Policy permissions were working.
    
*   The EC2 instance successfully authenticated using temporary credentials.
    
*   File upload and listing operations were successful.
    

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/c7b7e14d-b206-44cf-9242-59b1075d1819.png align="center")

# Conclusion

Day 37 focused on implementing secure access between Amazon EC2 and Amazon S3 using IAM Roles.

Instead of relying on long-term AWS credentials, I configured a private S3 bucket, created a least-privilege IAM policy, attached it to an EC2 IAM role, and successfully accessed the bucket using temporary credentials automatically provided by AWS.

This hands-on exercise demonstrated one of the most important AWS security best practices for granting service-to-service permissions in a scalable and secure way.
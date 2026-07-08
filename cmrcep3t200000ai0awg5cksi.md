---
title: "AWS Day 31: Configuring a Private RDS Instance for Application Development 
"
seoTitle: "AWS Day 31: Creating a Private Amazon RDS MySQL Instance |"
seoDescription: "Learn how to create a private Amazon RDS MySQL instance using the AWS Free Tier. This step-by-step guide covers RDS configuration, storage autoscali"
datePublished: 2026-07-08T18:23:33.290Z
cuid: cmrcep3t200000ai0awg5cksi
slug: aws-day-31-configuring-a-private-rds-instance-for-application-development
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/5958c358-03ca-4ef6-b432-9a5aa9b1d658.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/f6d29869-fb26-4dba-a2ad-f4a70c2b3d60.png
tags: aws, devops, rds, kodekloudengineer

---

## Introduction

During **Day 31** of the **KodeKloud 100 Days of Cloud Challenge**, I worked with **Amazon RDS (Relational Database Service)** by provisioning a **private MySQL database instance**.

In many production environments, databases should never be directly exposed to the internet. Instead, they are deployed inside private subnets where only trusted applications can access them. This approach improves security while allowing applications to communicate with the database within the VPC.

In this lab, the objective was to create a **private MySQL RDS instance** using the **AWS Free Tier**, enable **storage autoscaling**, and ensure the database reached the **Available** state before completing the task.

# Why Use Amazon RDS?

Managing databases manually can quickly become time-consuming. Tasks such as backups, software updates, monitoring, and scaling require continuous effort.

Amazon RDS simplifies database management by handling these operational tasks while allowing developers to focus on building applications.

Some key benefits of Amazon RDS include:

*   Automated backups
    
*   High availability options
    
*   Storage autoscaling
    
*   Easy monitoring with CloudWatch
    
*   Managed patching and maintenance
    
*   Improved security through private deployments
    

For this lab, **MySQL 8.4.x** was selected because it is one of the most widely used relational database engines.

## Step 1: Start Creating the RDS Database

I opened the **Amazon RDS Console** and clicked **Create Database**.

Instead of choosing the Easy Create option, I selected **Standard Create**, which provides full control over all database settings.

For the template, I selected **Free Tier** to keep the deployment within AWS free-tier eligible resources.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/a563083a-896f-43b9-bba6-cc279aee4e95.png align="center")

## Step 2: Configure the Database Engine

Next, I configured the database engine.

I selected:

| Setting | Value |
| --- | --- |
| Engine | MySQL |
| Version | 8.4.x |

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/02ab5e0a-9d7e-40a0-9ad6-237d0d27cfd3.png align="center")

## Step 3: Configure the DB Instance

In the database settings, I entered the required instance details.

| Setting | Value |
| --- | --- |
| DB Instance Identifier | datacenter-rds |
| Instance Class | db.t3.micro |

Since this was a development environment, the **db.t3.micro** instance type was sufficient and eligible for the AWS Free Tier.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/3ac000fe-8c7e-4a26-a6d8-3a81e5cef016.png align="center")

## Step 4: Enable Storage Autoscaling

To make the database storage more flexible, I enabled **Storage Autoscaling**.

I configured the maximum storage threshold to:

```plaintext
50 GB
```

This allows Amazon RDS to automatically increase storage if the allocated capacity becomes full, helping prevent storage-related issues without requiring manual intervention.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/b86e6360-7151-424f-a1f9-63542158845b.png align="center")

## Step 5: Review and Launch the Database

After verifying all the configuration settings, I reviewed the database configuration and clicked **Create Database**.

Provisioning an RDS instance usually takes several minutes because AWS needs to allocate compute resources, storage, networking, and configure the database engine.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/70c3a0cc-7fb8-407f-a484-08ca06c6d1c3.png align="center")

## Step 6: Verify the Database Status

Once the deployment completed, I returned to the **RDS Dashboard** and confirmed that the instance status had changed to:

```plaintext
Available
```

This confirmed that the database was successfully provisioned and ready for application use.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/afd7bab7-573d-4a47-99bc-8a0e371d1ec5.png align="center")

## What I Learned

This lab gave me practical experience with provisioning a managed relational database using Amazon RDS.

A few important takeaways from this exercise:

*   RDS removes the operational burden of managing database servers.
    
*   Deploying databases privately is a security best practice.
    
*   Storage Autoscaling helps prevent storage exhaustion without manual intervention.
    
*   Choosing the Free Tier template is useful for development and learning environments.
    

Although the setup was straightforward, it demonstrated how AWS simplifies database management while still allowing flexibility through advanced configuration options.

## Conclusion

Day 31 introduced another important AWS service by provisioning a **private Amazon RDS MySQL instance**.

Through this lab, I learned how to deploy a managed database using the **Free Tier**, configure **MySQL 8.4.x**, enable **Storage Autoscaling**, and verify that the instance was successfully created.

As I continue the **KodeKloud 100 Days of Cloud Challenge**, each lab is helping me build practical experience with core AWS services that are commonly used in real-world cloud environments.
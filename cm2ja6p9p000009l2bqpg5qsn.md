---
title: "DAY 08 : Decoding AWS Billing💡 A Guide to EC2, RDS, VPC, and Lambda Costs"
seoTitle: "AWS Billing Guide: EC2, RDS, VPC & Lambda"
seoDescription: "Decode AWS billing with an in-depth guide on EC2, RDS, VPC, and Lambda costs, including pricing models and influencing factors"
datePublished: Mon Oct 21 2024 17:19:00 GMT+0000 (Coordinated Universal Time)
cuid: cm2ja6p9p000009l2bqpg5qsn
slug: day-08-decoding-aws-billing-a-guide-to-ec2-rds-vpc-and-lambda-costs
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1729358085455/44515696-0770-4ecc-b21e-c0a3440232a6.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1729531105510/95062f81-1e21-470b-8cf1-2e036e390e53.png
tags: cloud, aws, cloud-computing, devops, vpc

---

### **EC2 Billing**

EC2 pricing is influenced by several factors:

* **Instance Size**: The number of vCPUs and the amount of memory.
    
* **Billing Duration**: Charges can be per second or per hour, depending on how long the instance runs.
    
* **Licensing Type**: The type of license associated with the instance.
    
* **Features Enabled**: Additional features that may incur extra costs.
    
* **Instance State**: Whether the machine is running or stopped. Note that a stopped instance still incurs a small cost.
    

### **Pricing Models**:

* **On-Demand**: Pay for compute capacity by the hour or second without long-term commitments.
    
* **Savings Plan**: Commit to a certain spend over 1-3 years for a discounted rate.
    
* **Spot Instances**: Use spare compute capacity at a discounted rate.
    
* **Reserved Instances**: Reserve capacity in advance for a discounted rate.
    
* **Dedicated Host**: A physical server dedicated exclusively to your account.
    
* **Dedicated Instance**: Instances run on dedicated hardware reserved for your account, but the server may vary.
    

### **RDS Billing**

RDS costs depend on:

* **RDS Flavor**: Options like Aurora or Aurora Serverless.
    
* **SQL Engine**: Choices include Oracle, MSSQL, MariaDB, MySQL, or PostgreSQL.
    
* **Memory Size**: The amount of memory allocated to the database.
    
* **Storage Disk Type**: General purpose or provisioned IOPS.
    
* **Additional Features**: Features like Multi-AZ or backup retention.
    

RDS also offers Reserved Instances but lacks spot, dedicated, or savings plans.

### **VPC Billing**

VPC costs include:

* **Base Charges**: Per VPC and their components.
    
* **Data Transfer Charges**: Only outbound data incurs charges, especially when moving between regions or using public IPs.
    
    * Includes data leaving one region for another.
        
    * Excludes data moving from an EC2 instance to an S3 bucket in the same region.
        
* **NAT Gateways**: Charges apply for their existence.
    
* **No Charges**: For subnets, Network ACLs (NACLs), Security Groups, or IP ranges.
    

### **Lambda Billing**

Lambda pricing is determined by several key factors:

* **Memory Size**: The amount of memory allocated to the function. Higher memory usage results in higher costs.
    
* **Duration**: The time your function runs, measured from the start of execution until it returns or otherwise terminates. Longer execution times increase costs.
    
* **Invocation Frequency**: The number of times your functions are invoked. More frequent invocations lead to higher charges.
    
* **Additional Features**: Features such as provisioned concurrency (hot provisioning) incur extra costs
    

Thankyou for reading !!!!
---
title: "AWS Day 35: Deploying and Managing Applications on AWS with Amazon RDS & EC2 | KodeKloud 100 Days of Cloud"
seoTitle: "AWS Day 35: Deploy a PHP Application with Amazon RDS and EC2"
seoDescription: "Learn how to deploy a PHP application using Amazon EC2 and Amazon RDS. This step-by-step AWS tutorial covers MySQL "
datePublished: 2026-07-15T19:21:15.533Z
cuid: cmrmgu9yf00000ajhfg6ifngu
slug: aws-day-35-deploying-and-managing-applications-on-aws-with-amazon-rds-ec2-kodekloud-100-days-of-cloud
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/81ad9230-47e7-4ac2-a127-ba229d6af0ac.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/20e4a61f-38dd-47a9-90af-3f1f80a590be.png
tags: aws, devops, rds, kodekloudengineer, anand-raval

---

## Introduction

On **Day 35** of the **KodeKloud 100 Days of Cloud Challenge**, I worked on a complete application deployment scenario involving **Amazon RDS** and **Amazon EC2**.

The objective wasn't just to create a database—it was to deploy a secure backend infrastructure where an application running on an EC2 instance could communicate with a private MySQL database hosted on Amazon RDS.

This lab closely resembles a real-world production workflow followed by DevOps engineers. It involved database provisioning, security group configuration, SSH key management, application deployment, and verifying end-to-end connectivity between the web server and the database.

## Why Use Amazon RDS with EC2?

Instead of installing MySQL directly on an EC2 instance, AWS recommends using **Amazon RDS**, a fully managed database service.

Some of the key benefits include:

*   Automated backups
    
*   High availability options
    
*   Automatic software patching
    
*   Storage scaling
    
*   Simplified database management
    
*   Better security through VPC integration
    

Keeping the database private while allowing only application servers to access it is also a common security best practice.

## Lab Objective

The objective of this lab was to:

*   Create a private RDS instance named **datacenter-rds**
    
*   Use **MySQL 8.4.5**
    
*   Deploy a **db.t3.micro** instance
    
*   Configure storage using **General Purpose SSD (gp2)** with **5 GiB**
    
*   Create a database named **datacenter\_db**
    
*   Allow the existing EC2 instance to access the database
    
*   Configure password-less SSH authentication
    
*   Deploy a PHP application on EC2
    
*   Verify database connectivity through the web browser
    

## Step 1: Create the Amazon RDS Instance

I started by navigating to the **Amazon RDS Console** and selected **Create Database → Full Configuration**.

The database was configured with the following settings:

| Setting | Value |
| --- | --- |
| Database Name | datacenter-rds |
| Engine | MySQL |
| Version | 8.4.5 |
| Instance Type | db.t3.micro |
| Storage Type | General Purpose SSD (gp2) |
| Storage Size | 5 GiB |
| Master Username | datacenter\_admin |

After entering the required credentials and database name, I left the remaining settings at their default values and launched the database.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/de46e407-636a-41b5-9a8e-71961c51c730.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/85aaa730-cd12-4afe-811e-b28d1e5b98c4.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/d75f100b-4db6-4bb4-b118-891958aa3c85.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/996b857e-b755-4638-b50e-0d38e2288310.png align="center")

## Step 2: Wait Until the Database Becomes Available

Provisioning an RDS instance usually takes several minutes.

Before moving forward, I waited until the database status changed to:

```plaintext
Available
```

Only after the instance became available could it accept client connections.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/e497c76a-e1cc-4668-9a08-6c48f0a22a6b.png align="center")

## Step 3: Configure Security Groups

Next, I updated the EC2 security group to allow the required traffic.

The following inbound rules were configured:

| Port | Purpose |
| --- | --- |
| 3306 | MySQL Database Access |
| 80 | HTTP Web Access |

This allowed the application server to communicate with the RDS instance while also making the web application accessible through a browser.

## Step 4: Generate an SSH Key Pair

To enable password-less SSH access, I generated a new SSH key pair on the **aws-client** host.

```plaintext
cd /root/.ssh

ssh-keygen
```

The command created:

```plaintext
id_rsa
id_rsa.pub
```

These files contain the private and public SSH keys used for secure authentication.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/7ffc9748-1b1b-4e8d-a8b5-8257271fcb21.png align="center")

## Step 5: Configure Password-less SSH Access

After generating the key pair, I copied the public key into the **authorized\_keys** file of the EC2 instance.

This allowed the aws-client machine to connect to the server without entering a password every time, making future deployments much easier.

This is a common practice in DevOps automation and remote server management.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/9d8b2708-3981-4738-b8a8-1e860648f5d9.png align="center")

## Step 6: Deploy the PHP Application

A PHP file named **index.php** was already available on the aws-client machine.

I copied it to the Apache web root directory on the EC2 instance using SCP.

```plaintext
scp index.php root@<EC2_PUBLIC_IP>:/var/www/html/
```

The file was successfully transferred to the web server.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/07489781-fd25-4a3b-be2c-a5bde05a24d9.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/6272954b-4f06-4e73-827e-49885c6f7b89.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/468e7184-b985-4a8f-9c6e-4c27c7998698.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/40f2f638-ab31-46c4-82d0-de96b2ea2864.png align="center")

## Step 7: Update the Database Configuration

Inside **index.php**, I updated the database connection details.

The configuration included:

*   Database Name
    
*   Database Username
    
*   Database Password
    
*   RDS Endpoint
    

After saving the changes, the PHP application was ready to communicate with Amazon RDS.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/ec6944ea-459c-4e03-b881-e74c3c530a9a.png align="center")

## Step 8: Verify the Application

Finally, I opened the EC2 instance's public IP address in a web browser.

The application displayed:

```plaintext
Connected successfully
```

This confirmed that:

*   The EC2 instance could reach the private RDS instance.  
    
*   The security group configuration was correct.  
    
*   The database credentials were valid.  
    
*   The PHP application was successfully communicating with MySQL.
    

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/9b621a55-5527-4603-b46a-02d005cf3bb3.png align="center")

## Conclusion

Day 35 was one of the most practical labs in the challenge, combining database provisioning, networking, Linux administration, and application deployment into a single workflow.

By creating a private Amazon RDS instance, configuring secure connectivity, deploying a PHP application on EC2, and successfully validating the database connection, I gained a deeper understanding of how application and database tiers interact in AWS.

This hands-on exercise closely mirrors real-world DevOps responsibilities and reinforced the importance of secure architecture, proper networking, and automated server management.
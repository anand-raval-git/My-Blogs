---
title: "AWS Day 36: Load Balancing EC2 Instances with Application Load Balancer (ALB) | KodeKloud 100 Days of Cloud"
seoTitle: "AWS Day 36: Create an Application Load BalanceEC2 and Nginx "
seoDescription: "Learn how to deploy an Nginx web server on Amazon EC2 and configure an Application Load Balancer (ALB) with Target Groups, Securi"
datePublished: 2026-07-18T18:35:54.388Z
cuid: cmrqpjiar00000aki8105fed9
slug: aws-day-36-load-balancing-ec2-instances-with-application-load-balancer-alb-kodekloud-100-days-of-cloud
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/1fe2b432-669f-47d9-8602-da26af4113b2.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/88468b9f-e7d6-4e85-9779-73083e4de0b0.png
tags: ec2, aws, elb, kodekloudengineer

---

On **Day 36** of the **KodeKloud 100 Days of Cloud Challenge**, I built a complete **Application Load Balancer (ALB)** architecture on AWS.

Instead of exposing an EC2 instance directly to the internet, an **Application Load Balancer** sits in front of it and intelligently distributes incoming HTTP requests. Although this lab uses a single EC2 instance, the same architecture easily scales to multiple instances for high availability and fault tolerance.

This exercise covered creating a custom security group, launching an Ubuntu EC2 instance with User Data, installing Nginx automatically, configuring an Application Load Balancer, creating a Target Group, and validating traffic flow through the ALB DNS.

## Lab Objective

The goal of this lab was to:

*   Create a Security Group named **devops-sg**
    
*   Allow HTTP traffic from the ALB
    
*   Launch an Ubuntu EC2 instance named **devops-ec2**
    
*   Install Nginx automatically using User Data
    
*   Create an Application Load Balancer named **devops-alb**
    
*   Create a Target Group named **devops-tg**
    
*   Register the EC2 instance as a target
    
*   Route HTTP traffic from the ALB to the EC2 instance
    
*   Verify the Nginx page using the ALB DNS
    

## Architecture Overview

The final architecture looks like this:

```plaintext
                Internet
                     │
                     ▼
        Application Load Balancer
             (HTTP Port 80)
                     │
                     ▼
           Target Group (devops-tg)
                     │
                     ▼
         Ubuntu EC2 Instance (Nginx)
```

The Application Load Balancer receives incoming HTTP requests and forwards them to the registered EC2 instance through the Target Group.

## Step 1: Create the Security Group

The first step was creating a custom Security Group named:

```plaintext
devops-sg
```

Inbound Rule:

| Type | Port | Source |
| --- | --- | --- |
| Custom TCP | 80 | Default Security Group |

This configuration allows HTTP requests originating from the ALB to reach the EC2 instance securely.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/69a77534-695f-44fa-862c-81736c2b8aee.png align="center")

## Step 2: Launch the EC2 Instance

Next, I launched a new Ubuntu EC2 instance.

Configuration:

| Setting | Value |
| --- | --- |
| Instance Name | devops-ec2 |
| AMI | Ubuntu |
| Instance Type | t3.micro |
| Security Group | devops-sg |

Instead of installing software manually, I used **User Data** to automate the server configuration during instance launch.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/e7cdc3ce-c85e-4f9f-806f-242d2c745a48.png align="center")

## Step 3: Attach the Security Group

While launching the EC2 instance, I attached the previously created security group:

```plaintext
devops-sg
```

This ensured that only the Application Load Balancer could communicate with the web server over HTTP.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/ef4aca63-9901-4815-990d-569015fcdca7.png align="center")

## Step 4: Configure User Data

The following script automatically installs and starts the Nginx web server.

```plaintext
#!/bin/bash

sudo apt update
sudo apt install nginx -y
sudo systemctl start nginx
```

When the EC2 instance booted for the first time, AWS automatically executed this script.

As a result:

*   Nginx was installed  
    
*   The service started automatically  
    
*   The web server became ready without manual intervention
    

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/fa31fc48-e8db-4622-9384-120c9433fe15.png align="center")

## Step 5: Create the Application Load Balancer

After the EC2 instance was running, I created an **Internet-facing Application Load Balancer**.

Configuration:

| Setting | Value |
| --- | --- |
| Name | devops-alb |
| Scheme | Internet-facing |
| IP Type | IPv4 |
| Listener | HTTP :80 |
| Security Group | Default Security Group |

The ALB acts as the public entry point for client requests.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/22c0c9b9-5f25-4b50-a0f4-9f5b2793ae66.png align="center")

## Step 6: Configure the ALB Security Group

The default Security Group attached to the ALB was configured to allow inbound HTTP traffic.

| Type | Port |
| --- | --- |
| HTTP | 80 |

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/3fa0899c-aeea-40d4-b71a-bad69b72aa69.png align="center")

## Step 7: Create the Target Group

The next step was creating a Target Group.

Configuration:

| Setting | Value |
| --- | --- |
| Name | devops-tg |
| Target Type | Instances |
| Protocol | HTTP |
| Port | 80 |

The Target Group acts as the bridge between the ALB and backend EC2 instances.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/0361f15a-cdbf-406a-bd19-dc4e0beaadb5.png align="center")

## Step 8: Register the EC2 Instance

After creating the Target Group, I registered the EC2 instance.

Registered Target:

```plaintext
devops-ec2
```

Target Port:

```plaintext
80
```

Once registered, AWS automatically began performing health checks on the instance.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/37b1284f-39c5-43e3-bb11-55286fbbb692.png align="center")

## Step 9: Verify the Application

Finally, I opened the **Application Load Balancer DNS name** in the browser.

The default Nginx welcome page appeared successfully.

```plaintext
Welcome to nginx!
```

This confirmed that:

*   The ALB was reachable
    
*   Security Groups were configured correctly
    
*   The Target Group was healthy
    
*   The EC2 instance was serving HTTP traffic
    
*   Nginx was installed successfully using User Data
    

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/01643b66-c4eb-4b68-8363-b65aa5dbb006.png align="center")

## Conclusion

Day 36 focused on building a scalable and production-ready web architecture using **Amazon EC2** and the **Application Load Balancer (ALB)**.

By creating a dedicated security group, launching an Ubuntu instance with automated Nginx installation, configuring an Application Load Balancer, registering the EC2 instance in a Target Group, and validating traffic through the ALB DNS, I gained practical experience with one of the most commonly used architectures in AWS.

This hands-on exercise demonstrated how AWS Elastic Load Balancing improves availability, simplifies traffic management, and provides the foundation for scaling web applications across multiple EC2 instances.
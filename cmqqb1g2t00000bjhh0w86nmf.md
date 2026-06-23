---
title: "Day 24: Setting Up an Application Load Balancer for an EC2 Instance"
seoTitle: "AWS Day 24: Application Load Balancer Setup for EC2"
seoDescription: "Learn how to set up an AWS Application Load Balancer (ALB) for an EC2 instance, create a Target Group, configure Security Groups, and route HT in AWS."
datePublished: 2026-06-23T07:10:14.735Z
cuid: cmqqb1g2t00000bjhh0w86nmf
slug: day-24-setting-up-an-application-load-balancer-for-an-ec2-instance
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/0113a9ad-45d4-4388-a7df-8b2aa9d79f96.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/69a1c010-53dd-4781-b19b-fde50e66be6a.png
tags: ec2, aws, load-balancing, kodekloud, anand-raval

---

## Introduction

During Day 24 of the KodeKloud 100 Days of Cloud Challenge, I worked on setting up an AWS Application Load Balancer (ALB) for an EC2 instance running an Nginx web server.

Application Load Balancers are commonly used in AWS to distribute incoming traffic across backend resources. Instead of exposing EC2 instances directly to users, organizations place an ALB in front of their applications to improve availability, scalability, and traffic management.

In this lab, the goal was to create an Application Load Balancer, configure a Target Group, and route HTTP traffic to an EC2 instance.

## AWS Application Load Balancer Setup Requirements

The task requirements were:

*   Create an Application Load Balancer named **devops-alb**
    
*   Create a Target Group named **devops-tg**
    
*   Create a Security Group named **devops-sg**
    
*   Allow HTTP traffic on port 80
    
*   Attach the Security Group to the ALB
    
*   Route traffic from the ALB to the **devops-ec2** instance
    
*   Verify that the EC2 instance receives traffic successfully
    

### Step 1: Navigate to Load Balancers

I opened the EC2 console and selected **Load Balancers** from the left navigation menu. From there, I clicked **Create Load Balancer** to begin the configuration process.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/c8d28652-b9ae-4624-8f7b-c10043ecda77.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/4e2b699e-bfad-48ad-a5c4-e0925d1e67db.png align="center")

### Step 2: Select Application Load Balancer

AWS provides multiple load balancer options. For this task, I selected **Application Load Balancer (ALB)** since it is designed to handle HTTP and HTTPS traffic efficiently.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/9b1d8415-3015-43ed-9a75-cf878c1f57e4.png align="center")

### Step 3: Configure the Load Balancer

Next, I configured the basic settings for the load balancer and provided the required name:

```plaintext
devops-alb
```

I kept the scheme as **Internet-facing** and configured the listener to use **HTTP on port 80**.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/8b72f8aa-034e-4a16-be36-fb4212bcbad2.png align="center")

## Step 4: Create a Security Group for the Application Load Balancer

The first step was creating a Security Group named **devops-sg**.

To allow public access to the application, I configured an inbound rule:

| Type | Port | Source |
| --- | --- | --- |
| HTTP | 80 | 0.0.0.0/0 |

This Security Group was later attached to the Application Load Balancer.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/50dbc5e9-5ffc-40be-afbe-94b5421037f8.png align="center")

## Step 5: Create the Target Group

Next, I created a Target Group named **devops-tg**.

Configuration used:

*   Target Type: Instance
    
*   Protocol: HTTP
    
*   Port: 80
    

After creating the Target Group, I registered the **devops-ec2** instance as a target.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/c1f546ae-8be3-44dd-85e1-750754174f84.png align="center")

### Step 7: Verify the Load Balancer

Once all configurations were completed, AWS successfully created the Application Load Balancer.

After the target passed the health checks, the load balancer became active and ready to route traffic to the EC2 instance.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/dc0010ff-5d58-49d9-8b62-cdc356e8e758.png align="center")

## Step 8: Test the Application Load Balancer

Finally, I copied the DNS name of the Application Load Balancer and opened it in a browser.

The Nginx sample page loaded successfully, confirming that traffic was being routed correctly from:

User → Application Load Balancer → Target Group → EC2 Instance

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/6a6caf5e-60d7-4ff7-b4a9-7bb7d811d146.png align="center")

## Conclusion

Day 24 provided hands-on experience with setting up an AWS Application Load Balancer for an EC2 instance.

Although the application was a simple Nginx web server, the architecture followed the same pattern commonly used in production environments. Understanding how ALBs, Target Groups, and Security Groups work together is an important skill for anyone working with AWS and cloud infrastructure.
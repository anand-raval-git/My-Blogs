---
title: "AWS Day 44: Implementing Auto Scaling for High Availability in AWS"
seoTitle: "AWS Auto Scaling and ALB: High Availability Guide"
seoDescription: "Learn how to configure EC2 Auto Scaling, an Application Load Balancer, Nginx, health checks, and CPU-based scaling for high availability."
datePublished: 2026-08-20T18:01:44.166Z
cuid: cmt1tuocn00000akq2ebo4crv
slug: aws-day-44-implementing-auto-scaling-for-high-availability-in-aws
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/9c49aabc-0263-4874-8180-d7f0205d3b5f.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/99a6dc12-8a89-40b4-a47c-55f321fc8d15.png
tags: aws, auto-scaling, kodekloud, kodekloudengineer, anand-raval

---

As part of my **KodeKloud 100 Days of Cloud** journey, Day 44 focused on building a highly available web application using **Amazon EC2, Auto Scaling Groups, and an Application Load Balancer (ALB)**.

The goal of this lab was to create an EC2-based web application that could automatically scale when traffic increased and continue serving requests through a load balancer.

For the application, I used **Nginx** as the web server. The EC2 instances were launched automatically using a launch template, while the Auto Scaling Group maintained the required number of instances.

## Step 1: Create the EC2 Launch Template

I started by opening:

**AWS Console → EC2 → Instances → Launch an instance**

Instead of launching a standalone EC2 instance, the requirement was to create a reusable **launch template**.

The launch template was named:

```plaintext
datacenter-launch-template
```

A launch template allows us to define the configuration that should be used whenever the Auto Scaling Group launches a new EC2 instance.

This is useful because every instance created by the ASG can use the same:

*   AMI
    
*   Instance type
    
*   Security group
    
*   User Data
    
*   Storage configuration
    
*   Other launch parameters
    

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/12b97625-af9c-4475-8e6e-e561e153b06c.png align="center")

## Step 2: Select Amazon Linux 2

The task specifically required **Amazon Linux 2**.

I selected an Amazon Linux 2 AMI from the available AMI catalog.

The AMI provides the operating system environment that will be installed on every EC2 instance launched through the template.

For this task, Amazon Linux 2 was selected because the provided User Data uses `amazon-linux-extras` to install Nginx.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/25fd4c36-fd67-40a9-90f7-a6ceef603eb3.png align="center")

## Step 3: Select the EC2 Instance Type

The required instance type was:

```plaintext
t2.micro
```

The `t2.micro` instance provides:

```plaintext
1 vCPU
1 GiB memory
```

It is appropriate for this lab because the workload is only a simple Nginx web server.

For production workloads, the instance type should be selected based on actual CPU, memory, network, and application requirements rather than simply using a small instance type.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/15ccfcea-410c-421c-b9d3-a3bd1066143a.png align="center")

## Step 4: Configure the Security Group

The EC2 instances need to receive HTTP traffic from the Application Load Balancer.

I configured a security group with an inbound rule allowing:

```plaintext
Protocol : TCP
Port     : 80
Source   : HTTP traffic
```

The important requirement is that the web server must be reachable on port `80`.

In a production environment, the preferred design would be more restrictive:

```plaintext
Internet
   |
   v
ALB Security Group
   |
   v
EC2 Security Group
```

The EC2 security group would allow port 80 only from the ALB security group instead of allowing HTTP from the entire internet.

For this lab, the required HTTP access was configured so that the ALB could successfully reach the Nginx instances.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/606725e3-3673-47d8-9267-607cf7c684ca.png align="center")

## Step 5: Configure User Data

One of the most useful parts of this lab was configuring **EC2 User Data**.

The objective was to automatically install and start Nginx whenever a new EC2 instance was launched.

I used:

```plaintext
#!/bin/bash

amazon-linux-extras install nginx1 -y
systemctl start nginx
systemctl enable nginx
```

This script performs three main operations.

### Install Nginx

```plaintext
amazon-linux-extras install nginx1 -y
```

This installs Nginx on the Amazon Linux 2 instance.

### Start Nginx

```plaintext
systemctl start nginx
```

This starts the Nginx service immediately.

### Enable Nginx at boot

```plaintext
systemctl enable nginx
```

This ensures that Nginx automatically starts after the instance reboots.

This approach means that every new EC2 instance launched by the Auto Scaling Group can automatically become a web server without manually connecting to the instance.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/a3f17aaf-5f47-47b6-b27b-f874308be3f2.png align="center")

## Step 6: Create the Auto Scaling Group

After creating the launch template, I moved to:

**EC2 → Auto Scaling Groups → Create Auto Scaling group**

I created the Auto Scaling Group with the name:

```plaintext
datacenter-asg
```

The ASG uses:

```plaintext
datacenter-launch-template
```

as its instance configuration.

This means that any EC2 instance launched by the ASG uses the configuration defined in the launch template.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/fca33a33-0a31-4f35-865c-47c675e53f2d.png align="center")

## Step 7: Configure Group Capacity

The required capacity settings were:

```plaintext
Desired capacity : 1
Minimum capacity : 1
Maximum capacity : 2
```

So the initial configuration was:

```plaintext
datacenter-asg
       |
       v
Desired = 1
Min     = 1
Max     = 2
```

The desired capacity of `1` means the ASG initially launches one EC2 instance.

The minimum capacity of `1` ensures that the ASG does not scale down to zero instances.

The maximum capacity of `2` limits the number of instances that can be running as part of this lab.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/ebdff7c1-9a8d-4c14-8b34-8a9f49461f1b.png align="center")

## Step 8: Configure CPU-Based Scaling

The task required the Auto Scaling Group to scale based on **CPU utilization**.

I selected:

**Target tracking scaling policy**

For the metric, I selected:

```plaintext
Average CPU utilization
```

The target value was:

```plaintext
50%
```

The scaling configuration was therefore:

```plaintext
Metric       : Average CPU utilization
Target       : 50%
Minimum      : 1
Desired      : 1
Maximum      : 2
```

The idea behind target tracking is simple.

If the average CPU utilization moves significantly above the target, the Auto Scaling Group can increase capacity.

If utilization falls and additional capacity is no longer required, the ASG can reduce capacity while respecting the minimum size.

This makes target tracking useful for workloads where CPU utilization is a reasonable indicator of application demand.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/3fc84917-fd3d-4c0d-9663-9a841e46ae9c.png align="center")

## Step 9: Verify Nginx

Once the instance was running and the User Data script had completed, Nginx was available on port `80`.

The browser test confirmed that the Nginx default page was being served.

The page displayed:

```plaintext
Welcome to nginx!
```

This confirmed that:

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/73056760-1c2c-4c39-8be6-fd20446cb164.png align="center")
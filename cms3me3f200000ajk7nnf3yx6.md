---
title: "AWS Day 40: Troubleshooting Internet Accessibility for an EC2-Hosted Application"
seoTitle: "Troubleshooting Internet Accessibility for an EC2-Hosted App"
seoDescription: "Troubleshot an EC2 internet connectivity issue by verifying the VPC configuration, attaching an Internet Gateway."
datePublished: 2026-07-27T19:28:43.245Z
cuid: cms3me3f200000ajk7nnf3yx6
slug: aws-day-40-troubleshooting-internet-accessibility-for-an-ec2-hosted-application
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/7f4c89c4-1097-4d68-af97-67f11910a761.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/c4826fd0-5a4a-4eb3-a2b5-e28e3972bf42.png
tags: ec2, aws, internet-gateway, kodekloud, anand-raval

---

One of the most common networking issues in AWS occurs when an EC2 instance is correctly configured but remains inaccessible from the internet. Even if the security group, network ACLs, and application are working properly, a missing or detached Internet Gateway can prevent inbound and outbound internet traffic.

In this hands-on lab, the EC2 instance was running inside a public VPC named **nautilus-vpc** with Nginx already configured to listen on port **80**. After verifying that the instance and security group were configured correctly, the root cause was identified as a detached Internet Gateway. Reattaching the Internet Gateway restored internet connectivity, allowing the application to be accessed successfully.

## Step 1 – Verify the VPC Configuration

The first step was verifying the networking components associated with the VPC.

The following were checked:

*   Public VPC
    
*   Route Table
    
*   Internet Gateway
    
*   Security Group
    
*   EC2 Public IP
    
*   Network ACL
    

The Security Group and EC2 configuration were already correct.

## Step 2 – Identify the Root Cause

During verification, the Internet Gateway named:

```plaintext
xfusion-ig
```

was found in the **Detached** state.

Without an attached Internet Gateway:

*   Internet traffic cannot enter the VPC.
    
*   Public IP addresses become unreachable.
    
*   Applications remain inaccessible from external users.
    

This was the root cause of the issue.

## Step 3 – Attach the Internet Gateway

The detached Internet Gateway was attached to the **nautilus-vpc**.

AWS Console Steps:

1.  Open **VPC**
    
2.  Navigate to **Internet Gateways**
    
3.  Select **xfusion-ig**
    
4.  Choose **Actions → Attach to VPC**
    
5.  Select **nautilus-vpc**
    
6.  Save the configuration
    

Once attached, the VPC regained internet connectivity.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/b02f5b1c-c1c4-4fe7-b09e-8c0b60c39252.png align="center")

## Step 4 – Verify the Application

After attaching the Internet Gateway, the EC2 instance became publicly reachable.

Opening the EC2 Public IP in a browser displayed the default **Nginx Welcome Page**, confirming that the application was successfully accessible over HTTP on port **80**.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/b7f30b42-982a-4c58-875e-14c5c00def04.png align="center")

## Conclusion

Troubleshooting AWS networking requires checking each component involved in the traffic flow rather than focusing only on the EC2 instance. In this lab, the EC2 instance and Nginx server were functioning correctly, but the VPC lacked an attached Internet Gateway. Reattaching the Internet Gateway restored the network path, making the application publicly accessible.

This exercise reinforces the importance of understanding how VPC components such as Internet Gateways, route tables, subnets, and security groups work together to enable internet connectivity in AWS.
---
title: "DAY 11 : 🚀 Navigating AWS Networking: Subnets, Gateways, and More"
seoTitle: "AWS Networking: Subnets and Gateways Basics"
seoDescription: "Explore AWS networking essentials, including VPCs, subnets, gateways, and firewalls, to optimize security and connectivity in the cloud"
datePublished: 2024-10-26T18:07:12.976Z
cuid: cm2qh3y34000109lc1tmq8pdj
slug: day-11-navigating-aws-networking-subnets-gateways-and-more
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1729965970123/84eb37e8-f178-4c5a-9147-2a257dd6c79a.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1729966007841/fe5ec266-52b9-4a87-a4f8-edb20ba43b8c.png
tags: cloud, aws, cloud-computing, devops, aws-cloud-practitioner

---

1. **VPC (Virtual Private Cloud):**
    
    * A VPC is a secure, isolated network segment hosted within AWS.
        
    * It isolates computing resources within the cloud and acts as a network boundary.
        
    * Provides full control over networking, including subnetting, routing, firewalls, and gateways.
        
    * Specific to a single region.
        
    * Utilizes a CIDR block, which is a range of IP addresses that resources in the VPC can use.
        
2. **Subnets:**
    
    * Subnets are groups of IP addresses within your VPC.
        
    * They reside within a single availability zone.
        
    * The IP address range must be within the parent VPC's CIDR block.
        
    * Subnets can be public or private, determining external access to resources.
        
3. **Gateways:**
    
    * An Internet gateway allows subnets in a VPC to communicate with the internet.
        
    * NAT gateways provide internet access for resources, with connections initiated from within the VPC.
        
    * Virtual private gateways enable secure access to private resources over the internet.
        
    * Direct Connect (DX) offers a direct connection to an AWS region, providing low latency and high speeds.
        
4. **Default Networking:**
    
    * Each region has a Default VPC with default subnets, security groups, and Network ACLs (NACLs).
        
    * The CIDR block for the Default VPC is 172.31.0.0/16.
        
    * One default subnet exists in each Availability Zone (AZ).
        
    * Default VPCs and subnets have outbound internet access by default.
        
    * Security groups allow outbound traffic, and NACLs are open in both directions.
        
    * Default subnets have access to an Internet Gateway for connectivity.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729706185795/925732a6-7ca0-4904-8363-c1385e11e0d8.png align="left")
        
5. **Firewalls:**
    
    * Stateless firewalls require explicit permission for inbound and outbound traffic.
        
    * Stateful firewalls track requests and automatically allow responses.
        
    * Network ACLs (NACLs) filter traffic entering and leaving a subnet and are stateless.
        
    * Security groups act as firewalls for individual resources like EC2 instances and are stateful.
        

Thankyou for reading !!!!!!
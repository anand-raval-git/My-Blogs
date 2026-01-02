---
title: "AWS Task Day 02 :-  Create Security Group in aws"
seoTitle: "Create AWS Security Group: Step-by-Step Guide"
seoDescription: "Learn to create an AWS security group for HTTP and SSH access with our step-by-step guide. Ideal for DevOps cloud migrations"
datePublished: Fri Jan 02 2026 08:22:41 GMT+0000 (Coordinated Universal Time)
cuid: cmjwlw3k3000202l5hp25dolu
slug: aws-task-day-02-create-security-group-in-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1767342074278/fb8269fa-dfe3-4041-abe1-47b2a436285f.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1767342144589/9588f5a4-d71d-4f88-bd0d-d1b89468ec9f.png
tags: cloud-computing, devops, 100daysofcloud, kodekloudengineer, anand-raval

---

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition. To achieve this, they have segmented large tasks into smaller, more manageable units. This granular approach enables the team to execute the migration in gradual phases, ensuring smoother implementation and minimizing disruption to ongoing operations. By breaking down the migration into smaller tasks, the Nautilus DevOps team can systematically progress through each stage, allowing for better control, risk mitigation, and optimization of resources throughout the migration process.

For this task, create a security group under default VPC with the following requirements:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1765876908653/3db03ce6-d6ed-41bf-a99c-2c17a9dc2087.png align="center")

* Name of the security group is `datacenter-sg`.
    
* The description must be `Security group for Nautilus App Servers`
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1765877015699/6c74b57f-1804-482b-bde0-0c797f7eda53.png align="center")

* Add the inbound rule of type `HTTP`, with port range of `80`. Enter the source CIDR range of `0.0.0.0/0`.
    
* Add another inbound rule of type `SSH`, with port range of `22`. Enter the source CIDR range of `0.0.0.0/0`.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1765877402370/d9bc2711-5305-40eb-89e7-9585793f16c3.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1765877458658/a2d15fe8-7073-419a-90cc-7cfdf71b47d4.png align="center")

Thankyou !!!!!!!!!!!!!!!!
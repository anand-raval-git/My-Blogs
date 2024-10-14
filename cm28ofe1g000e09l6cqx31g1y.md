---
title: "Day 03 : 🌩️ Exploring AWS Core Services and Cloud Benefits"
seoTitle: "AWS Core Services and Cloud Benefits Exploration"
seoDescription: "Learn AWS core services, cloud benefits, pricing models, and design principles for scalable, resilient cloud-native applications"
datePublished: Mon Oct 14 2024 07:12:13 GMT+0000 (Coordinated Universal Time)
cuid: cm28ofe1g000e09l6cqx31g1y
slug: day-03-exploring-aws-core-services-and-cloud-benefits
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1728889865069/1f3fd806-b0c8-4db7-a692-26f2dc240a8b.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1728889912534/028508bd-fa28-4407-af28-ee81f67e8e5d.png
tags: cloud, aws, cloud-computing, cloud-native, aws-cloud-practitioner

---

### AWS Core Service Categories

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1728889331060/2fa7284c-c918-4ead-8efa-898443d22661.jpeg align="center")

AWS services can be broken down into six major categories.

<table><tbody><tr><td colspan="1" rowspan="1"><p>CATEGORY</p></td><td colspan="1" rowspan="1"><p>DESCRIPTION</p></td></tr><tr><td colspan="1" rowspan="1"><p>Networking and Content Delivery</p></td><td colspan="1" rowspan="1"><p>These are services for managing networking in the cloud.</p></td></tr><tr><td colspan="1" rowspan="1"><p>Databases</p></td><td colspan="1" rowspan="1"><p>These are services that manage databases.</p></td></tr><tr><td colspan="1" rowspan="1"><p>Security, Identity and Compliance</p></td><td colspan="1" rowspan="1"><p>These handle the security of your AWS infrastructure.</p></td></tr><tr><td colspan="1" rowspan="1"><p>Management and Governance</p></td><td colspan="1" rowspan="1"><p>These ensure that AWS infrastructure is following best practices and meeting regulatory requirements</p></td></tr><tr><td colspan="1" rowspan="1"><p>Storage</p></td><td colspan="1" rowspan="1"><p>These are services used to store data.</p></td></tr></tbody></table>

### Interacting With AWS

| WEB GUI | Command Line Interface | Programmatically |
| --- | --- | --- |
| Console | AWS CLI | AWS SDK |
| Beginners | Engineer | Developers |

### Benefits of the Cloud

  
● CAPEX can be converted to OPEX  
a) Upfront expenditures are referred to as capital expenditures (CAPEX).  
b) Day-to-day expenses are referred to as operational expenses (OPEX).  
c) In the cloud, you trade upfront expenses for variable day-to-day expenses;  
therefore, you pay for only what you use and give back what you don’t  
need.  
● In the cloud, you do not have to predict your future capacity.  
● Allows faster deployment of applications  
\- Companies don’t have to order physical equipment and have it installed for  
scaling up or upgrading according to requirements.  
● High availability and low latency  
\- With AWS, you can access their entire global infrastructure and deploy  
applications on any of their sites with just a click of a button.

### Cloud Economics

AWS has five different pricing models, so you can select the one that saves you on cost for your specific workload.

| Free Tier | On-Demand | Reserved Volume | Discounts Price | Drops |
| --- | --- | --- | --- | --- |
| Over 100 services available for free | Pay for what you use or the size you request | If you know you will be using a service for a long time, you can reserve it ahead of time (for 1-3 years) to save on cos | Like most things in the world, when you buy more, the price per unit goes down | AWS drops prices on services fairly regularly |
| 12 months of free service |  |  |  | There have been 129 price drops from 2006 to early 2023 |
| Some services are always free |  |  |  |  |

### Cloud Native Design principles

| Design for Failure | \- No single point of failure – no single component or location going down should take down your entire application - Add redundancy as much as possible |
| --- | --- |
| Decouple Components | \- AWS offers Simple Queue Service (SQS) that allows you to move data between different components When components need to communicate with one another, they’ll send messages through the queue - Allows you to have individual components go down without loss of data |
| Implement Elasticity | \- Make sure your application and all its components can scale up and down as load varies |
| Think Parallel | \- Have multiple instances running concurrently to finish tasks as quickly as possible |

Thankyou for reading !!!!!
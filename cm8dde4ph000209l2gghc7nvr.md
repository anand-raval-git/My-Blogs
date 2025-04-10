---
title: "Day 04: Azure Basics, Purchasing & Licensing Options, Account, Subscription, Support and Billing"
seoTitle: "Azure Essentials: Licensing, Billing & Support"
seoDescription: "Learn Azure basics: purchasing, licensing, support, billing, subscriptions, and its impact on Fortune 500 companies"
datePublished: Mon Mar 17 2025 18:00:23 GMT+0000 (Coordinated Universal Time)
cuid: cm8dde4ph000209l2gghc7nvr
slug: day-04-azure-basics-purchasing-and-licensing-options-account-subscription-support-and-billing
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1742234356051/714b3551-db1a-441f-a490-964df3102efb.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1744280215702/32b577cf-22f2-4f5d-85d5-10d54775b2f9.png
tags: cloud, azure, cloud-computing, devops, azure-devops

---

# Azure Basics

* Azure is Microsoft's private & public cloud computing platform
    
* Provides developers & IT admins tools to provide, build, manage, and deploy applications.
    
    * on a massive global network
        
    * freedom to choose tools and frameworks
        
* More than 90% of Fortune 500 companies run on the Microsoft Cloud
    

## Azure services

* More than 100 services..
    
* **Compute services** such as VMs and containers that can run your applications
    
* **Database services** that provide both relational and NoSQL choices
    
* **Identity services** that help you authenticate and protect your users
    
* **Networking services** that connect your datacenter to the cloud, provide high availability or host your DNS domain
    
* **Storage solutions** that can accommodate massive amounts of both structured and unstructured data
    
* **AI and machine-learning** services can analyze data, text, images, comprehend speech, and make predictions using data
    

## How Azure works

* It uses virtualization
    
    * Uses an abstraction layer called **hypervisor**.
        
        * Separates tight coupling between hardware (CPU, RAM, GPU..) and its operating system
            
        * Emulates a real computer in a **virtual machine**
            
            * Can run multiple virtual machines in same time
                
            * Optimizes capacity of abstracted hardware
                
            * Can run any OS such as Windows, Linux & macOS
                
* Azure repeats virtualization in massive scale
    
    * Each data center has many racks filled with servers
        
    * Each server includes a hypervisor to run multiple virtual machines.
        
    * A network switch provides connectivity to all those servers
        
    * One server in each rack runs a special software called **fabric controller**
        
        * Each fabric controller is connected to another software called as **orchestrator**
            
            * Orchastrator manages everything in Azure, including responding user requests
                
                * Users requests using **Azure API**
                    
                    * Azure API can be reached in many ways including Azure Portal
                        
                * Orchestrator packages everything it's needed and sends to package & request to fabric controller.
                    

# Purchasing & Licensing Options

## Azure purchasing options

1. From Microsoft by signing up through Azure website [Azure.com](http://Azure.com)
    
    * 📝 Monthly billing
        
2. From Microsoft through a Microsoft representative
    
    * 📝 Monthly billing
        
3. From a Microsoft partner
    
    * CSP = **Cloud Solution Provider**
        
        * Offer a range of complete managed cloud solutions for Azure.
            
    * Your partner will provide you with access to Azure, manage your billing, and provide support.
        

## Licensing

### Free-trial

* Free access to some Azure products for 12 months
    
* $200 USD credit to spend for the first 30 days on any service.
    
* Sign-up from [sign-up page](https://azure.microsoft.com/free)
    

### Pay-as-you-go

* Get billed for services as you use them
    

### CSP (Cloud Solution Provider)

* Buy Azure services from a Microsoft Partner organization
    
* You will be billed by the partner organization.
    
* First line Azure support will be provided by the partner organization.
    

### Azure in Open licensing

* You buy from a third party reseller using a 12 month upfront commitment
    
* Buy Azure Monetary Commitment credits to use in your subscription.
    

### Enterprise Agreement (EA)

* For big enterprises
    
* **EA Portal**: enterprise overview of all the spending and budgeting for organization's Azure spend
    
* **Discounts**: E.g. up to 30% cheaper virtual machines.
    
* **Enterprise Level Capabilities and Features**: Access to enterprise-only service.
    

# Account, Subscription, Support and Billing

* Requires: Phone number, credit card identity verification, Microsoft/GitHub account.
    

## Subscription

* Used to create and use Azure services
    
* Created for you when you sign up
    
* 📝 Logical container used to provision resources in Azure such as virtual machines, databases and more.
    
* 📝 When you create an Azure resource like a VM, you identify the subscription it belongs to
    
    * As you use the VM, the usage of the VM is aggregated and billed monthly.
        
* 📝 Each subscription is a separate entity that can't be merged.
    

### Multiple Azure Subscriptions

* You can create new subscriptions to separate e.g.
    
    * **Environments**
        
        * E.g. for testing, security, or to isolate data for compliance reasons.
            
        * 💡Useful because resource access control occurs at the subscription level.
            
    * **Organizational structures**
        
        * E.g. limit a team to lower-cost resources & allow IT department a full range
            
        * 💡Allows you to manage and control access to the resources that users provision within each subscription
            
    * **Billing**
        
        * Costs are first aggregated at the subscription level
            
            * Manage and track costs based on your needs
                
        * E.g. for production, development, testing
            
* Or due to **subscription limits**:
    
    * Subscriptions are bound to some hard limitations
        
        * E.g. the maximum number of Express Route circuits per subscription is 10
            

## Billing

* You'll receive a monthly invoice with payment instructions provided
    
    * You also can get set up for multiple invoices.
        
* Customize billing
    
    * Allows you to e.g. have single invoice for organization but organize charges by department, team, or project.
        
    * Billing structure:
        
        * Each **billing account** has billing profile
            
            * Each **billing profile** has different invoice sections
                
                * Each **invoice section** can be coupled to different subscriptions.
                    
                    * Each invoice section is a line item on the invoice that shows the charges incurred that month
                        

## Support

### Free

* 24/7 access to the online documentation, community support, and new Azure capabilities demo videos on YouTube
    
* Demo videos by Azure engineers are available on [Azure Friday](https://azure.microsoft.com/en-us/resources/videos/azure-friday/), [Microsoft Mechanics](https://www.youtube.com/c/MicrosoftMechanicsSeries), Azure portal how-to videos playlists
    
* **Azure Quickstart Center**: Guided experience in the portal.
    
* **Azure Service Health**: Insights on issues related to your Azure services
    
* **Azure Advisor**: Personalized recommendations on how to optimize your cost and performance.
    

#### Basic support

* Included free for everyone.
    
* Billing and subscription management support
    
* Ability to submit as many support tickets as you need
    
    * Either through • Help + support on top right menu or on resource level (Resource blade -&gt; Support + troubleshooting -&gt; New support request)
        

#### Community support

| Channel | Description |
| --- | --- |
| Azure Knowledge Center | The Azure Knowledge Center is a searchable database that contains answers to common support questions. |
| Microsoft Tech Community | Get support by reading responses to Azure technical questions from Microsoft's developers and testers. |
| Stack Overflow | You can review answers to questions from the development community. |
| Server Fault | Review community responses to questions about System and Network Administration in Azure. |
| Azure Feedback Forums | Read ideas and suggestions for improving Azure made by Azure users. |
| Twitter | Tweet `@AzureSupport` to get answers and support from the official Microsoft Azure Twitter channel. |

### Paid

* 📝 Azure Support plans
    
    |  | Developer | Standard | Professional Direct |
    | --- | --- | --- | --- |
    | Best for | Non-critical workloads | Production workloads | Business-critical workloads |
    | Reactive technical support | 1 business day response | 1-hour response for critical cases | 1-hour response + priority tracking of critical cases |
    | Proactive technical support | Not applicable | Not applicable | Access to a pool of technical experts |
    
* You can also purchase [Azure Premier support](https://azure.microsoft.com/en-us/support/plans/premier/)
    
    * faster response times
        
    * Architecture/code review
        
    * onsite support..
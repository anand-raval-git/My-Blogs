---
title: "Day 07: Azure Services are Compute, Virtual Machines Their Examples of use-cases and Scaling and High Availability"
seoTitle: "Azure: Use Cases, Scaling & High Availability"
seoDescription: "Explore Azure services, compute options, virtual machines, scaling strategies, high availability, practical use-cases, and deployment tips"
datePublished: 2025-03-23T20:37:45.958Z
cuid: cm8m3nmna000308jle6t9affs
slug: day-07-azure-services-are-compute-virtual-machines-their-examples-of-use-cases-and-scaling-and-high-availability
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1742762209341/e74582bf-eee5-4b53-9de4-bd11b30426e1.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1742762254863/6f8d6c1e-b5a6-48e7-9d75-171f379ebfaf.png
tags: cloud, azure, cloud-computing, devops, 90daysofdevops

---

# Azure Services

* 📝 Microsoft notifies at least 1 months before ending support for an Azure service that does NOT have a successor service.
    
* **App Hosting**
    
    * Run entire your web application on a managed platform on Linux & Windows
        
    * In Azure Marketplace there are huge range of third party products you can run on Azure
        
        * Including SAP & SQL database solutions
            
* **Integration**
    
    * Logic apps and service bus connect applications & services
        
    * Allow for workflows to orchestrate business processes on cloud or on-premises
        
* **Security**
    
    * Security is integrated in every aspect of Azure
        
    * Hardened structures (designed to withstand a range of threats) & global security intelligence monitoring
        
    * **Azure Identity Management** gives you tight control to choose who gets access to what.
        

# Compute

* Primarily for performing calculations, executing logic and running applications
    
* On-demand & computing service for running cloud-based applications
    
* Provides computing resources like multi-core processors and supercomputers via virtual machines and containers.
    
* Provides serverless computing to run apps without requiring infrastructure setup or configuration.
    
* Pay only for the resources you use and only for as long as you're using them.
    
* Four common techniques for performing compute in Azure:
    
* ## Choosing a computing strategy
    
* "All or nothing" is not needed when choosing a cloud computing strategy.
    
* Each provides benefits as well as tradeoffs against other options.
    
* E.g. serverless computing removes the need for you to manage infrastructure
    
    * Serverless computing expects work to be completed quickly; usually within seconds or less.
        
    * You might run your core application on a virtual machine or container but offload some of the data processing onto a serverless app.
        
* 📝 Most control to least control: Virtual machines, containers, serverless computing
    
* Learn more: [Overview of Azure compute options](https://docs.microsoft.com/en-us/azure/architecture/guide/technology-choices/compute-decision-tree)
    

# Virtual Machines

* Infrastructure as a service (IaaS)
    
* Virtual machines, or VMs, are software emulations of physical computers.
    
* They include a virtual processor, memory, storage, and networking resources.
    
* They host an operating system (OS), and you're able to install and run software like a physical computer.
    
* You can connect to VM & control it using a remote desktop client.
    
* Good choice when you need:
    
    * Total control over the operating system (OS)
        
    * The ability to run custom software
        
    * To use custom hosting configurations
        
* Azure takes care of the physical hardware
    
    * You take care of configuring, updating, and maintaining the software that runs on the VM.
        
* An **image** is a template used to create a VM.
    
    * Includes an OS and often other software, like development tools or web hosting environments.
        

## Examples of use-cases

* **During test + dev** as it's easy to create different OS & application configurations. Easy to delete when not needed.
    
* **Minor tasks**. E.g. application handles fluctations in demand and shut down VMs when you don't need them & quickly start them to meet a suddenly increased demand.
    
* **Extending your datacenter** to the cloud, e.g. running SharePoint.
    
* **During disaster recovery**. E.g. if primary datacenter fails, create VMs running on Azure to run your critical applications and then shut them down when the primary datacenter becomes operational again.
    
* **Lift and shift**: Moving from physical datacenter to cloud. You can take image of the server & run within a VM with little to no changes.
    
* Learn more: [Typical scenarios for running Azure VMs](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/overview?toc=%2Fazure%2Fvirtual-machines%2Fwindows%2Ftoc.json)
    

## Scaling and High Availability

* 📝 [99.99% uptime guarantee](https://azure.microsoft.com/en-us/support/legal/sla/virtual-machines/v1_8/) for all Virtual Machines that have two or more instances deployed across two or more Availability Zones.
    

### Domains & maintenance events

#### Update domains

* Groups of VMs and underlying physical hardware that can be rebooted at the same time.
    

##### Planned maintenance events

* When the underlying Azure fabric that hosts VMs is updated by Microsoft.
    
* Done to patch security vulnerabilities, improve performance, and add or update features.
    
* Often no impact, sometimes requires reboot.
    
* When the VM is part of an availability set, the Azure fabric updates are sequenced so not all of the associated VMs are rebooted at the same time.
    
    * VMs are put into different **update domains**
        

#### Fault domains

* Fault domain = rack of servers.
    
* provides the physical separation of your workload across different power, cooling, and network hardware that support the physical servers in the data center server racks.
    
* In the event the hardware that supports a server rack becomes unavailable, only that rack of servers is affected by the outage.
    

##### Unplanned maintanance events

* Involve a hardware failure in the data center e.g. a power outage or disk failure
    
* VMs that are part of an availability set automatically switch to a working physical server so the VM continues to run.
    
* The group of virtual machines that share common hardware are in the same **fault domain**.
    

### Availability sets

* Logical grouping of two or more VMs that help keep your application available during planned or unplanned maintenance.
    
* With an availability set, you get:
    
    * ❗ Up to three **fault domains**
        
        * each have a server rack with dedicated power and network resources.
            
    * Five logical **update domains**
        
        * ❗ can be increased to a maximum of 20.
            
* There's no cost for an availability set.
    
    * Only pay for the VMs within the availability set.
        
* 💡📝 Recommended for high availability.
    

### Virtual machine scale sets

* Lets you create & manage a group of identical, load balanced VMs.
    
* Allow you to centrally manage, configure, and update a large number of VMs to provide highly available applications.
    
* The number of VM instances can automatically increase or decrease in response to demand or a defined schedule.
    
* 💡 Helps you build large-scale services for areas such as compute, big data, and container workloads.
    
* Provides high availability through [regional or multiple Availability Zones](https://docs.microsoft.com/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-use-availability-zones) deployment options.
    

### Azure Batch

* Large-scale job scheduling and compute management.
    
* When running a job, batch:
    
    1. Starts a pool of compute VMs for you
        
    2. Installs applications and staging data
        
    3. Runs jobs with as many tasks as you have
        
    4. Identifies failures
        
    5. Requeues work
        
    6. Scales down the pool as work completes
        
* 💡 Good for cases where you need raw computing power or supercomputer level compute power.
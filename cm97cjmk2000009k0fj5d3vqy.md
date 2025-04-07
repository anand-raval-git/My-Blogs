---
title: "Day 12: Shared Responsibility Model in Azure And What is Defence"
seoTitle: "Azure Shared Responsibility Model Explained"
seoDescription: "Learn about Azure's shared responsibility model and defense strategies for securing cloud services and data against unauthorized access"
datePublished: Mon Apr 07 2025 17:29:45 GMT+0000 (Coordinated Universal Time)
cuid: cm97cjmk2000009k0fj5d3vqy
slug: day-12-shared-responsibility-model-in-azure-and-what-is-defence
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1744046909457/ad5a719a-fc26-4fe7-b5c2-2a8b91257df9.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1744046968161/77a284c1-2e5c-4d98-adef-e6156724adf2.png
tags: cloud, azure, cloud-computing, devops

---

# Shared Responsibility Model

* Cloud security is a shared responsibility of both cloud providers and customers.
    
* Azure has many security certifications from outside auditors.
    
* **Physical security**
    
    * Handled by Microsoft
        
    * Walls, cameras, gates, security personnel
        
    * Strict procedures for employees
        
* **Digital security**
    
    * Handled by customer + Microsoft
        
    * Azure has tools to mitigate security threats, consumer is responsible to use the tools.
        
    * E.g. role-based access control, multi factor authentication, encryption, monitoring tools such as login failures, suspicious locations, DDoS protection, real-time telemetry & firewalls.
        
* ❗ You **always** retain responsibility for: Data, Endpoints, Accounts, Access management (identities)
    

## Cloud computing levels

* 📝 From maximum effort to your side to minimum: IaaS, PaaS, SaaS
    

| Responsibility | On-prem | IaaS | PaaS | SaaS |
| --- | --- | --- | --- | --- |
| Data governance & rights management | 🤪 | 🤪 | 🤪 | 🤪 |
| Client endpoints | 🤪 | 🤪 | 🤪 | 🤪 |
| Account & access management | 🤪 | 🤪 | 🤪 | 🤪 |
| Identity & directory infrastructure | 🤪 | 🤪 | ☁️🤪 | ☁️🤪 |
| Application | 🤪 | 🤪 | ☁️🤪 | ☁️ |
| Network controls | 🤪 | 🤪 | ☁️🤪 | ☁️ |
| Operating system | 🤪 | 🤪 | ☁️ | ☁️ |
| Physical host | 🤪 | ☁️ | ☁️ | ☁️ |
| Physical network | 🤪 | ☁️ | ☁️ | ☁️ |
| Physical datacenter | 🤪 | ☁️ | ☁️ | ☁️ |

* Cloud provider: ☁️
    
* Customer: 🤪
    

Azure-in-bullet-points/AZ-900 Microsoft Azure Fundamentals/4.1. Shared Responsibility [Model.md](http://Model.md) at master · undergroundwires/Azure-in-bullet-points

  
Defence in Depth

* Strategy to slow the advance of an attack to get unauthorized access to information.
    
* Layered approach: Each layer provides protection, so if one layer is breached, a subsequent prevents further exposure.
    
* Applied by Microsoft, both in physical data centers and across Azure services.
    

## Layers

* ![Defence in depth layers](https://github.com/undergroundwires/Azure-in-bullet-points/raw/master/AZ-900%20Microsoft%20Azure%20Fundamentals/img/defence-in-depth.png align="left")
    

### Data

* In almost all cases attackers are after data.
    
* Data can be in database, stored on disk inside VMs, on a SaaS application such as a Microsoft 365 app or in cloud storage.
    
* Those storing and controlling access to data to ensures that it's properly secured
    
* Often regulatory requirements dictates controls & processes
    
    * to ensure confidentiality, integrity, and availability.
        

### Application

* Ensure applications are secure and free of vulnerabilities.
    
* Store sensitive application secrets in a secure storage medium.
    
* Make security a design requirement for all application development.
    
* Integrate security into the application development life cycle,
    

### Compute

* Secure access to virtual machines.
    
* Implement endpoint protection and keep systems patched and current.
    
    * Malware, unpatched systems, and improperly secured systems open your environment to attacks.
        

### Networking

* Limit communication between resources.
    
* Deny by default.
    
    * Allow only what is required
        
* Restrict inbound internet access and limit outbound, where appropriate.
    
* Implement secure connectivity to on-premises networks.
    

### Perimeter

* Use distributed denial of service (DDoS) protection to filter large-scale attacks before they can cause a denial of service for end users.
    
* Use perimeter firewalls to identify and alert on malicious attacks against your network.
    

### Identity and access

* Control access to infrastructure and change control.
    
* Access granted is only what is needed
    
* Use single sign-on and multi-factor authentication.
    
* Audit events and changes.
    

### Physical security

* Building security & controlling access to computing hardware.
    
* First line of defense
    

Azure-in-bullet-points/AZ-900 Microsoft Azure Fundamentals/4.2. Defence in [Depth.md](http://Depth.md) at master · undergroundwires/Azure-in-bullet-
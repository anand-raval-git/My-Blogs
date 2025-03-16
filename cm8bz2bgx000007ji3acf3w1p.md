---
title: "Day 03 : Azure IaaS vs PaaS vs SaaS and Cloud Compliance"
seoTitle: "Azure Services Compared: IaaS, PaaS, SaaS"
seoDescription: "Explore the differences between IaaS, PaaS, SaaS, and cloud compliance essentials to enhance your understanding of cloud-based solutions"
datePublished: Sun Mar 16 2025 18:31:31 GMT+0000 (Coordinated Universal Time)
cuid: cm8bz2bgx000007ji3acf3w1p
slug: day-03-azure-iaas-vs-paas-vs-saas-and-cloud-compliance
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1742149834662/a8a21b25-7c66-41f7-b966-c30232e88811.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1742149879161/8d0baec7-5b7c-4726-98aa-78af29f3ead1.png
tags: cloud, azure, cloud-computing, devops, cloud-native

---

# IaaS vs PaaS vs SaaS

## Three categories of cloud computing

* 📝 [IaaS](https://github.com/undergroundwires/Azure-in-bullet-points/blob/master/AZ-900%20Microsoft%20Azure%20Fundamentals/1.3.2.%20IaaS%20vs%20PaaS%20vs%20SaaS.md#infrastructure-as-a-service-iaas), [PaaS](https://github.com/undergroundwires/Azure-in-bullet-points/blob/master/AZ-900%20Microsoft%20Azure%20Fundamentals/1.3.2.%20IaaS%20vs%20PaaS%20vs%20SaaS.md#platform-as-a-service-paas), [SaaS](https://github.com/undergroundwires/Azure-in-bullet-points/blob/master/AZ-900%20Microsoft%20Azure%20Fundamentals/1.3.2.%20IaaS%20vs%20PaaS%20vs%20SaaS.md#software-as-a-service-saas).
    
* Allows using a combination of these types of infrastructure.
    
    * E.g. [Microsoft 365 Apps](https://www.microsoft.com/en-ww/microsoft-365/business/microsoft-365-apps-for-business?market=af) on company computers (SaaS), VMs (IaaS) on Azure and Azure SQL Database (PaaS) to store your data.
        

### Infrastructure as a service (IaaS)

* Instant computing infrastructure, provisioned and managed over the internet.
    
* Aims to give you the most control over the provided hardware that runs your application
    
* 📝 E.g. virtual machines (VMs), storage, and operating systems.
    
* You rent hardware instead of buying
    
* Ensuring that a service is up and running is a shared responsibility
    
    * cloud provider ensures the cloud infrastructure is functioning correctly
        
    * cloud customer ensures the service they are using is
        
        * configured correctly
            
        * up to date
            
        * available to their customers.
            

#### Common IaaS use cases

* **Migrating workloads**: Managed similar to on-prem infrastructure & provides easy migration path.
    
* **Test and development**: Teams can quickly set-up & dispose test/dev environments with fast & economical scaling.
    
* **Storage, backup and recovery**: Organizations avoid the capital outlay and complexity of storage management.
    
    * Useful for managing unpredictable demand and steadily growing storage needs.
        
    * can also simplify the planning and management of backup and recovery systems.
        

### Platform as a service (PaaS)

* Provides an environment for building, testing, and deploying software applications
    
    * Can add features such authentication.
        
* Aims to help creating an application quickly without managing the underlying infrastructure.
    
    * 📝 E.g. for a web app / Azure SQL databases you don't need to install an operating system, web server, or even system updates.
        
* Resources are purchased on a pay-as-you-go basis and accessed over a secure Internet connection.
    

#### Common PaaS use cases

##### Development framework

* Lets developers create applications using built-in software components.
    
* 📝 Cloud features such as scalability, high-availability, and multi-tenant capability are included
    
* Reducing the amount of coding that developers must do.
    

##### Analytics or business intelligence

* Tools provided as a service with PaaS allow organizations to analyze and mine their data.
    
* They can find insights and patterns, and predict outcomes to improve business decisions such as forecasting, product design, and investment returns.
    

### Software as a service (SaaS)

* Software that is centrally hosted and managed for the end customer.
    
* Usually based on an architecture where one version of the application is used for all customers
    
* Usually licensed through a monthly or annual subscription
    
* 📝 E.g. Office 365, Skype, and Dynamics CRM Online.
    

## Cost and Ownership

|  | IaaS | PaaS | SaaS |
| --- | --- | --- | --- |
| Upfront costs | None, pay for what you use | None, pay for what you use | None, monthly / annual subscription |
| User ownership | purchase, installation, configuration, and management of their own software, operating systems, middleware, and applications | development of their own applications | not responsible for any maintenance or management of that software. |
| Cloud provider ownership | underlying cloud infrastructure (such as virtual machines, storage, and networking) is available for the user. | operating system management, network, and service configuration.. typically everything except user application | provision, management, and maintenance of the application software |

## Management responsibilities

* These categories are layers on top of each other
    
    * Abstraction order: SaaS &gt; PaaS &gt; IaaS
        
    * Abstraction = Hide details, quicker production but less control over the underlying hardware.
        
* IaaS: user is responsible for managing the operating systems, data, and applications.
    
* PaaS: user is responsible for the applications and data they run and store.
    
* SaaS: user just uses the software.
    

[![shared responsibility model](https://github.com/undergroundwires/Azure-in-bullet-points/raw/master/AZ-900%20Microsoft%20Azure%20Fundamentals/img/shared-responsibility-model.png align="left")](https://github.com/undergroundwires/Azure-in-bullet-points/blob/master/AZ-900%20Microsoft%20Azure%20Fundamentals/img/shared-responsibility-model.png)

# Cloud Compliance

* Provider can help you comply with regulations and standards
    
* Think about:
    
    * How compliant is the cloud provider when it comes to handling sensitive data?
        
    * How compliant are the services offered by the cloud provider?
        
    * How can I deploy my own cloud-based solutions to scenarios that have accreditation or compliance requirements?
        
    * What terms are part of the privacy statement for the provider?
        

## Some compliance offerings

### CJIS

* CJIS = Criminal Justice Information Services
    
* Any US state or local agency that wants to access the FBI's CJIS database is required to adhere to the CJIS Security Policy
    
* Microsoft Azure adheres to the same requirements that law enforcement and public safety entities must meet.
    

### CSA STAR Certification

* CSA = Cloud Security Alliance
    
* Independent third-party assessment of a cloud provider's security posture
    
* Ensures:
    
    * ISO/IEC 27001 certification is achieved
        
    * Criteria specified in the Cloud Controls Matrix (CCM) are met
        
        * Also assesed against the STAR Capability Maturity Model for the management of activities in CCM control areas.
            

### GDPR

* 📝 GDPR = General Data Protection Regulation, european privacy law
    
* Imposes rules for collecting & analyzing data tied to EU residents.
    
* The GDPR applies no matter where you are located.
    

### EU Model Clauses

* EU Standard Contractual Clauses
    
* Guarantees around transfers of personal data outside of the EU.
    
* Ensures customers can use cloud service to move data freely through cloud from Europe to the rest of the world.
    

### HIPAA

* HIPAA = Health Insurance Portability and Accountability Act
    
* US federal law that regulates patient Protected Health Information (PHI)
    
* HIPAA Business Associate Agreement (BAA)
    
    * Adheres o certain security and privacy provisions in HIPAA and the Health Information Technology for Economic and Clinical Health (HITECH) Act.
        
* Azure offers BAA as contract addendum to assist customers individual compliance.
    

### ISO/IEC 27018

* 📝 ISO/IEC 27018 = International Organization for Standardization (ISO) and the International Electrotechnical Commission (IEC) 27018
    
* Covers the processing of personal information by cloud service providers
    

### MTCS Singapore

* MTCS = Multi-Tier Cloud Security (MTCS) Singapore
    
* MTCS 584:2013 asses for IaaS & PaaS & SaaS service classifications.
    

### SOC 1, 2, and 3

* SOC = Service Organization Controls
    
* Cloud services audited at least annually against the SOC report framework by independent third-party auditors.
    
* Audit covers controls for data security, availability, processing integrity, and confidentiality
    
    * as applicable to in-scope trust principles for each service.
        

### NIST CSF

* 📝 NIST CSF = National Institute of Standards and Technology (NIST) Cybersecurity Framework (CSF)
    
    * NIST is agency of United States Department of Commerce.
        
* Voluntary framework that defines security guidelines, and best practices to manage cybersecurity-related risks.
    
* Azure have undergone independent, third-party Federal Risk and Authorization Management Program (FedRAMP) Moderate and High Baseline audits & is certified
    
    * Also validated by the Health Information Trust Alliance (HITRUST)
        
        * a leading security and privacy standards development and accreditation organization
            

### UK Government G-Cloud

* Cloud computing certification for services used by government entities in UK.
    
* Azure has received official accreditation from the UK Government Pan Government Accreditor.
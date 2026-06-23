---
title: "Day 06: Azure Resource Manager (Resources & Resource Groups & Management Groups) and Compliance in Azure"
seoTitle: "Azure Resource Manager & Compliance Overview"
seoDescription: "Azure Resource Manager groups resources for compliance and management, ensuring effective access and organization in Azure environments"
datePublished: 2025-03-22T18:13:02.150Z
cuid: cm8kj1nie000207leawmk2r98
slug: day-06-azure-resource-manager-resources-and-resource-groups-and-management-groups-and-compliance-in-azure
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1742667111021/7fe16b2a-7d62-423e-896b-7886631f0d8c.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1742667165070/51d5d0fb-70e8-4fb9-8e4d-9ff5f1a7c07f.png
tags: cloud, azure, cloud-computing, devops, azure-devops

---

# Azure Resource Manager (Resources & Resource Groups & Management Groups)

## Azure Resource

* Anythings you create in an Azure subscription
    
* E.g. virtual machines, Application Gateways, and CosmosDB instances
    
* 💡 Good to have consistent naming convention e.g.: `cloudarchitecture-prod-infrastructure-rg`
    
    * what it's used for (`cloudarchitecture`)
        
    * environment (`prod`)
        
    * the types of resources contained within (`infrastructure`)
        
    * type of resource it is itself (`rg` = resource group)
        
* Provides fine-grained access management through [role-based access control (RBAC)](https://github.com/undergroundwires/Azure-in-bullet-points/blob/master/AZ-900%20Microsoft%20Azure%20Fundamentals/4.4.%20Identity%20and%20Access%20\(Azure%20AD\).md#role-based-access-control)
    
* 📝 You can move some resources that supports move to a new resource group or subscription if they [support move operation](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-move-resources).
    

### Tagging

* Helps you better search, filter, and organize these resources
    
* Name/value pairs of text data that you can apply to resources and resource groups
    
* E.g.
    
    * department (like finance, marketing, and more)
        
    * environment (prod, test, dev)
        
    * cost center
        
    * life cycle and automation (like shutdown and startup of virtual machines)
        
* 💡📝 Good way to group your billing data
    
    * E.g. VMs on production that belongs to a cost center A.
        
* 💡 Help with monitoring
    
    * You can set-up alerts based on tags e.g. if a resource fails notification goes to the finance department.
        
* 💡 Help with automation
    
    * E.g. `shutdown:6PM` and `startup:7AM` tag TO automate the shutdown and startup of virtual machines in development environments during off-hours to save costs.
        
* 💡 Help with automation Governance through [Policies](https://github.com/undergroundwires/Azure-in-bullet-points/blob/master/AZ-900%20Microsoft%20Azure%20Fundamentals/5.1.%20Azure%20Policy%20&%20Azure%20Blueprints.md)
    
    * E.g. ensure that all resources have the Department tag associated with them and block creation if it doesn't exist.
        
* ❗ Limitations:
    
    * A resource can have up to 50 tags.
        
    * 📝 Tags aren't inherited from parent resources.
        
    * 📝 Not all resource types support tags
        

### Resource locks

* 📝 Blocks modification (**Read-only**) or deletion (**Delete**) of the resource.
    
    * For more granular control of what can be deployed e.g. see [Azure policies](https://github.com/undergroundwires/Azure-in-bullet-points/blob/master/AZ-900%20Microsoft%20Azure%20Fundamentals/5.1.%20Azure%20Policy%20&%20Azure%20Blueprints.md#azure-policy)
        
* Read-only allows only `HTTP GET` requests
    
    * ❗ Can lead to unexpected results e.g. listing all objects in a storage account requires `POST` request is denied
        
* 📝 You must remove the lock in order to perform forbidden activity.
    
* Apply regardless of RBAC permissions
    
* 📝 Protects against accidental deletion
    
* 💡 Use to protect key resources that could have a large impact if they were removed or modified
    
    * E.g. ExpressRoute circuits, virtual networks, critical databases, and domain controllers
        
* Only "Owner" and "User Access Administrator" can create/delete locks
    
    * It requires access to `Microsoft.Authorization/locks/*`
        

## Azure Resource Group

* Also an Azure resource so it can have locks, tags, RBAC permissions etc.
    
    * It's free!
        
* Logical container for resources deployed on Azure.
    
* Tied to a region & subscription itself.
    
    * 📝 But can contain resources from different regions
        
        * ❗If region the RG goes down, the management of the RG would not work.
            
* Helps you organize resources
    
    * You can place resources of e.g. similar usage, type, or location in same group.
        
* 📝 If you delete a resource group, all resources contained within are also deleted.
    
* Authorization
    
    * Scope for applying role-based access control (RBAC) permissions.
        
    * Permissions are inherited in all resources that the group has.
        
* ❗ All resources must be in a resource group and a resource can only be a member of a single resource group.
    
    * Before any resource can be provisioned, you need a resource group
        
* ❗ Some services has specific limitations or requirements to move from one resource group to another
    
* ❗ Can't be nested.
    
* Can see history of the deployments to a resource group
    

### Organizing resource groups

* By type (virtual networks, virtual machines, cosmos dbs)
    
    * ![by type](https://github.com/undergroundwires/Azure-in-bullet-points/raw/master/AZ-900%20Microsoft%20Azure%20Fundamentals/img/organize-resource-groups/by-resource-type.png align="left")
        
* By environment (prod, qa, dev)
    
    * ![by environment](https://github.com/undergroundwires/Azure-in-bullet-points/raw/master/AZ-900%20Microsoft%20Azure%20Fundamentals/img/organize-resource-groups/by-environment.png align="left")
        
* By department (marketing, finance, human resources)
    
    * ![by department](https://github.com/undergroundwires/Azure-in-bullet-points/raw/master/AZ-900%20Microsoft%20Azure%20Fundamentals/img/organize-resource-groups/by-department.png align="left")
        
* Combining strategies e.g. environment and department:
    
    * ![by department and environment](https://github.com/undergroundwires/Azure-in-bullet-points/raw/master/AZ-900%20Microsoft%20Azure%20Fundamentals/img/organize-resource-groups/by-department-and-environment.png align="left")
        
* By authorization
    
    * By who needs to administer them.
        
    * See [RBAC](https://github.com/undergroundwires/Azure-in-bullet-points/blob/master/AZ-900%20Microsoft%20Azure%20Fundamentals/4.4.%20Identity%20and%20Access%20\(Azure%20AD\).md#role-based-access-control)
        
    * E.g. databases in database administration group to give access to database administrators.
        
* By life cycle
    
    * Allows you to e.g. delete after experimentation.
        
* By billing
    
    * A way to filter and sort the data to better understand where costs are allocated.
        

## Management Groups

* 📝 Groups multiple subscriptions.
    
* 📝 Can have RBAC assignments and policies
    
    * Inherited by underlying subscriptions
        
* Good for enterprises
    
* E.g.
    
    * ![management groups](https://github.com/undergroundwires/Azure-in-bullet-points/raw/master/AZ-900%20Microsoft%20Azure%20Fundamentals/img/management-groups.png align="left")
        

# Compliance in Azure

## Microsoft Privacy Statement

* [privacy.microsoft.com/privacystatement](https://privacy.microsoft.com/en-us/privacystatement)
    
* 📝 Explains what personal data Microsoft processes, how Microsoft processes it, and for what purposes.
    
* Applies to the interactions Microsoft has with you and Microsoft products such as Microsoft services, websites, apps, software, servers, and devices.
    

## Microsoft Trust Center

* [microsoft.com/trust-center](https://www.microsoft.com/trust-center)
    
* 📝 In-depth information about security, privacy, compliance offerings, policies, features, and practices across Microsoft cloud products.
    
* Recommended resources in the form of a curated list of the most applicable and widely used resources for each topic.
    
* Direct guidance and support
    

## Service Trust Portal

* [servicetrust.microsoft.com](https://servicetrust.microsoft.com/)
    
* 📝 Can download
    
    * audit reports produced by external auditors
        
    * Microsoft-authored reports about its cloud services.
        
* Also has compliance guides to help you understand how you can use Microsoft cloud service features to manage compliance with various regulations.
    
* Hosts [Compliance Manager](https://github.com/undergroundwires/Azure-in-bullet-points/blob/master/AZ-900%20Microsoft%20Azure%20Fundamentals/2.7.%20Compliance%20in%20Azure.md#compliance-manager), companion feature to the [Trust Center](https://github.com/undergroundwires/Azure-in-bullet-points/blob/master/AZ-900%20Microsoft%20Azure%20Fundamentals/2.7.%20Compliance%20in%20Azure.md#microsoft-trust-center).
    

### Compliance Manager

* [servicetrust.microsoft.com/ComplianceManager](https://servicetrust.microsoft.com/ComplianceManager)
    
* Free workflow-based risk assessment dashboard with
    
    * summary of your data protection, compliance stature, recommendations for improvement
        
* Features:
    
    * Combines the following three items:
        
        1. Information provided by Microsoft to auditors and regulators e.g.ISO 27001, ISO 27018, and NIST.
            
        2. Information that Microsoft compiles internally for its compliance with regulations (such as HIPAA and the EU GDPR).
            
        3. An organization's self-assessment of their own compliance with these standards and regulations.
            
    * Repository in which to upload and manage evidence and other artifacts related to compliance activities.
        
    * Assign, track, and record compliance and assessment-related activities
        
        * Help your organization cross team barriers to achieve your organization's compliance goals.
            
    * ***Compliance Score*** to help you track your progress with onging risk assessments.
        
        * Recommends also actions as part of the risk assessment.
            
    * Excel reports that document the compliance activities performed by Microsoft and your organization.
        
        * 💡 Can be provided to auditors, regulators, and other compliance stakeholders
            

## Azure Security Center

* 📝 Global service in Azure that includes regulatory compliance dashboard of **your** services.
    
* Insights into your compliance posture based on continuous assessments
    
* Analyzes risk factors in your hybrid cloud environment according to security best practices
    
* Overall security score, assessment against e.g. CIS, PCI DSS 3.2.1, SOC, ISO 27001..
    
* ![Compliance Dashboard in Azure Security Center](https://github.com/undergroundwires/Azure-in-bullet-points/raw/master/AZ-900%20Microsoft%20Azure%20Fundamentals/img/compliance-dashboard.png align="left")
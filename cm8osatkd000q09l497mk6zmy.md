---
title: "Day 08 : Containers in Azure and Micro-services, App Service"
seoTitle: "Azure Containers & Microservices: Day 8 Recap"
seoDescription: "Explore Azure containers, microservices, and app services to enhance app deployment, scalability, and management with efficient platform solutions"
datePublished: 2025-03-25T17:43:11.149Z
cuid: cm8osatkd000q09l497mk6zmy
slug: day-08-containers-in-azure-and-micro-services-app-service
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1742924535471/37fc6381-f5d9-4da5-9d16-4420d95ee684.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1742924574805/c9b02567-ea59-420a-9f5c-668736515ec1.png
tags: cloud, azure, cloud-computing, devops

---

# Containers

* Virtualization environment for running applications.
    
* Bundles apps + operating system + runtime.
    
* Run on top of a host operating system like VMs.
    
    * But unlike VMs, containers don't include an operating system for the apps running inside the container.
        
        * A container doesn't use virtualization
            
    * Instead, containers bundle the libraries and components needed to run the application and use the existing host OS running the container.
        
        * Those not waste resources simulating virtual hardware with a redundant OS.
            
            * You can run multiple isolated applications on a single container host.
                
            * Much more lightweight than VMs.
                
                * Allows you to quickly respond to changes in demand or failure
                    
        * E.g. if five containers are running on a server with a specific Linux kernel, all five containers and the apps within them share that same Linux kernel.
            
* The container orchestrator can start, stop, and scale out application instances as needed.
    
    * Faster than VM (seconds instead of minutes)
        
* You can use same server to host multiple container applications
    
    * They are secured and isolated
        
* More efficient than VM
    
    * Run containers side by side without sacrificing isolation.
        
    * Much smaller in size
        
    * Development process is simplified. Dev env = prod env.
        

## Containers in Azure

### Azure Container Instances

* PaaS: Fastest & simplest way to run containers
    
* No configuration of VM or any other additional services.
    
* Just upload containers + run with automatic scaling
    

### Azure Kubernetes Service

* Orchestration = The task of automating, managing, and interacting with a large number of containers
    
* Azure Kubernetes Service (AKS) is a complete orchestration service for containers
    
* You can migrate existing apps to AKS e.g. :
    
    1. Convert an existing application to one or more containers and then publish one or more container images to the Azure Container Registry.
        
    2. Deploy the containers to an AKS cluster using the Azure portal or the command line.
        
    3. Azure AD controls access to AKS resources.
        
    4. You access SLA-backed Azure services, such as Azure Database for MySQL, via OSBA.
        
    5. Optionally, AKS is deployed with a virtual network.
        

#### Kubernetes

* Most popular option for managing container-based workloads
    
* Combines container management automation with an API
    
* Cloud-native: Can run across different clouds
    
* **Pod management**
    
    * A pod is a group of one or more containers that share the same network namespace and can communicate with eachother via '[localhost](http://localhost)'
        
    * 1 pod = 1 or more containers on a node
        
        * If node is removed = Kubernetes move affected workloads to different node.
            
    * If one pod crashes = Kubernetes creates new instance
        
    * Pods can be scaled manually or automatically (horizontal)
        
* Spreads deployment to minimize downtime
    
    * If update is problematic, it can roll-back
        
* Can manage storage
    
    * Persistent volumes to represent data storage to one or more containers
        
    * Data can be persisted across many pod instances
        
    * Can utilize cloud-based storage and data system e.g. Azure storage + Cosmos DB
        
* Can manage networking
    
    * Can expose pods to internet
        
    * Load balances traffic across multiple replicas of a pod
        
    * Network isolation
        
    * Policy-driven network security.
        
    * Manage communication + name resolution between pods
        
* It can be extended with additional capabilities
    
    * E.g. cloud events on pod creation, custom pod scheduling logic, on-demand provisioning of managed cloud services.
        

## Micro-services

* Architecture where you break solutions into smaller, independent pieces.
    
* Allows you to separate portions of your app into logical sections that can be maintained, scaled, or updated independently.
    
* Each service has small code-base that can be managed by a small development team.
    
* Don't need to share same technology stack, libraries or frameworks.
    
    * Each team can choose the right tool for the job.
        
    * Single development team can test & build & deploy a service
        
* Results in continuous innovation and faster release cadence.
    
* Smaller scope =
    
    * Easier to understand code-base
        
    * Easier for new team members to get started
        
* Each micro-service is completely autonomous with no cross-dependencies.
    
    * Provides fault isolation: If one goes down, it does not take out all application
        
* Communicates with each other using Application Programming Interface (API)
    
    * APIs encapsulate internal functionality.
        
        * Internal implementation details of each services are encapsulated behind their interface.
            
    * 💡Good practices:
        
        * Reduce interdependencies
            
        * Introduce orchestration / management layer in the higher level consuming application to coordinate calls and combine results.
            
* 💡 Good for:
    
    * High release velocity
        
    * Highly scalable applications
        
    * Applications with rich domains / subdomains
        
    * Organizations with small development teams
        

### Micro-services deployment

* Allows each microservice to be deployed independently of every other microservice.
    
* A team can update an existing service without rebuilding/redeploying the entire application.
    
* They can easily roll back & roll forward & update if something goes wrong.
    
* Makes bug fixes + feature releases more manageable & less risky
    
* Allows each microservice
    
    * to be scaled independently
        
    * persist own data & external state without common repository layer
        
* E.g. one for front-end, one for back-end and one for storage.
    
    * If back-end reaches capacity but not others, you can scale it individually.
        
    * Allows you replace storage microservice without affecting rest of the application.
        

### Azure Service Fabric

* Distributed systems platform
    
* Runs in Azure or on-premises
    

# App Service

* Azure App Service is an HTTP-based service.
    
* Enables you to build and host many types of web-based solutions without managing infrastructure.
    
* E.g. you can host web apps, mobile back-ends, and RESTful APIs in several supported programming languages.
    
* Supports different frameworks such as .NET, .NET Core, Java, Ruby, Node.js, PHP, Python..
    
* Can scale on both both Windows and Linux-based environments.
    

## Mobile apps

* Allows developers to create mobile backend as a service (MBaaS)
    
* Features include
    
    * Autoscaling
        
    * Offline data synchronization
        
    * Broadcasting push notifications
        
    * Integration with identity providers including Azure Active Directory, Google, Twitter, Facebook, and Microsoft
        

## Azure Marketplace

* Online store that hosts applications that are certified and optimized to run in Azure.
    
* Many types of applications are available, e.g. AI / web applications.
    
* Deployments from the store are done via the Azure portal using a wizard-style user interface.
    
    * Makes evaluating different solutions easy.
        

## Pricing tiers

* Categories
    
    | Category | Description |
    | --- | --- |
    | **Dev / Test** | Ideal for less demanding workloads. Focused on providing shared infrastructure. Additional features include custom domains / SSL and manual scale. |
    | **Production** | Ideal for more demanding workloads. Additional features include staging slots, daily backups, and a traffic manager. |
    | **Isolated** | Ideal for workloads that require advanced networking and fine-grained scaling. |
    
* Within each category, there are different pricing tiers.
    

### Scale up an App Service

1. Open the [Azure portal](https://portal.azure.com)
    
2. From the left-hand navigation menu (may need to click on menu icon), select **Dashboard**
    
3. Select the **App Service** with the name you chose it in the previous exercise.
    
4. Under **Settings** you see many configurable settings
    
5. Select **Scale up (App service plan)**.
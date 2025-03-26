---
title: "Day 09: What is Serverless Computing In Azure and How many types of storage are there in azure"
seoTitle: "Understanding Serverless and Azure Storage Types"
seoDescription: "Discover Azure's serverless computing with Azure Functions and Logic Apps, and explore storage types like Azure Blob, Disk, and Queue Storage"
datePublished: Wed Mar 26 2025 19:11:05 GMT+0000 (Coordinated Universal Time)
cuid: cm8qavpq8000h0ajoa454b3a8
slug: day-09-what-is-serverless-computing-in-azure-and-how-many-types-of-storage-are-there-in-azure
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1743016209267/64c0ecd3-d10e-4213-a9d8-75be6b2cb698.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1743016256071/ed80ed35-f6d1-4d62-807a-bd07c0b3ce13.png
tags: cloud, azure, cloud-computing, devops, azure-devops

---

# Serverless Computing

* 📝 Serverless computing services in Azure are:
    
    * Azure Functions and Azure Logic Apps
        

## Serverless concepts

### Abstraction of servers

* Completely abstracts the underlying hosting environment.
    
* No infrastructure configuration / maintenance.
    
    * Basically deploy your code and it runs with high availability.
        
* Automatically scaling, performance and allocation/deallocation of resources
    
    * You never explicitly reserve capacity.
        

### Event-driven scale

* Good fit for workloads that respond to incoming events.
    
* Events include triggers by e.g.
    
    * timers e.g. if a function needs to run every day at 10:00 AM UTC
        
    * HTTP e.g. API and webhook scenarios
        
    * queues e.g. with order processing)
        
* Triggers & bindings
    
    * A function contains both code and metadata about its triggers and bindings.
        
    * Triggers define how a function is invoked
        
    * Bindings provide a declarative way to connect to services from within the code.
        
* The platform automatically schedules the function to run and scales the number of compute instances based on the rate of incoming events.
    

### Micro-billing

* Pay only for the time the code runs.
    
* No active function executions occur = they're not charged.
    
* E.g. if the code runs once a day for two minutes, they're charged for one execution and two minutes of computing time.
    

## Azure Functions

* Can execute code in almost any modern language.
    
* Commonly used when you need to perform work in response to an event.
    
* Can be either
    
    * **Stateless** (the default)
        
        * Behave as if restarted every time responding to an event
            
    * **Stateful** (called "Durable Functions")
        
        * Has a context to track prior activity.
            
* Open-source, can deploy anywhere. See [Azure functions host](https://github.com/Azure/azure-functions-host)
    

## Azure Logic Apps

* Execute workflows designed to automate business scenarios and built from predefined logic blocks.
    
* Every logic app workflow starts with a trigger (many can be scheduled) and runs actions
    
    * Actions include data conversions and flow controls (e.g. conditional / switch statements, loops, and branching)
        
* You create using a visual designer on the Azure portal or in Visual Studio.
    
    * The workflows are persisted as a JSON file with a known workflow schema.
        
* Azure provides over 200 different connectors and processing blocks to interact with different services
    
    * You can also build custom connectors to interact.
        
* Often no code is written.
    
* E.g. a ticket arrives in ZenDesk, you could detect the intent of the message with cognitive services and then create an item in SharePoint to track the issue.
    

## Functions vs. Logic Apps

Functions and Logic Apps can both create complex orchestrations. An orchestration is a collection of functions or steps, that are executed to accomplish a complex task. With Azure Functions, you write code to complete each step, with Logic Apps, you use a GUI to define the actions and how they relate to one another.

You can mix and match services when you build an orchestration, calling functions from logic apps and calling logic apps from functions. Here are some common differences between the two.

|  | Functions | Logic Apps |
| --- | --- | --- |
| **State** | Normally stateless, but Durable Functions provide state | Stateful |
| **Development** | Code-first (imperative) | Designer-first (declarative) |
| **Connectivity** | Write code for custom bindings from many binding types | Large collection of connectors, Enterprise Integration Pack for B2B scenarios, build custom connectors |
| **Actions** | Each activity is an Azure function; write code for activity functions | Large collection of ready-made actions |
| **Monitoring** | Azure Application Insights | Azure portal, Log Analytics |
| **Management** | REST API, Visual Studio | Azure portal, REST API, PowerShell, Visual Studio |
| **Execution context** | Can run locally or in the cloud | Runs only in the cloud. |

# Storage

* Secure, durable, scalable, and easily accessible from across the globe.
    
* E.g. persistent data across devices for mobile applications.
    
* Uses REST API endpoints that make data available to huge range of application types & platforms e.g. .NET, JAVA, NODE.
    

## Benefits

* **Automated backup and recovery**: mitigates the risk of losing data if there is any unforeseen failure or interruption.
    
* **Replication across the globe**
    
    * Copies your data to protect it against any planned or unplanned events
        
        * e.g. scheduled maintenance or hardware failures.
            
    * Allows you to replicate your data at multiple locations across the globe.
        
* **Support for data analytics**: supports performing analytics on your data consumption.
    
* **Encryption capabilities**: You have tight control over who can access the data.
    
* **Multiple data types**: Almost any e.g. videos, text, like binary files. Many options for SQL and NoSQL data.
    
* **Data storage in virtual disks**: Up to 32 TB. Significant when you're storing heavy data such as videos and simulations.
    
* **Storage tiers**: To prioritize access to data based on frequently used vs rarely used information.
    

## Types of data

### Structured data

* Also called **relational data**
    
* Data that adheres to a schema.
    
    * Defines table, fields, clear relationship between two
        
* Can be stored in e.g. database table with rows and columns.
    
* Relies on keys to indicate how one row in a table relates to data in another row of another table.
    
* 💡 It's easy to enter, query, and analyze.
    
    * All of the data follows the same format.
        
    * E.g. sensor data or financial data.
        
* Azure services:
    
    * Azure SQL Database
        
    * Azure Cosmos DB (SQL API)
        

### Semi-structured data

* Also called as **non-relational** or **NoSQL data**.
    
* Doesn't fit neatly into tables, rows, and columns.
    
* Instead uses tags or keys that organize and provide a hierarchy for the data.
    
* Azure services:
    
    * Azure Cosmos DB (MongoDB API, Cassandra API)
        
    * Azure Table Storage
        
    * Azure Queue Storage
        

### Unstructured data

* Encompasses data that has no designated structure to it
    
* There are no restrictions on the kinds of data it can hold.
    
    * e.g. PDF document, a JPG image, a JSON file, video content, etc
        
* 💡More prominent as businesses try to tap into new data sources.
    
* Azure services:
    
    * Azure Blob Storage
        
    * Azure File Storage
        
    * Azure Data Lake Storage
        
    * Azure Disk Storage
        

## Azure Storage

* Includes disks attached to virtual machines, file shares, databases
    
* They can expand & shrink necessarily
    
* Common characteristics:
    
    * **Durable** and highly available with redundancy and replication.
        
    * **Secure** through automatic encryption and role-based access control.
        
    * **Scalable** with virtually unlimited storage.
        
    * **Managed**, handling maintenance and any critical problems for you.
        
    * **Accessible** from anywhere in the world over HTTP or HTTPS.
        

### Azure Blob Storage

* Also known as **Azure blobs**
    
* Good for very large objects, such as video files or bitmaps
    
* Unstructured, meaning that there are no restrictions on the kinds of data it can hold.
    
* Can manage thousands of simultaneous uploads, massive amounts of video data, constantly growing log files, and can be reached from anywhere with an internet connection.
    
* Lets you
    
    * Stream large video or audio files directly to the user's browser from anywhere in the world.
        
    * Send large volumes of data directly to the browser.
        
* 💡 Also used to store data for backup, disaster recovery, and archiving.
    
* 📝 Ability to store up to 8 TB of data for virtual machines (VM disks)
    

#### Storage tiers

1. **Hot storage tier**: optimized for storing data that is accessed frequently.
    
2. **Cool storage tier**: optimized for data that are infrequently accessed and stored for at least 30 days.
    
3. **Archive storage tier**: for data that are rarely accessed and stored for at least 180 days with flexible latency requirements.
    

### Azure Disk Storage

* Also known as **Azure disks**
    
* Provides disks for virtual machines, applications, and other services to access and use as they need.
    
* In the background they are page-blobs in a blob storage
    
* Allows data to be persistently stored and accessed from an attached virtual hard disk.
    
* Disks can be managed or unmanaged by Azure, and therefore managed and configured by the user.
    
* 💡 Use-case examples: Lift and shift
    
    * Storing data that is not required to be accessed from outside the virtual machine to which the disk is attached.
        
* Different sizes and performance levels
    
    * Solid-state drives (SSDs)
        
    * Hard disk drives (HDDs)
        
* 💡 Use standard SSD and HDD disks for less critical workloads
    
    * Premium SSD disks for mission-critical production applications.
        
* Durable: ZERO% annualized failure rate.
    

### Azure Data Lake Storage

* 📝 Allows you to perform analytics on your data usage and prepare reports.
    
* Stores both structured and unstructured data.
    
* Combines the scalability and cost benefits of object storage with the reliability and performance of the Big Data file system capabilities.
    
* Supports batch queries, interactive queries, real-time analytics, machine learning, and being a data warehouse.
    

### Azure File Storage

* Also known as **Azure files**
    
* File shares that you can access and manage like a file server
    
* Fully managed file shares in the cloud that are accessible via the industry standard Server Message Block (SMB) protocol.
    
* Ensures the data is encrypted at rest and in transit.
    
* Can be mounted concurrently by cloud or on-premises Windows, Linux, and macOS.
    
* 📝 Any number of Azure virtual machines or roles can mount and access the file storage share simultaneously.
    
* 💡 Good to share files anywhere in the world, diagnostic data, or application data sharing.
    

### Azure Queue Storage

* A data store for queuing and reliably delivering messages between applications
    
* 💡 Helps build flexible applications and separate functions for better durability across large workloads
    
    * When application components are decoupled, they can scale independently
        
    * Provides asynchronous message queueing for communication between application components
        
* Typically, there are one or more sender components and one or more receiver components.
    
    * Sender components add messages to the queue
        
    * Receiver components retrieve messages from the front of the queue for processing
        
* 💡 Use-case examples:
    
    * Create a backlog of work and to pass messages between different Azure web servers.
        
    * Distribute load among different web servers/infrastructure and to manage bursts of traffic.
        
    * Build resilience against component failure when multiple users access your data at the same time.
        

### Azure Table Storage

* NoSQL data store
    
* Schema-less design
    

### Encryption Types

#### Azure Storage Service Encryption (SSE)

* For data at rest helps you secure your data.
    
* It encrypts the data before storing it and decrypts the data before returning it.
    
* Encryption & decryption are transparent to the user.
    

#### Client-side encryption

* Data is already encrypted by the client libraries.
    
* Azure stores the data in the encrypted state at rest, which is then decrypted during retrieval.
    

### Replication

* Set up when you create a storage account
    
* Ensures that your data is durable and always available
    
* Provides regional and geographic replications
    
    * Protects data against natural disasters and other local disasters like fire or flooding.
        

### On-premises storage vs Azure data storage

#### Why migrate to cloud

* **Cost effectiveness**
    
    * Pay-as-you go
        
    * No dedicated hardware to be purchased, installed, configured and maintained. = no up-front expense (or capital cost).
        
    * Scalable: No need to have idle hardware
        
* **Reliability**
    
    * Managed data backup, load balancing, disaster recovery, and data replication as services to ensure data safety and high availability.
        
* **Storage types**
    
    * On-premises =&gt; often requires numerous servers and administrative tools for each storage type.
        
    * Azure has different storage options for each part of your solution.
        
* **Agility**
    
    * Requirements and technologies change: No need to reprovisioning & deployment of new infrastructure.
        
    * Create new services in minutes = change storage back-ends quickly without needing a significant hardware investment.
        

#### Comparison

| Needs | On-premises | Azure data storage |
| --- | --- | --- |
| **Compliance and security** | Dedicated servers required for privacy and security | Client-side encryption and encryption at rest |
| **Store structured and unstructured data** | Additional IT resources with dedicated servers required | Azure Data Lake and portal analyzes and manages all types of data |
| **Replication and high availability** | More resources, licensing, and servers required | Built-in replication and redundancy features available |
| **Application sharing and access to shared resources** | File sharing requires additional administration resources | File sharing options available without additional license |
| **Relational data storage** | Needs a database server with database admin role | Offers database-as-a-service options |
| **Distributed storage and data access** | Expensive storage, networking, and compute resources needed | Azure Cosmos DB provides distributed access |
| **Messaging and load balancing** | Hardware redundancy impacts budget and resources | Azure Queue provides effective load balancing |
| **Tiered storage** | Management of tiered storage needs technology and labor skill set | Azure offers automated tiered storage of data |
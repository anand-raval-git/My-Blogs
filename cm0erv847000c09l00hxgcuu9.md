---
title: "Day 30 Task:🚀 Understanding Kubernetes Architecture 🛠️"
seoTitle: "Kubernetes Architecture Overview"
seoDescription: "Learn about Kubernetes, its benefits, key components, and architecture for managing containerized applications in this comprehensive guide"
datePublished: 2024-08-29T04:15:43.063Z
cuid: cm0erv847000c09l00hxgcuu9
slug: day-30-task-understanding-kubernetes-architecture
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1724904880603/36582df3-5fbc-400e-a47e-5776421bc603.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1724904910800/13654b72-f398-44cd-b26f-bec7c532f6e2.png
tags: kubernetes, devops, kubernetes-container, 90daysofdevops, trainwithshubham

---

## Kubernetes Overview

With the widespread adoption of [containers](https://cloud.google.com/containers) among organizations, Kubernetes, the container-centric management software, has become a standard to deploy and operate containerized applications and is one of the most important parts of DevOps.

Originally developed at Google and released as open-source in 2014. Kubernetes builds on 15 years of running Google's containerized workloads and the valuable contributions from the open-source community. Inspired by Google’s internal cluster management system, [Borg](https://research.google.com/pubs/pub43438.html),

## Tasks

1. What is Kubernetes? Write in your own words and why do we call it k8s?
    
    Kubernetes is an open-source platform designed to automate the deployment, scaling, and operation of containerized applications. It helps manage clusters of containers, ensuring that they run efficiently and reliably. The term "k8s" is a shorthand notation where the "8" represents the eight letters between the "K" and the "s" in "Kubernetes." This abbreviation is commonly used in the tech community to simplify communication.
    
2. What are the benefits of using k8s?
    
    The benefits of using Kubernetes (k8s) include:
    
    1. **Automated Deployment and Scaling**: Kubernetes automates the deployment and scaling of containerized applications, making it easier to manage large-scale applications.
        
    2. **Self-Healing**: Kubernetes can automatically restart failed containers, replace and reschedule them, and kill containers that don't respond to user-defined health checks.
        
    3. **Service Discovery and Load Balancing**: Kubernetes can expose a container using the DNS name or their own IP address and can load balance across them.
        
    4. **Storage Orchestration**: Kubernetes allows you to automatically mount the storage system of your choice, such as local storage, public cloud providers, and more.
        
    5. **Secret and Configuration Management**: Kubernetes can manage and deploy secrets and application configuration without rebuilding your container images, and without exposing secrets in your stack configuration.
        
    6. **Automated Rollouts and Rollbacks**: Kubernetes can progressively roll out changes to your application or its configuration, while monitoring application health to ensure it doesn’t kill all your instances at the same time.
        
    7. **Resource Optimization**: Kubernetes can efficiently manage resources for containerized applications, ensuring optimal use of hardware resources.
        
    8. **Extensibility and Modularity**: Kubernetes is highly extensible and modular, allowing you to integrate with various third-party tools and services.
        
    9. **Multi-Cloud and Hybrid Cloud Support**: Kubernetes can run on various environments, including on-premises, public clouds, and hybrid cloud setups, providing flexibility and avoiding vendor lock-in.
        
3. Explain the architecture of Kubernetes
    
    Kubernetes architecture can be understood as a system that helps manage and run applications in containers. Think of it as a manager that ensures everything runs smoothly and efficiently
    
    1. **Cluster**: A Kubernetes cluster is a set of machines (computers) (group of servers)that work together. There are two main types of machines in a cluster: the **Control Plane**(Master node)and the **Worker Nodes**.
        
    2. **Control Plane**: This is the brain of the Kubernetes cluster. It makes decisions about the cluster, like scheduling (deciding which machine should run a new container) and responding to cluster events (like when a container crashes).
        
    3. **Worker Nodes**: These are the machines that actually run the applications. Each worker node has a set of tools to manage the containers.
        
        ### **Key Components in the Control Plane (Master node)**
        
        1. **API Server**: This is the front end of the control plane. It exposes the Kubernetes API, which is used by users and other components to interact with the cluster.
            
        2. **etcd**: This is a key-value store that stores all the data about the cluster. It’s like a database that keeps track of the state of the cluster.
            
        3. **Controller Manager**: This component ensures that the cluster is in the desired state. For example, if a container crashes, the controller manager will notice and start a new one.
            
        4. **Scheduler**: This component decides which worker node should run a new container based on resource availability and other factors
            
    
    ### **Key Components in the Worker Nodes**
    
    1. **Kubelet**: This is an agent that runs on each worker node. It ensures that containers are running in a Pod (a group of one or more containers).
        
    2. **Kube-proxy**: This component maintains network rules on each worker node. It allows communication between different parts of the cluster.
        
    3. **Container Runtime**: This is the software that actually runs the containers. Examples include Docker and containerd.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724904187423/8ca70e6b-ab63-4884-889e-b0cee543cbf3.png align="center")
        
        ### **Example**
        
        Imagine you have an online store application. You want to make sure it’s always available and can handle lots of customers. Here’s how Kubernetes helps:
        
        1. **Deployment**: You tell Kubernetes to run 5 copies of your online store application. Kubernetes will schedule these copies on different worker nodes.
            
        2. **Scaling**: If more customers visit your store, you can tell Kubernetes to run more copies of your application. Kubernetes will automatically find the best worker nodes to run these new copies.
            
        3. **Self-Healing**: If one of the copies crashes, Kubernetes will automatically start a new one to replace it.
            
        4. **Load Balancing**: Kubernetes will distribute customer requests evenly across all copies of your application, ensuring no single copy gets overwhelmed.
            
        5. Pods :-A **Pod** is the smallest and simplest Kubernetes object. It represents a single instance of a running process in your cluster. A Pod can contain one or more containers that share storage, network, and a specification for how to run the containers.
            
        
        By managing these tasks, Kubernetes ensures your application is always running smoothly and can handle changes in demand.
        
4. What is Control Plane?
    
    Master node known as control plane in k8s The Control Plane in Kubernetes is like the brain of the system. It’s responsible for making all the important decisions to keep everything running smoothly. Here’s a simple way to understand it:
    
    ### What is the Control Plane?
    
    The Control Plane is a set of components that manage the overall state of the Kubernetes cluster. It makes decisions about what needs to be done and ensures that the desired state of the system is maintained.
    
    ### Key Components of the Control Plane
    
    1. **API Server**: Think of this as the receptionist. It’s the main entry point for all the commands and requests. When you or other parts of the system want to do something, they talk to the API Server.
        
    2. **etcd**: This is like the memory of the system. It stores all the information about the state of the cluster, such as which applications are running and where they are running.
        
    3. **Controller Manager**: Imagine this as a manager who keeps an eye on everything. If something goes wrong, like if an application crashes, the Controller Manager notices and takes action to fix it.
        
    4. **Scheduler**: This is like a dispatcher. It decides which worker node (computer) should run a new application based on available resources and other factors.
        
    
    ### Example
    
    Imagine you have a garden with several plants, and you want to make sure they are always healthy and growing well. Here’s how the Control Plane helps:
    
    1. **API Server**: You tell the API Server that you want to plant 5 new flowers. The API Server takes your request and starts the process.
        
    2. **etcd**: The etcd component keeps a record of all the plants in your garden, including the new flowers you want to plant.
        
    3. **Controller Manager**: If one of your flowers starts wilting, the Controller Manager notices and takes action, like watering the plant or replacing it with a new one.
        
    4. **Scheduler**: The Scheduler decides the best spots in your garden to plant the new flowers, ensuring they have enough sunlight and space to grow.
        
    
    By managing these tasks, the Control Plane ensures your garden (or in the case of Kubernetes, your applications) is always in the best possible state and can handle any changes or issues that arise.
    
5. Write the difference between kubectl and kubelets.
    
    The difference between `kubectl` and `kubelet` is as follows:
    
    ### kubectl
    
    * **Purpose**: `kubectl` is a command-line tool used to interact with the Kubernetes API server. It allows users to manage and control Kubernetes clusters.
        
    * **Functionality**: With `kubectl`, you can perform various operations such as deploying applications, inspecting and managing cluster resources, and viewing logs.
        
    * **Usage**: It is used by administrators and developers to send commands to the Kubernetes cluster. For example, you can use `kubectl` to create, update, delete, and get the status of resources like pods, services, and deployments.
        
    
    ### kubelet
    
    * **Purpose**: `kubelet` is an agent that runs on each worker node in the Kubernetes cluster. It ensures that containers are running in a Pod as specified by the control plane.
        
    * **Functionality**: The `kubelet` monitors the state of the pods on its node and reports this information back to the control plane. It also takes instructions from the control plane to start, stop, or manage containers.
        
    * **Usage**: It is used by the Kubernetes system itself to maintain the desired state of the pods on each node. The `kubelet` continuously checks the health of the pods and ensures they are running as expected.
        
    
    In summary, `kubectl` is a tool for users to interact with the Kubernetes cluster, while `kubelet` is a component that runs on each node to ensure the containers are running as intended.
    
6. Explain the role of the API server.
    
    The API server in Kubernetes acts as the central communication hub for the entire cluster. It is the main entry point for all administrative tasks and interactions with the cluster. Here’s a simple explanation of its role:
    
    ### Role of the API Server
    
    1. **Central Communication Point**: The API server is like the receptionist of the Kubernetes cluster. It receives all the requests from users, administrators, and other components within the cluster. These requests can include actions like deploying applications, scaling services, or retrieving the status of resources.
        
    2. **Exposes Kubernetes API**: The API server exposes the Kubernetes API, which is a set of endpoints that allow users and components to interact with the cluster. This API is used to perform various operations such as creating, updating, deleting, and querying Kubernetes resources like pods, services, and deployments.
        
    3. **Authentication and Authorization**: The API server handles authentication and authorization, ensuring that only authorized users and components can perform actions on the cluster. It verifies the identity of the requester and checks their permissions before allowing any operation.
        
    4. **Validation and Admission Control**: When a request is received, the API server validates it to ensure it is well-formed and adheres to the required specifications. It also runs admission controllers, which are plugins that can enforce policies on the requests, such as resource quotas or security policies.
        
    5. **State Management**: The API server interacts with etcd, the key-value store that holds the cluster's state. It reads from and writes to etcd to keep track of the current state of the cluster, ensuring that the desired state specified by the users matches the actual state of the cluster.
        
    
    ### Example
    
    Imagine you want to deploy a new version of your application in the Kubernetes cluster. Here’s how the API server helps:
    
    1. **Submit Request**: You use `kubectl` to submit a request to deploy the new version of your application. This request is sent to the API server.
        
    2. **Authentication and Authorization**: The API server checks your identity and permissions to ensure you are allowed to deploy applications.
        
    3. **Validation**: The API server validates your request to make sure it is correctly formatted and adheres to the cluster’s policies.
        
    4. **State Update**: The API server updates the desired state in etcd to reflect the new version of your application.
        
    5. **Communication**: The API server communicates with other components, like the scheduler and controller manager, to ensure the new version of your application is deployed and running as expected.
        
    
    By managing these tasks, the API server ensures that all interactions with the Kubernetes cluster are handled efficiently and securely.
    

Thankyou for reading !!!!
---
title: "Day 33 Task: Working with Namespaces and Services in Kubernetes"
seoTitle: "Namespaces & Services in Kubernetes"
seoDescription: "Learn how to manage Namespaces and Services in Kubernetes to create isolated environments and expose Pods to the network"
datePublished: 2024-09-09T09:12:09.215Z
cuid: cm0usatbz001s09ml7l13biou
slug: day-33-task-working-with-namespaces-and-services-in-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1725873095409/dd44e940-f27e-4538-90ce-ddd966af4a7c.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1725873118574/0c2d6802-2338-460d-bf35-07f7f6b6e061.png
tags: kubernetes, devops, minikube, 90daysofdevops, trainwithshubham

---

## What are Namespaces and Services in k8s

In Kubernetes, Namespaces are used to create isolated environments for resources. Each Namespace is like a separate cluster within the same physical cluster. Namespaces are intended for use in environments with many users spread across multiple teams, or projects. Services are used to expose your Pods and Deployments to the network. Read more about Namespace [Here](https://kubernetes.io/docs/concepts/workloads/pods/user-namespaces/)

# Today's task:

## Task 1:

* Create a Namespace for your Deployment
    
* Use the command `kubectl create namespace <namespace-name>` to create a Namespace
    
* Update the deployment.yml file to include the Namespace
    
* Apply the updated deployment using the command: `kubectl apply -f deployment.yml -n <namespace-name>`
    
* Verify that the Namespace has been created by checking the status of the Namespaces in your cluster.
    
    Let's start
    
    1. **Create a Namespace:** Use the command below to create a namespace:
        
        ```bash
        kubectl create namespace <namespace-name>
        ```
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725862917049/3f6d1df1-a957-4a0d-9841-649cef010850.png align="center")
        
    2. Verify the creation of the namespace by listing all namespaces:
        
        ```bash
        kubectl get namespace
        ```
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725862953616/def76ad9-9291-4dd5-bb7b-82fca8c08ba4.png align="center")
        
    3. **Update the Deployment YAML file:** Update your `deployment.yml` file to include the namespace:
        
        ```bash
        apiVersion: apps/v1
        kind: Deployment
        metadata:
          name: my-app-deployment
          namespace: deploy
        spec:
          replicas: 2
          selector:
            matchLabels:
              app: my-app
          template:
            metadata:
              labels:
                app: my-app
            spec:
              containers:
                - name: my-app
                  image: anandraval12/django-todo-app:latest
                  ports:
                    - containerPort: 8000
        ```
        
    4. **Apply the Updated Deployment:** Apply the deployment using the following command:
        
        ```bash
        kubectl apply -f deployment.yml -n <namespace-name>
        ```
        
        or
        
        assign namespace as default and you can use further command without namespace
        
        ```bash
        kubectl config set-context --current --namespace=<name space name>
        ```
        
        ```bash
        kubectl apply -f deployment.yml
        ```
        
    5. **Verify the Namespace:** Check the status of the namespaces to ensure the new namespace is active:
        
        ```bash
        kubectl get namespaces
        ```
        
    
    ### Task 2: Read about Services, Load Balancing, and Networking in Kubernetes
    
    In Kubernetes, a Service is an abstraction that defines a logical set of Pods and a policy by which to access them. Services provide a stable IP address and DNS name, enabling reliable communication between different parts of an application. They also facilitate load balancing traffic across the Pods, ensuring even distribution of network traffic.
    
    Read about Services, Load Balancing, and Networking in Kubernetes. Refer official documentation of kubernetes [Link](https://kubernetes.io/docs/concepts/services-networking/)
    
    ### Let's do task 2
    
    * Read about Services, Load Balancing, and Networking in Kubernetes. Refer official documentation of kubernetes [Li](https://kubernetes.io/docs/concepts/services-networking/)[nk](https://kubernetes.io/docs/concepts/services-networking/)
        
        ### Key Points:
        
        1. **Pod Communication**: Each pod in Kubernetes gets a unique IP address, allowing direct communication between pods without the need for NAT (Network Address Translation), even if the pods are on different nodes.
            
        2. **Services**: A **Service** in Kubernetes allows you to expose a set of pods behind a stable, single IP or DNS name, enabling load balancing and internal/external access to your applications.
            
        3. **Load Balancing**: Services automatically handle load balancing between pods to distribute traffic evenly.
            
        4. **Service Types**: Different types of services (ClusterIP, NodePort, LoadBalancer) are available depending on whether you want the service to be accessible within the cluster or from outside.
            
        5. **Ingress**: Ingress is used to expose HTTP/HTTPS services with routing rules (like URL paths) and allows for more fine-grained traffic control.
            
        6. **Network Policies**: You can use Network Policies to control traffic flow between pods or between pods and external services at the IP address and port level.
            
        
        For more details, you can visit the official documentation of Kubernetes here: [Kubernetes Networking and Services Documentation](https://kubernetes.io/docs/concepts/services-networking/).
        

Thankyou for reading !!!!!!
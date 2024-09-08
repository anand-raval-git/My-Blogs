---
title: "Day 32 Task: Launching your Kubernetes Cluster with Deployment"
seoTitle: "Deploy Kubernetes Cluster: Day 32 Guide"
seoDescription: "Learn to launch your Kubernetes cluster with Deployment and implement auto-healing and auto-scaling for a sample todo-app"
datePublished: Sun Sep 08 2024 17:31:58 GMT+0000 (Coordinated Universal Time)
cuid: cm0tupqq2001709kyf63r97on
slug: day-32-task-launching-your-kubernetes-cluster-with-deployment
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1725801135912/96ca53a9-6a94-4ea7-8890-b6b7c79f8999.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1725801165306/6aa89151-4a5b-4ffd-97b1-dccc4f5e64b9.png
tags: kubernetes, devops, minikube, 90daysofdevops, trainwithshubham

---

## What is Deployment in k8s

A Deployment provides a configuration for updates for Pods and ReplicaSets.

You describe a desired state in a Deployment, and the Deployment Controller changes the actual state to the desired state at a controlled rate. You can define Deployments to create new replicas for scaling, or to remove existing Deployments and adopt all their resources with new Deployments.

## Task-1:

**Create one Deployment file to deploy a sample todo-app on K8s using "Auto-healing" and "Auto-Scaling" feature**

* add a deployment.yml file (sample is kept in the folder for your reference)
    
* apply the deployment to your k8s (minikube) cluster by command `kubectl apply -f deployment.yml`
    

### **Deploy a Sample todo-app on Kubernetes**

Let’s apply our Deployment configuration:

1. **Clone the repository** for your application:
    
    ```bash
     git clone https://github.com/anand-raval-git/django-todo.git
    ```
    
2. **Create a Docker image** from your Dockerfile:
    
    ```bash
    # Dockerfile
    FROM python:3.11
    
    WORKDIR /data
    
    RUN pip install django==3.2
    
    COPY . .
    
    RUN python manage.py migrate
    
    EXPOSE 8000
    
    CMD ["python","manage.py","runserver","0.0.0.0:8000"]
    ```
    
    ```bash
    docker build -t anandraval12/django-todo-app .
    ```
    
3. **Push the Docker image** to DockerHub:
    
    ```bash
    docker login
    docker push anandraval12/django-todo-app:latest
    
    ```
    
4. **Create the Deployment YAML file**
    
    Create `deployment.yml` file for deploying a todo-app:
    
    ```bash
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: django-todo-deployment
      namespace: default
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: django-todo
      template:
        metadata:
          labels:
            app: django-todo
        spec:
          containers:
          - name: django-todo
            image: anandraval12/django-todo-app:latest
            ports:
            - containerPort: 8000
    ```
    
5. **Apply the Deployment** to your Kubernetes (Minikube) cluster:
    
    ```bash
     kubectl apply -f deployment.yml
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725800909415/393c1bbf-82ec-44b2-85fe-778436f51799.png align="center")
    
6. **Verify the Pods** are running:
    
    ```bash
     kubectl get pods
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725800948505/5be1ba1d-e2a7-4c8d-b1eb-7c6a95bbe857.png align="center")
    
7. **Test the application** on the worker node:
    
    ```bash
     docker ps
     sudo docker exec -it <docker-container> bash
     curl -L http://127.0.0.1:8000
    ```
    
8. **Test Auto-healing** by deleting a Pod and ensuring a new one is created:
    
    ```bash
    kubectl delete pod <pod-name>
    ```
    
9. **Delete the Deployment** when done:
    
    ```bash
    kubectl delete -f deployment.yml
    ```
    

Thankyou for reading !!!!!!
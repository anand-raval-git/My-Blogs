---
title: "Day 31 Task: Launching Your First Kubernetes Cluster with Nginx Running 🌐"
seoTitle: "Launch Kubernetes Cluster with Nginx"
seoDescription: "Learn to launch your first Kubernetes cluster with Minikube and create your first Pod in a simplified environment"
datePublished: Sat Sep 07 2024 18:51:44 GMT+0000 (Coordinated Universal Time)
cuid: cm0si4gqu003g09mgelc54w0x
slug: day-31-task-launching-your-first-kubernetes-cluster-with-nginx-running
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1725735068757/240b0cb9-fdd7-4fab-8052-98177dcbb809.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1725735092761/ad64b8f8-2678-421b-857e-237bdde236df.png
tags: kubernetes, devops, minikube, 90daysofdevops, trainwithshubham

---

## What about doing some hands-on now?

Let's read about minikube and implement *k8s* in our local machine

1. ### **What is minikube?**
    

*Ans*:- Minikube is a tool which quickly sets up a local Kubernetes cluster on macOS, Linux, and Windows. It can deploy as a VM, a container, or on bare-metal.

Minikube is a pared-down version of Kubernetes that gives you all the benefits of Kubernetes with a lot less effort.

This makes it an interesting option for users who are new to containers, and also for projects in the world of edge computing and the Internet of Things.

2. ### **Features of minikube**
    

*Ans* :-

(a) Supports the latest Kubernetes release (+6 previous minor versions)

(b) Cross-platform (Linux, macOS, Windows)

(c) Deploy as a VM, a container, or on bare-metal

(d) Multiple container runtimes (CRI-O, containerd, docker)

(e) Direct API endpoint for blazing fast image load and build

(f) Advanced features such as LoadBalancer, filesystem mounts, FeatureGates, and network policy

(g) Addons for easily installed Kubernetes applications

(h) Supports common CI environments

### • **What is difference between k8s and minikube ?**

* **Kubernetes (k8s)**: Kubernetes is a powerful open-source platform designed to automate deploying, scaling, and operating application containers. It is typically used to manage clusters of nodes in production environments, which can span multiple machines and data centers.
    

**Minikube**: Minikube is a tool that makes it easy to run Kubernetes locally. It sets up a single-node Kubernetes cluster inside a virtual machine (VM) on your local machine. Minikube is primarily used for development and testing purposes, providing a simplified environment to learn and experiment with Kubernetes , in short minikube is a docker container.

> Note :- Minikube is work under dind (docker in docker) principal

## Let's understand the concept **pod**

*Ans:-*

Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.

A Pod (as in a pod of whales or pea pod) is a group of one or more containers, with shared storage and network resources, and a specification for how to run the containers. A Pod's contents are always co-located and co-scheduled, and run in a shared context. A Pod models an application-specific "logical host": it contains one or more application containers which are relatively tightly coupled.

You can read more about pod from [here](https://kubernetes.io/docs/concepts/workloads/pods/) .

## Task-01:

## Install minikube on your local

For installation, you can Visit [this page](https://minikube.sigs.k8s.io/docs/start/).

If you want to try an alternative way, you can check [this](https://k8s-docs.netlify.app/en/docs/tasks/tools/install-minikube/).

### **There are some types of Installation of K8s**

1. **Minikube**: Docker Inside Docker (DIND) - Least used in production, easiest to set up.
    
2. **Kubeadm**: Bare-metal tool - Used in production, intermediate setup.
    
3. **KIND**: Kubernetes in Docker
    
4. **Managed K8s Cluster**:
    
    * AWS: EKS (Elastic Kubernetes Service)
        
    * Azure: AKS (Azure Kubernetes Service)
        
    * GCP: GKE (Google Kubernetes Engine)
        

### Installation of Minikube

1. **Launch an AWS instance** (t2-medium recommended cause of Minikube need atleast 2 cpu and 4gb ram to run)
    
2. Update System Packages:
    
    Update your package lists to make sure you are getting the latest version and dependencies.
    
    ```bash
    sudo apt update
    ```
    
3. **Install necessary packages**:
    
    Install some basic required packages.
    
    ```bash
    sudo apt install -y curl wget apt-transport-https
    ```
    
4. **Install and start Docker**:
    
    ```bash
    sudo apt install -y docker.io
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725732296697/34077f28-ef0d-4be7-8de4-bb88d465d5e1.png align="center")
    
5. Give Permission to docker
    
    ```bash
    sudo usermod -aG docker $USER
    sudo systemctl start docker
    sudo systemctl enable docker
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725732328431/f39d909e-8d12-4d8d-9fe0-5ad7d78b91d1.png align="center")
    
6. If you getting error when run docker ps command then run below command before docker ps
    
    ```bash
    sudo chmod 666 /var/run/docker.sock
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725732463856/00e770fe-0aca-4c57-973c-a04a404fe7f7.png align="center")
    
7. Install Minikube
    
    First, download the Minikube binary using `curl`:
    
    ```bash
    curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    ```
    
8. Make it executable and move it into your path:
    
    ```bash
    chmod +x minikube
    sudo mv minikube /usr/local/bin/
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725732878322/767cb37d-dd70-4ebe-880f-bebb0e3367ec.png align="center")
    
9. **Now install kubectl**:
    
    ```bash
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
    ```
    
10. Make it executable and move it into your path:
    
    ```bash
    chmod +x kubectl
    sudo mv kubectl /usr/local/bin/
    ```
    
11. **Start Minikube**:
    
    This command will start a single-node Kubernetes cluster inside a Docker container.
    
    ```bash
    minikube start --driver=docker --vm=true
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725732962484/823105c5-86ec-4f11-af8e-b8f36c988823.png align="center")

1. Check Cluster Status
    
    Check the cluster status with:
    
    ```bash
    minikube status
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725732992468/37ed41d3-198e-44a6-8913-c533e62c205d.png align="center")
    
2. You can also use `kubectl` to interact with your cluster:
    
    ```bash
    kubectl get nodes
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725733032634/35a651c3-6a12-4bd4-9de0-6435daecc19e.png align="center")
    
3. Stop Minikube
    
    When you are done, you can stop the Minikube cluster with:
    
    ```bash
    minikube stop
    ```
    
4. Optional: Delete Minikube Cluster
    
    If you wish to delete the Minikube cluster entirely, you can do so with:
    
    ```bash
    minikube delete
    ```
    
    ## Task-02:
    

### Create Your First Pod on Kubernetes through Minikube

1. **Start Minikube** (if not running):
    
    ```bash
    minikube start
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725733107477/bb5181e0-aeea-4307-bd08-103eef3dab34.png align="center")
    
2. **Create a Pod YAML Manifest**:
    
    ```bash
    # first-pod.yml
    apiVersion: v1
    kind: Pod
    metadata:
      name: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725734243438/3b460b2e-794a-4d55-bc09-3f4d803051e5.png align="center")
    
3. **Create the pod**:
    
    ```bash
    kubectl apply -f first-pod.yml
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725734285667/884d8884-b517-484d-aa20-212473f80634.png align="center")
    
4. **Check pod status**:
    
    ```bash
    kubectl get pods
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725734352380/e056a4b6-379e-47bb-9511-67427c1b0f89.png align="center")
    

Thankyou for reading !!!!!
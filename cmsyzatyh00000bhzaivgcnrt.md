---
title: "AWS Day 43: Scaling and Managing Kubernetes Clusters with Amazon EKS
"
seoTitle: "Scaling and Managing Kubernetes Clusters with Amazon EKS"
seoDescription: "Learn how to create a private Amazon EKS cluster with Kubernetes 1.36, IAM roles, multi-AZ networking, and EKS Auto Mode disabled."
datePublished: 2026-08-18T18:10:57.490Z
cuid: cmsyzatyh00000bhzaivgcnrt
slug: aws-day-43-scaling-and-managing-kubernetes-clusters-with-amazon-eks
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/789b4632-4315-43ec-a9a2-a1a4f19f911a.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/3fec27bf-d958-49d3-b592-0a3fd9ef6726.png
tags: aws, k8s, eks, kodekloud, anand-raval

---

As part of my **KodeKloud 100 Days of Cloud** journey, Day 43 focused on creating and configuring an **Amazon Elastic Kubernetes Service (EKS)** cluster with a strong focus on security, availability, and controlled cluster configuration.

For this task, the Nautilus DevOps team needed an EKS cluster for a new Kubernetes-based application. The cluster had to use the latest stable Kubernetes version available in the lab, remain private from the public internet, and be deployed across multiple Availability Zones for better availability.

## What is Amazon EKS?

**Amazon Elastic Kubernetes Service (EKS)** is a managed Kubernetes service provided by AWS.

With EKS, AWS manages the Kubernetes control plane infrastructure, while we can choose how the worker compute is provisioned using options such as:

*   Managed Node Groups
    
*   Self-managed nodes
    
*   AWS Fargate
    
*   EKS Auto Mode
    

EKS is commonly used for running containerized applications that require Kubernetes orchestration, automated scaling, service discovery, rolling deployments, and high availability.

In this task, the focus was on creating the EKS control plane with a secure network configuration rather than deploying application workloads.

## Step 1: Create the EKS Cluster IAM Role

The first step was creating the IAM role required by the EKS control plane.

I opened:

**AWS Console → IAM → Roles → Create role**

For the trusted entity, I selected:

**Trusted entity type:** AWS service

Then selected:

**Service:** EKS

For the use case, I selected:

**EKS - Cluster**

This creates a trust relationship allowing the EKS service to assume the role.

I named the role:

```plaintext
eksClusterRole
```

The trust policy generated for the role allows the EKS service to assume the role:

```plaintext
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "eks.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

The cluster IAM role is used by the EKS control plane to interact with AWS resources required for cluster management.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/3db591bf-6456-4bec-87b6-efff9a5032aa.png align="center")

## Step 2: Start Creating the EKS Cluster

Next, I opened the **Amazon EKS** console and selected:

**Create cluster**

AWS provides different configuration approaches. For this task, I selected:

**Custom configuration**

I did not use the quick configuration because the task specifically required controlling the cluster networking and EKS Auto Mode settings.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/acf5af29-db5a-4a42-b1c3-50de10131516.png align="center")

## Step 3: Disable EKS Auto Mode

Under the EKS Auto Mode section, I made sure that:

**Use EKS Auto Mode = Disabled**

EKS Auto Mode can automate several infrastructure operations, including provisioning compute resources and managing parts of the cluster infrastructure.

For this lab, Auto Mode was not required because the objective was to create the cluster with explicit configuration choices.

Keeping Auto Mode disabled also makes it clearer which components are being configured manually.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/78e0e635-1585-4de6-bf81-81ed01d01bee.png align="center")

## Step 4: Configure the Cluster Name

Under **Cluster configuration**, I entered:

```plaintext
xfusion-eks
```

The cluster name is important because it is used later with AWS CLI and Kubernetes tooling.

For example:

```plaintext
aws eks describe-cluster \
  --name xfusion-eks \
  --region us-east-1
```

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/e4179ca2-99d6-4db3-bee7-535673b93183.png align="center")

## Step 5: Select the Cluster IAM Role

For **Cluster IAM role**, I selected the role created earlier:

```plaintext
eksClusterRole
```

This connects the EKS control plane with the IAM permissions required to manage AWS resources on behalf of the cluster.

At this point, the basic cluster configuration was:

```plaintext
Cluster Name: xfusion-eks
IAM Role: eksClusterRole
EKS Auto Mode: Disabled
```

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/ced98c78-9114-47e9-baeb-d3ae0fb1eb4e.png align="center")

## Step 6: Select the Kubernetes Version

The task required using the latest stable Kubernetes version available in the environment.

During this lab, the AWS console provided:

```plaintext
Kubernetes Version: 1.36
```

I selected Kubernetes **1.36**.

Keeping the Kubernetes control plane on a supported and current version is important because newer Kubernetes releases provide updated features, fixes, and security improvements.

However, in a production environment, I would still verify application compatibility with the target Kubernetes version before upgrading.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/7bebb565-2f2d-43ea-93af-1e8453611cc4.png align="center")

## Step 7: Configure Private Cluster Endpoint

This was one of the most important settings in the entire task.

Under **Cluster endpoint access**, AWS provides three options:

*   Public
    
*   Public and private
    
*   Private
    

I selected:

```plaintext
Private
```

With a private endpoint, the Kubernetes API server is accessible through the VPC rather than directly from the public internet.

This reduces the public attack surface of the Kubernetes control plane.

The configuration was:

```plaintext
Cluster endpoint access: Private
```

This is particularly useful for environments where Kubernetes administration should happen from controlled network locations such as:

*   Bastion hosts
    
*   VPN-connected networks
    
*   AWS Systems Manager-based administration
    
*   Corporate networks connected through AWS networking
    
*   Internal CI/CD infrastructure
    

One important operational consideration is that administrators must have network connectivity to the VPC in order to communicate with a private Kubernetes API endpoint.

Useful AWS EKS Commands

For future reference, these are some useful commands from this lab:
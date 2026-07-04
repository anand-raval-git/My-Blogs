---
title: "AWS Day 28: Creating a Private Amazon ECR Repository and Pushing a Docker Image"
seoTitle: "WS Day 28: Create a Private Amazon ECR Repository Docker "
seoDescription: "Learn how to create a private Amazon ECR repository, build a Docker image from a Dockerfile, authenticate Docker using AWS CLI, and push the image ecr"
datePublished: 2026-07-04T06:26:09.199Z
cuid: cmr5zb44400000akl7kve7cc4
slug: aws-day-28-creating-a-private-amazon-ecr-repository-and-pushing-a-docker-image
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/9e9435b4-4b11-4464-810a-37473ca644ce.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/fea2af05-09ed-4f0b-bfec-85a4937737da.png
tags: aws, kodekloud, aws-ecr, kodekloudengineer, anand-raval

---

## Introduction

During Day 28 of the KodeKloud 100 Days of Cloud Challenge, I worked with **Amazon Elastic Container Registry (Amazon ECR)**, AWS's fully managed container image registry.

When deploying containerized applications on services like Amazon ECS, Amazon EKS, or AWS Fargate, Docker images need to be stored in a secure and reliable container registry. Amazon ECR provides a private repository where Docker images can be securely stored, versioned, and managed before deployment.

In this lab, I created a private ECR repository, built a Docker image from a Dockerfile, and pushed the image to Amazon ECR using the AWS CLI and Docker.

## Why Use Amazon ECR?

Amazon Elastic Container Registry (ECR) is a fully managed Docker container registry provided by AWS.

It allows developers to:

*   Store private Docker images securely
    
*   Manage image versions and tags
    
*   Integrate with Amazon ECS and Amazon EKS
    
*   Simplify container image deployments
    
*   Improve security using IAM permissions
    

Using ECR eliminates the need to maintain your own Docker registry while providing seamless integration with other AWS container services.

### Task Requirements

The following tasks needed to be completed:

*   Create a private Amazon ECR repository named **devops-ecr**
    
*   Build a Docker image from the Dockerfile located in **/root/pyapp**
    
*   Tag the Docker image with **latest**
    
*   Authenticate Docker with Amazon ECR
    
*   Push the Docker image to the newly created ECR repository
    

## Step 1: Create a Private Amazon ECR Repository

I opened the **Amazon ECR Console** and selected **Create Repository**.

The repository was configured with the following details:

| Setting | Value |
| --- | --- |
| Repository Type | Private |
| Repository Name | devops-ecr |

After reviewing the configuration, I created the repository successfully.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/4d015910-bdc8-4bf5-b963-f194eb7c8196.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/69c0c2b5-170c-48ce-bdab-15d65cd21380.png align="center")

## Step 2: Build the Docker Image

The Dockerfile was already available under:

```plaintext
/root/pyapp
```

I navigated to the project directory and built the Docker image using Docker.

```plaintext
cd /root/pyapp

docker build -t devops-ecr:latest .
```

Once the build completed successfully, the Docker image was available locally with the **latest** tag.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/ed2b57a0-643f-4021-a4b2-bfdbaa166f52.png align="center")

## Step 3: Authenticate Docker with Amazon ECR

Before pushing the image, Docker must be authenticated with the Amazon ECR registry.

I used the AWS CLI to retrieve a temporary authentication token and logged in to the private ECR repository.

```plaintext
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <account-id>.dkr.ecr.us-east-1.amazonaws.com
```

After successful authentication, Docker was ready to push images to Amazon ECR.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/0c4bcddd-8c94-4595-a37d-8fdf3a84461c.png align="center")

## Step 4: Tag the Docker Image

Next, I tagged the locally built Docker image using the Amazon ECR repository URI.

```plaintext
docker tag devops-ecr:latest <account-id>.dkr.ecr.us-east-1.amazonaws.com/devops-ecr:latest
```

This associates the local image with the destination ECR repository.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/0a2a16ce-217b-4942-883d-340d91f699e8.png align="center")

## Step 5: Push the Docker Image to Amazon ECR

Finally, I pushed the Docker image to the private ECR repository.

```plaintext
docker push <account-id>.dkr.ecr.us-east-1.amazonaws.com/devops-ecr:latest
```

Docker uploaded all image layers, and the image was successfully stored in the **devops-ecr** repository.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/6d30d974-971b-488e-b542-7d6f513b5eaa.png align="center")

## Step 6: Verify the Repository

To verify the task, I opened the Amazon ECR Console and confirmed that the repository contained the Docker image with the **latest** tag.

This verified that the image had been successfully built and uploaded to Amazon ECR.

### What I Learned

This lab introduced the complete workflow for managing container images using Amazon ECR.

I learned that creating a repository is only one part of the process. Before an image can be pushed, Docker must authenticate with Amazon ECR, the image must be tagged correctly, and then uploaded to the registry.

Since services like Amazon ECS and Amazon EKS pull container images directly from Amazon ECR, understanding this workflow is an essential skill for deploying containerized applications on AWS.

## Conclusion

Day 28 provided hands-on experience with Amazon Elastic Container Registry by creating a private repository, building a Docker image, authenticating Docker with AWS, and pushing the image to Amazon ECR.

This workflow is commonly used in modern DevOps pipelines where Docker images are stored securely before being deployed to container orchestration platforms such as Amazon ECS, Amazon EKS, or AWS Fargate.
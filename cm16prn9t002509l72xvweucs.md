---
title: "Day 39 : AWS and IAM Basics☁"
seoTitle: "AWS IAM Basics Overview"
seoDescription: "Learn AWS and IAM basics with hands-on tasks. Understand EC2 instances, user data, and IAM roles, users, and groups"
datePublished: 2024-09-17T17:34:29.777Z
cuid: cm16prn9t002509l72xvweucs
slug: day-39-aws-and-iam-basics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1726594433293/c1bef944-48e9-48d9-a294-5177a9bfe246.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1726594448727/577928a0-9907-4d99-a9fe-4fcee7eb03f2.png
tags: aws, devops, iam, 90daysofdevops, trainwithshubham

---

[![AWS](https://camo.githubusercontent.com/fa0a1ec316ac368d5ebdbe0fdae0e3452d70e79c9e0e71ebe2c3a30012102994/68747470733a2f2f6d69726f2e6d656469756d2e636f6d2f6d61782f313430302f302a64497a584c516e366142436c6d31544a2e706e67 align="left")](https://camo.githubusercontent.com/fa0a1ec316ac368d5ebdbe0fdae0e3452d70e79c9e0e71ebe2c3a30012102994/68747470733a2f2f6d69726f2e6d656469756d2e636f6d2f6d61782f313430302f302a64497a584c516e366142436c6d31544a2e706e67)

By this time you have created multiple EC2 instances, and post installation manually installed applications like Jenkins, docker etc. Now let's switch to little automation part. Sounds interesting??🤯

## AWS:

Amazon Web Services is one of the most popular Cloud Provider that has free tier too for students and Cloud enthutiasts for their Handson while learning (Create your free account today to explore more on it).

Read from [here](https://aws.amazon.com/what-is-aws/)

## User Data in AWS:

* When you launch an instance in Amazon EC2, you have the option of passing user data to the instance that can be used to perform common automated configuration tasks and even run scripts after the instance starts. You can pass two types of user data to Amazon EC2: shell scripts and cloud-init directives.
    
* You can also pass this data into the launch instance wizard as plain text, as a file (this is useful for launching instances using the command line tools), or as base64-encoded text (for API calls).
    
* This will save time and manual effort everytime you launch an instance and want to install any application on it like apache, docker, Jenkins etc
    

Read more from [here](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/user-data.html)

## IAM:

AWS Identity and Access Management (IAM) is a web service that helps you securely control access to AWS resources. With IAM, you can centrally manage permissions that control which AWS resources users can access. You use IAM to control who is authenticated (signed in) and authorized (has permissions) to use resources. Read from [here](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)

### What is IAM Roles and explain the IAM Users, Groups and Roles ?

IAM Roles are a feature of AWS Identity and Access Management (IAM) that allow you to delegate access to users or services without sharing long-term credentials. Roles are used to grant permissions to entities you trust, such as AWS services, users from other AWS accounts, or users authenticated through an identity provider.

### IAM Users

IAM Users are individuals or services that need access to AWS resources. Each user has a unique identity and can be assigned specific permissions. Users can have their own credentials, such as passwords or access keys, to interact with AWS services.

### IAM Groups

IAM Groups are collections of IAM users. You can use groups to manage permissions for multiple users at once. For example, you might create a group for developers and assign permissions that all developers need. When you add a user to the group, they inherit the permissions assigned to the group.

### IAM Roles

IAM Roles are similar to users in that they are identities with permissions policies that determine what the identity can and cannot do in AWS. However, instead of being uniquely associated with one person, a role is intended to be assumable by anyone who needs it. Roles do not have long-term credentials (passwords or access keys) associated with them. Instead, when you assume a role, it provides temporary security credentials for the role session. Roles are often used to grant permissions to AWS services or to allow users from other AWS accounts to access your resources.

### Task1:

* Launch EC2 instance with already installed Jenkins on it. Once server shows up in console, hit the IP address in browser and you Jenkins page should be visible.
    
* Take screenshot of Userdata and Jenkins page, this will verify the task completion.
    

### Task2:

* Read more on IAM Roles and explain the IAM Users, Groups and Roles in your own terms.
    
* Create three Roles named: DevOps-User, Test-User and Admin.
    

### Let’s begin with Task 1

1. **Login to AWS Console** and open EC2.
    
2. **Launch an instance** with the following details:
    
    * Name: `userdata-instance`
        
    * OS: `Ubuntu`
        
    * Instance Type: `t2.micro` (Free tier)
        
    * Key Pair: Select or create a key pair(Example:-userdata-instance) then Allow HTTPS and HTTP traffic from the Internet in Network Settings.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726587357277/18c33280-68d1-449c-bbd6-d11527d87f0c.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726587390600/9e0d3e93-57f9-440a-98b1-d07fc4d59047.png align="center")
        
3. **Expand the Advanced Details tab** and enter the following script in the User Data box:
    

```bash
#!/bin/bash
sudo apt-get update -y
sudo apt install openjdk-11-jre -y
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins -y
sudo systemctl enable jenkins
sudo systemctl start jenkins
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726587536876/14c2c6e2-be99-41ba-bbaf-530b279594fd.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726587550129/41b0c842-1c35-4f0a-b2c5-47f8fb0d9c82.png align="center")

4. **Now Launch the instance**
    
5. Open port 8080 and Select My-ip in the inbound rules of the security group.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726587729260/8c70a136-07a4-4b52-a4c7-370c4039d792.png align="center")
    
6. **Open the Jenkins UI** in the browser using `<Public_IP:8080>`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726587781827/9abe1e7d-e6ae-4288-b8e2-9d695951d779.png align="center")
    

### Let’s begin with Task 2

#### Create IAM Roles

1. **Go to AWS Management Console**
    
2. Search IAM and click on the left side located Roles.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726588141699/098ee7d6-435a-4bc4-afa2-a7b1f755dbe6.png align="center")
    
3. **Click on Create Role**.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726588179745/c21e83c7-4ca3-4e6c-baee-d3765e8a1392.png align="center")
    
4. **Select AWS Service**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726588264511/e872957a-aa24-4211-93fc-d717f3f4d6c0.png align="center")
    
5. Choose EC2.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726588277899/611a848c-0c35-43c5-b194-7865260bbd83.png align="center")
    
6. **Select permission** `AmazonEC2FullAccess` creation and management.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726588370198/5b8c0668-82a6-4beb-a221-015b451a73c5.png align="center")
    
7. **Name the role** `User` and create it.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726588448474/814cbc64-10f4-46a0-ab25-40ec2bf6cd81.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726588393066/898d8a9c-8765-4400-816a-5cb378f9a6ca.png align="left")
    
    Thankyou For Reading !!!!!!
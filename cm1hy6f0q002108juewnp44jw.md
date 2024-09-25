---
title: "Day 42: IAM Programmatic access and AWS CLI 🚀 ☁"
seoTitle: "IAM Programmatic Access and AWS CLI Guide"
seoDescription: "Learn how to set up AWS IAM programmatic access and configure the AWS CLI. Step-by-step tasks for creating access keys and installing the CLI"
datePublished: Wed Sep 25 2024 14:15:23 GMT+0000 (Coordinated Universal Time)
cuid: cm1hy6f0q002108juewnp44jw
slug: day-42-iam-programmatic-access-and-aws-cli
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1727248028291/3992b460-00cf-4509-b1bc-8c3ea93e2527.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1727248387101/48f27ba5-0951-409d-b179-351c4a8167f1.png
tags: aws, devops, aws-cli, 90daysofdevops, trainwithshubham

---

Today is more of a reading excercise and getting some programmatic access for your AWS account

## IAM Programmatic access

In order to access your AWS account from a terminal or system, you can use AWS Access keys and AWS Secret Access keys.

## AWS CLI

The AWS Command Line Interface (AWS CLI) is a unified tool to manage your AWS services. With just one tool to download and configure, you can control multiple AWS services from the command line and automate them through scripts.

The AWS CLI v2 offers several new features including improved installers, new configuration options such as AWS IAM Identity Center (successor to AWS SSO), and various interactive features.

## Task-01

* Create AWS\_ACCESS\_KEY\_ID and AWS\_SECRET\_ACCESS\_KEY from AWS Console.
    

## Task-02

* Setup and install AWS CLI and configure your account credentials
    

Let me know if you have any issues while doing the task.

### Let’s begin with Task-01

### **Task 01: Create AWS Access Keys**

1. **Log in to AWS Management Console:**
    
    * Go to the AWS Management Console.
        
2. **Navigate to IAM:**
    
    * Click on your username in the top right corner of the console and select "Security Credentials" from the drop-down menu.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727246424836/c6e492e9-f2c2-4640-85fb-1bae13912c7d.png align="center")
        
3. **Create a New IAM User:**
    
    * Click on the "Access keys (access key ID and secret access key)" section.
        
    * Click on "Create Access Key".
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727246514369/23407328-b7f6-404e-98fc-26746a2a44ff.png align="left")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727246557571/89623b13-555a-4bd1-aa33-837a3c3f02dd.png align="left")
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727246625199/8819a8ff-c58d-4ab0-b498-f0657bf883d7.png align="center")

1. **Download Access Keys:**
    
    * Your Access Key ID and Secret Access Key will be displayed. Download the CSV file containing the access key information and store it in a secure location.
        

### Let’s begin with Task 02

1. Launch EC2 instance with below configuration
    
    * **AMI**: Ubuntu
        
    * **Instance Type**: t2.micro
        
    * **Network Settings**: Allow HTTP and HTTPS traffic
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727247033568/e8661b31-a590-4f3e-ac70-b21f62d3c69c.png align="center")
        
2. **Download and Install AWS CLI:**
    
    * Follow the instructions from documentation [AWS CLI installation](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
        
    
    ```bash
    sudo apt update
    sudo apt install unzip
    ```
    
    **To install** the AWS CLI, run the following commands.
    
    ```bash
    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
    unzip awscliv2.zip
    sudo ./aws/install
    ```
    
3. **Check AWS CLI Version:**
    
    * Open your terminal or command prompt and run the following command:
        
        ```bash
          aws --version
        ```
        
    * Ensure that AWS CLI is installed correctly and the version is displayed.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727247524863/7c7e4491-989a-4db6-b1ea-7050c5cbb838.png align="center")
        
4. **Configure AWS CLI:**
    
    * Run the command:
        
        ```bash
          aws configure
        ```
        
    * Enter your AWS Access Key ID, AWS Secret Access Key, Default region name, and Default output format when prompted.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727247732408/adb23187-69ba-4d3f-9a32-53ff3872b299.png align="center")
        

Example:

```bash
    $ aws configure
    AWS Access Key ID [None]: <Your_Access_Key_ID>
    AWS Secret Access Key [None]: <Your_Secret_Access_Key>
    Default region name [None]: us-west-2
    Default output format [None]: json
```

4. **Verify Configuration:**
    
    * Run a simple AWS CLI command to verify the setup:
        
        **Copy**
        
        **Copy**
        
        ```bash
          aws s3 ls
        ```
        
    * This command lists your S3 buckets. If configured correctly, you should see a list of your S3 buckets or an empty list if you don't have any.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727247864942/e2d2eeaa-0e2b-45b8-8804-bb4e37dfb358.png align="center")
        

Thankyou for reading !!!!!
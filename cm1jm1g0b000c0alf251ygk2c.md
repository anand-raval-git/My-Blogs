---
title: "Day 43: S3 Programmatic access with AWS-CLI 💻 📁"
seoTitle: "AWS S3 Programmatic Access with AWS-CLI"
seoDescription: "Learn to programmatically access Amazon S3 using AWS CLI in this"
datePublished: 2024-09-26T18:11:08.747Z
cuid: cm1jm1g0b000c0alf251ygk2c
slug: day-43-s3-programmatic-access-with-aws-cli
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1727374218847/a968a6ba-2007-4235-9e82-40e7cc639c20.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1727374249257/d8c853b6-acfc-42f4-b6f5-8aecf4aef576.png
tags: aws, devops, aws-s3, 90daysofdevops, trainwithshubham

---

Hi, I hope you had a great day yesterday. Today as part of the #90DaysofDevOps Challenge we will be exploring most commonly used service in AWS i.e S3.

[![s3](https://user-images.githubusercontent.com/115981550/218308379-a2e841cf-6b77-4d02-bfbe-20d1bae09b20.png align="left")](https://user-images.githubusercontent.com/115981550/218308379-a2e841cf-6b77-4d02-bfbe-20d1bae09b20.png)

# S3

Amazon Simple Storage Service (Amazon S3) is an object storage service that provides a secure and scalable way to store and access data on the cloud. It is designed for storing any kind of data, such as text files, images, videos, backups, and more. Read more [here](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html)

## Task-01

* Launch an EC2 instance using the AWS Management Console and connect to it using Secure Shell (SSH).
    
* Create an S3 bucket and upload a file to it using the AWS Management Console.
    
* Access the file from the EC2 instance using the AWS Command Line Interface (AWS CLI).
    

Read more about S3 using aws-cli [here](https://docs.aws.amazon.com/cli/latest/reference/s3/index.html)

## Task-02

* Create a snapshot of the EC2 instance and use it to launch a new EC2 instance.
    
* Download a file from the S3 bucket using the AWS CLI.
    
* Verify that the contents of the file are the same on both EC2 instances.
    

### Let’s begin with task 1

1. Login to AWS Console and search for "EC2".
    
2. Launch an instance with the following details:
    
    * Name: S3-AWS-CLI
        
    * Number of instance: 1
        
    * AMI: Ubuntu
        
    * Instance type: t2-micro
        
    * Network Settings: Allow HTTPS and HTTP traffic from the Internet
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727370111055/3e5f04b2-a348-4ea9-9e84-3d05303f8b88.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727370180486/2d9157d5-ee86-448e-89c4-2bf7b5292d92.png align="center")

3. Click "Launch Instance".
    
4. Connect to the instance.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727370243211/59d11d65-2628-48bb-8fac-6ef8971649b8.png align="center")
    
5. Search for S3 in the AWS Console and create a bucket.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727370277635/7c3181b4-373b-4d7f-baeb-1d1d61995e2b.png align="center")
    
    Click on right corner Create bucket
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727370335274/a62789a2-312b-4dbb-93f6-6baee1e792a0.png align="center")
    
    Now enter bucket name
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727370403532/572a74cf-d8c3-4e98-a3f9-e30fd39e8aa8.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727370423550/b09a39f5-3e97-4b9d-ac93-a6b85b42814f.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727370473612/d15e932f-2e45-455d-b55f-9b778789a717.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727370514560/a55e27d1-f4f3-4ff8-8f57-87dae2a9e564.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727370524239/6a74f64f-9d16-4336-8eca-802585574917.png align="center")
    
    Now click on create bucket
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727370559631/c325d22a-dd93-4ba6-9d99-635660295097.png align="center")
    
6. Upload a file to the bucket.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727370637084/ba69c9a3-fc03-4db4-9dea-eed47d7b02fe.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727370660007/d8e3c060-7219-48a5-b60b-75078fc673f9.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727370697682/d9b1aec8-6f99-4d33-bf73-67039aca4e86.png align="center")
    
7. Configure aws cli in created ec2 instance and Access the file from the EC2 instance using AWS CLI.
    

```bash
aws configure
```

#### AWS CLI Commands:

* List S3 buckets: `aws s3 ls`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727371246809/5b606a4f-c6c6-4397-91c0-85ce9fc12289.png align="center")
    
* Create a file and upload it to S3:
    
    ```bash
      echo "This is for testing purposes" > sample.txt
      aws s3 cp sample.txt s3://<bucket-name>
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727371375525/15dca7a7-d73c-4325-ab7e-58a1b3262853.png align="left")
    
* Download a file from S3: `aws s3 cp s3://<bucket-name>/<file-name> .`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727371445257/5a38482e-b3ed-4c3f-9100-dd244749871a.png align="center")
    
* Sync local folder with S3 bucket: `aws s3 sync . s3://<bucket-name>`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727371552354/669ed2e8-0fcf-43c3-be26-0f3eca15bb26.png align="center")
    
* List objects in an S3 bucket: `aws s3 ls s3://<bucket-name>`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727372074188/2d6148fd-4ebb-4531-9df3-35f691d0d6d0.png align="center")
    
* Delete an object from S3: `aws s3 rm s3://<bucket-name>/<file-name>`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727372170545/a886da5c-3f13-4d92-be6b-fd6e4396718a.png align="center")
    
* Create a new bucket: `aws s3 mb s3://<bucket-name>`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727372341617/8322e7c7-90eb-4d3d-9737-be286dd39b23.png align="center")
    
* Delete a bucket: `aws s3 rb s3://<bucket-name>`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727372386605/1843ffe1-cee4-45f6-8320-0f03cc8344d9.png align="center")
    

### Let’s begin with task 2

#### **Steps:**

1. Go to the instances page in the AWS Console and create a snapshot.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705481258958/d75f2b56-4c46-4fe3-97e1-7fd5250d92d0.png?auto=compress,format&format=webp&auto=compress,format&format=webp align="left")
    
2. Use the snapshot to launch a new EC2 instance.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727373401443/1763e57e-9aa9-4a5a-afa3-67de9200f9fc.png align="center")
    
3. Connect to the new instance using SSH.
    
4. Access the bucket list and download the content of the bucket.
    

Thankyou for reading !!!!!
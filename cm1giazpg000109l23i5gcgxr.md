---
title: "Day 41: Setting up an Application Load Balancer with AWS EC2 🚀 ☁"
seoTitle: "AWS EC2: Setup Application Load Balancer"
seoDescription: "Learn how to set up an Application Load Balancer on AWS EC2, enhancing your web applications' reliability and performance"
datePublished: Tue Sep 24 2024 14:03:17 GMT+0000 (Coordinated Universal Time)
cuid: cm1giazpg000109l23i5gcgxr
slug: day-41-setting-up-an-application-load-balancer-with-aws-ec2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1727152573937/83ce6fea-aec2-4278-a2f9-08b048f1b1f5.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1727153157132/361381fd-5a50-43dc-b256-480d212773de.png
tags: aws, devops, aws-ec2, 90daysofdevops, trainwithshubham

---

[![LB2](https://user-images.githubusercontent.com/115981550/218145297-d55fe812-32b7-4242-a4f8-eb66312caa2c.png align="left")](https://user-images.githubusercontent.com/115981550/218145297-d55fe812-32b7-4242-a4f8-eb66312caa2c.png)

Hi, I hope you had a great day yesterday learning about the launch template and instances in EC2. Today, we are going to dive into one of the most important concepts in EC2: Load Balancing.

## What is Load Balancing?

Load balancing is the distribution of workloads across multiple servers to ensure consistent and optimal resource utilization. It is an essential aspect of any large-scale and scalable computing system, as it helps you to improve the reliability and performance of your applications.

## Elastic Load Balancing:

**Elastic Load Balancing (ELB)** is a service provided by Amazon Web Services (AWS) that automatically distributes incoming traffic across multiple EC2 instances. ELB provides three types of load balancers:

Read more from [here](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/what-is-load-balancing.html)

1. **Application Load Balancer (ALB)** - *operates at layer 7 of the OSI model and is ideal for applications that require advanced routing and microservices.*
    

* Read more from [here](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html)
    

2. **Network Load Balancer (NLB)** - *operates at layer 4 of the OSI model and is ideal for applications that require high throughput and low latency.*
    

* Read more from [here](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html)
    

3. **Classic Load Balancer (CLB)** - *operates at layer 4 of the OSI model and is ideal for applications that require basic load balancing features.*
    

* Read more [here](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/introduction.html)
    

## 🎯 Today's Tasks:

### Task 1:

* launch 2 EC2 instances with an Ubuntu AMI and use User Data to install the Apache Web Server.
    
* Modify the index.html file to include your name so that when your Apache server is hosted, it will display your name also do it for 2nd instance which include " TrainWithShubham Community is Super Aweasome :) ".
    
* Copy the public IP address of your EC2 instances.
    
* Open a web browser and paste the public IP address into the address bar.
    
* You should see a webpage displaying information about your PHP installation.
    

### Task 2:

* Create an Application Load Balancer (ALB) in EC2 using the AWS Management Console.
    
* Add EC2 instances which you launch in task-1 to the ALB as target groups.
    
* Verify that the ALB is working properly by checking the health status of the target instances and testing the load balancing capabilities.
    

[![LoadBalancer](https://user-images.githubusercontent.com/115981550/218143557-26ec33ce-99a7-4db6-a46f-1cf48ed77ae0.png align="left")](https://user-images.githubusercontent.com/115981550/218143557-26ec33ce-99a7-4db6-a46f-1cf48ed77ae0.png)

### Let’s begin with task 1 :

1. **Log in to AWS Console** and navigate to EC2.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727104781899/a9485150-6075-400f-991f-0a69a8447392.png align="center")
    
2. **Launch two EC2 instances** with the following settings (Name:- Apache-1,Apache-2):
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727150209596/8e54f36f-fa05-4420-824e-62e0e48b1e39.png align="left")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727150128891/e73ccb4a-5763-4b8e-b259-81b092db4fa7.png align="left")
    
    * **AMI**: Ubuntu
        
    * **Instance Type**: t2.micro
        
    * **Network Settings**: Allow HTTP and HTTPS traffic
        
3. **Configure User Data** to install Apache using advanced detail and customize the `index.html` file.
    

```bash
#!/bin/bash
sudo apt-get update -y
sudo apt-get install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727150409370/287f2759-30bc-4ec1-9f6e-6dddc14e2a1d.png align="center")

4. **Modify** `index.html` on each server to display different content.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727150577621/da4e5b28-05de-4daa-95a5-825b119982c2.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727150729487/4f20d2a7-33da-43d0-963f-724da20fccc1.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727151081359/af875a95-bc87-42d9-ba95-c611f14e74b2.png align="center")
    
5. **Access the public IP addresses** of the instances to verify Apache installation.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727151059287/ba5733b2-8dcc-4ad4-904c-166b7249fc64.png align="center")
    

### Let’s begin with task 2:

#### Steps:

1. **Navigate to Load Balancers** in the AWS Management Console.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727151330673/ece2b4be-a705-442a-b23c-eba3becb77ff.png align="center")
    
    Click on create load balancer
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727151372365/43729914-d548-43e5-a121-1ee971b51f57.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727151422316/40fb31b2-88f6-42ac-8440-975c51a90212.png align="center")
    
2. **Create an Application Load Balancer**:
    
    * **Name**: php-load-balancer
        
    * **Scheme**: Internet Facing
        
    * **IP Address Type**: IPv4
        
    * **Network Mapping**: Select at least two AZs.
        
    * **Security Group**: Choose the required security groups.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727151501906/b33fc7b0-2a71-4bcc-b2dc-df1bc5923345.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727151569420/04953aae-0105-4cbd-a915-a21e9750e77c.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727151601293/545f2b8c-c983-426e-acdb-2febbad55e8c.png align="center")
        
3. **Create Target Groups** and register your EC2 instances.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727151649361/ffd60a72-f5a0-4cb6-a50d-2ee028988b22.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727151704208/ac89b62e-11df-401e-89dc-a258d69768da.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727151720028/d3c96cfd-2dd5-4188-b29b-4def915a65db.png align="center")
    
    * Now click on Create load balancer
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727151895356/9be397e1-4d59-4040-9bb9-5a44e01d6b9f.png align="center")
        

5. **Test the ALB** by accessing its DNS name. Verify that traffic is distributed between your instances.
    

Thankyou for reading !!!!!
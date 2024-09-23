---
title: "Day 40 : AWS EC2 Automation ☁"
seoTitle: "AWS EC2 Automation Day 40"
seoDescription: "Learn to automate AWS EC2 with launch templates, instance types, AMIs, and Auto Scaling groups. Step-by-step guide included"
datePublished: Mon Sep 23 2024 17:42:30 GMT+0000 (Coordinated Universal Time)
cuid: cm1fap29e00090al43jki5cma
slug: day-40-aws-ec2-automation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1727113391946/11d0515b-92fc-4d61-96ff-3aaf8584412f.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1727113319711/3b3815a7-136c-4f94-a27e-169a7e973f5e.png
tags: aws, devops, instance, 90daysofdevops, trainwithshubham

---

## Automation in EC2:

Amazon EC2 or Amazon Elastic Compute Cloud can give you secure, reliable, high-performance, and cost-effective computing infrastructure to meet demanding business needs.

Also, if you know a few things, you can automate many things.

Read from [here](https://aws.amazon.com/ec2/)

## Launch template in AWS EC2:

* You can make a launch template with the configuration information you need to start an instance. You can save launch parameters in launch templates so you don't have to type them in every time you start a new instance.
    
* For example, a launch template can have the AMI ID, instance type, and network settings that you usually use to launch instances.
    
* You can tell the Amazon EC2 console to use a certain launch template when you start an instance.
    

Read more from [here](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-launch-templates.html)

## Instance Types:

Amazon EC2 has a large number of instance types that are optimised for different uses. The different combinations of CPU, memory, storage and networking capacity in instance types give you the freedom to choose the right mix of resources for your apps. Each instance type comes with one or more instance sizes, so you can adjust your resources to meet the needs of the workload you want to run.

Read from [here](https://aws.amazon.com/ec2/instance-types/?trk=32f4fbd0-ffda-4695-a60c-8857fab7d0dd&sc_channel=ps&s_kwcid=AL!4422!3!536392685920!e!!g!!ec2%20instance%20types&ef_id=CjwKCAiA0JKfBhBIEiwAPhZXD_O1-3qZkRa-KScynbwjvHd3l4UHSTfKuigd5ZPukXoDXu-v3MtC7hoCafEQAvD_BwE:G:s&s_kwcid=AL!4422!3!536392685920!e!!g!!ec2%20instance%20types)

## AMI:

An Amazon Machine Image (AMI) is an image that AWS supports and keeps up to date. It contains the information needed to start an instance. When you launch an instance, you must choose an AMI. When you need multiple instances with the same configuration, you can launch them from a single AMI.

### Task1:

* Create a launch template with Amazon Linux 2 AMI and t2.micro instance type with Jenkins and Docker setup (You can use the Day 39 User data script for installing the required tools.
    
* Create 3 Instances using Launch Template, there must be an option that shows number of instances to be launched ,can you find it? :)
    

## **Creating a Launch Template and Launching Instances**

1. **Create a Launch Template**:
    
    * Login into AWS Console and search for "EC2".
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727104781899/a9485150-6075-400f-991f-0a69a8447392.png align="center")
        
    * Now click on Launch Templates(Left side corner).
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727104936622/9c65182d-f126-4973-a7e5-01a004a2e3eb.png align="center")
        
    * Click on **Create launch template(Orange button)**.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727104957256/bd24ad59-1216-4638-8007-8f5f94fe194d.png align="center")
        
    * Enter a name (e.g., `DevopsTemplate`) and a description for the template.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727105066814/67614f06-c006-4106-bee6-6aec031685ae.png align="center")
        
    * For **Amazon Machine Image (AMI)**, Click on Quick start and choose **Ubuntu**.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727105110645/cb8035ec-cee4-487a-af05-c7d9a119dd42.png align="center")
        
    * For **Instance type**, choose **t2.micro**.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727105183775/649e5ce7-aede-47a4-8f7e-d84cacf0a18f.png align="center")
        
    * Select or create a security group.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727105224496/06e3cbd9-5a27-4f5e-a32e-3d81fa959184.png align="center")
        
    * In the **Advanced Details** section, paste the user data script for installing Jenkins and Docker.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727105271045/69599417-4b22-4470-a731-28deb03ab0bc.png align="center")
        

Here's an example of a user data script for setting up Jenkins and Docker:

```bash
#!/bin/bash
sudo apt-get update -y
sudo apt install openjdk-11-jre -y
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins -y
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo apt-get update
sudo apt-get install docker.io -y
sudo systemctl start docker
```

* Click **Create launch template**.
    

2. **Launch Instances Using the Launch Template**:
    
    * In the Amazon EC2 console, click on Create launch instance (orange button).
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727111270093/0a3cb36c-9cba-4216-8605-a76fbdb79617.png align="center")
        
    * Select the launch template you created.
        
    * Specify the number of instances you want to launch (e.g., 2).
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727111400592/4e9a1b6d-678a-4169-94cf-82b2d5bd8ab9.png align="center")
        
    * Configure other settings such as VPC, subnet, and security group as desired.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727111495077/332c8073-063b-4929-9628-51c8f9119b51.png align="center")
        
    * Choose **Launch instances**.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727111532940/c68b46de-f928-49dd-bd05-a6ddc8070561.png align="center")
        
    * Verify that the instances are running in the **Instances** section.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727111565260/dcce92ce-edd2-4014-b651-2e4c36a233d2.png align="center")
        

## Creating an Auto Scaling Group

An Auto Scaling group (ASG) is a collection of EC2 instances that are treated as a logical unit for automatic scaling and management. ASGs automatically adjust the number of instances based on demand, ensuring your application maintains optimal performance and cost-efficiency.

### Steps to Create an Auto Scaling Group:

1. **Navigate to Auto Scaling Groups**:
    
    * In the left navigation pane, choose **Auto Scaling Groups**.
        
    * Click **Create Auto Scaling group**.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727111613183/37224581-6489-4ce7-a39c-78c97b8c94ac.png align="center")
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727111653222/d5e3b23e-ff8b-41ad-8285-061fa0f28184.png align="center")
    
2. **Configure the Auto Scaling Group**:
    
    * Enter a name (e.g., `DJScaling`).
        
    * Choose the launch template created earlier, Specify the version (default to the latest version).
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727111751234/48dbf340-d196-4c6a-aead-d40aa1271814.png align="center")
        
3. **Configure Network and Load Balancer**:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727111819752/b8fa6c24-a540-471f-9482-6f6e968cc4b9.png align="center")
    
    * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727111922018/7700d524-623b-42a1-9e3b-12ea625742c7.png align="center")
        
        Select the VPC and subnets for the instances.
        
    * Attach a new load balancer if required.
        
    * Create a target group for the load balancer.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727112007413/018a7a41-6af7-4c8f-b813-fed24f09b08c.png align="center")
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727112043332/a7956efe-4929-48e0-977c-4b91622102d2.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727112124521/08e9adb8-86e6-4f89-a1ef-d625e1029a0f.png align="center")

1. **Set Group Size and Scaling Policies**:
    
    * Desired capacity: 3
        
    * Minimum capacity: 1
        
    * Maximum capacity: 5
        
    * Configure scaling policies based on metrics such as CPU utilization.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727112225239/028b01d2-ab75-47ad-9220-c1c800227622.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727112245084/d1e80c46-fd52-4023-a1b2-752514361f74.png align="center")
        
2. **Finalize and Create the Auto Scaling Group**:
    
    * Add notifications and tags if needed.
        
    * Review the configuration.
        
    * Click **Create Auto Scaling group**.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727112334800/afcd6529-c55b-49f8-8d5b-fe33c7709644.png align="center")
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727112424545/21bc55aa-9549-46a6-8f5e-e536665bac42.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727112457412/3f5ee391-74f5-4353-88fe-3c12b68f4825.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727112551656/c2802425-1eb5-4173-8816-de7cf2d93392.png align="center")

Thankyou for reading !!!!!
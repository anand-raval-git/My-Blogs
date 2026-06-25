---
title: "AWS Day 26: Configuring an EC2 Instance as an Nginx Web Server Using User Data"
seoTitle: "AWS Day 26: Configure an EC2 Instance as an Nginx Web Server"
seoDescription: "Learn how to configure an Amazon EC2 instance as an Nginx web server using EC2 User Data. Step-by-step guide covering User Data scripts."
datePublished: 2026-06-25T18:08:23.228Z
cuid: cmqttfixm00000ai79uq15814
slug: aws-day-26-configuring-an-ec2-instance-as-an-nginx-web-server-using-user-data
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/9ff5dab8-412c-49f3-905f-9ba3ead706d0.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/d36b6674-cc44-4fb2-b8f7-2b7562a94ecc.png
tags: ec2, aws, nginx, kodekloud, anand-raval

---

## Introduction

During Day 26 of the KodeKloud 100 Days of Cloud Challenge, I learned how to automate the setup of an EC2 instance using **User Data**.

Instead of launching an EC2 instance and manually installing Nginx after connecting through SSH, AWS provides User Data scripts that run automatically during the first boot of the instance. This makes server provisioning faster, repeatable, and suitable for production environments.

In this lab, the objective was to launch an Ubuntu EC2 instance, automatically install Nginx using a User Data script, and make the web server accessible over HTTP.

## Why Use EC2 User Data?

User Data allows you to execute shell scripts automatically when an EC2 instance starts for the first time.

Some common use cases include:

*   Installing software packages
    
*   Configuring web servers
    
*   Updating the operating system
    
*   Deploying applications automatically
    
*   Bootstrapping cloud infrastructure
    

Instead of performing these tasks manually after every launch, User Data automates the entire setup process.

### Task Requirements

The following resources needed to be configured:

*   Launch an EC2 instance named **nautilus-ec2**
    
*   Use any available Ubuntu AMI
    
*   Configure a User Data script to install Nginx
    
*   Start and enable the Nginx service
    
*   Allow HTTP traffic on port **80**
    
*   Verify that the Nginx welcome page is accessible from the internet
    

## Step 1: Launch an EC2 Instance

I opened the EC2 Dashboard and clicked **Launch Instance**.

The instance was configured with the following settings:

| Setting | Value |
| --- | --- |
| Name | nautilus-ec2 |
| AMI | Ubuntu |
| Instance Type | t2.micro (default) |

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/bdcb783e-9cc8-4e70-9829-e3a9e0250773.png align="center")

## Step 2: Configure the User Data Script

While creating the instance, I expanded the **Advanced Details** section and added the following User Data script.

```plaintext
#!/bin/bash

apt update
apt upgrade -y
apt install nginx -y
systemctl start nginx
systemctl enable nginx
```

This script updates the package list, installs Nginx, starts the service, and ensures it starts automatically whenever the EC2 instance reboots.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/b29d350d-28f8-4a25-baad-2273b75eced1.png align="center")

## Step 3: Configure the Security Group

Since the Nginx server needs to be accessible from the internet, I configured the Security Group to allow inbound HTTP traffic.

The inbound rule used was:

<table style="min-width: 75px;"><colgroup><col style="min-width: 25px;"><col style="min-width: 25px;"><col style="min-width: 25px;"></colgroup><tbody><tr><td colspan="1" rowspan="1"><p>Type</p></td><td colspan="1" rowspan="1"><p>Port</p></td><td colspan="1" rowspan="1"><p>Source</p></td></tr><tr><td colspan="1" rowspan="1"><p>HTTP</p></td><td colspan="1" rowspan="1"><p>80</p></td><td colspan="1" rowspan="1"><p>0.0.0.0/0</p></td></tr></tbody></table>

This allows users to access the web server using the EC2 public IP address.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/06178dc7-38b8-41a7-a56a-6a536768c643.png align="center")

## Step 4: Verify the Nginx Installation

Finally, I copied the Public IPv4 address of the EC2 instance and opened it in my browser.

```plaintext
http://<EC2-Public-IP>
```

The default **Nginx Welcome Page** appeared successfully, confirming that the User Data script had installed and configured Nginx correctly.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/ee22673a-b95b-424b-993f-ebce39f489be.png align="center")

## Conclusion

Day 26 introduced one of the most practical automation features available in Amazon EC2.

By using a User Data script, I successfully configured an Ubuntu EC2 instance as an Nginx web server without any manual installation steps. This approach is commonly used in production environments to automate infrastructure provisioning and create consistent server deployments.
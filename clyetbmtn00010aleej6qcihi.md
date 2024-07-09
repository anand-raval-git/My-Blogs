---
title: "Day 4 [part :- 2] :- 🔗 Connecting Two EC2 Instances via SSH: A Step-by-Step Guide 🚀"
seoTitle: "Connect Two EC2 Instances via SSH: Guide"
seoDescription: "Step-by-step guide to connect two EC2 instances via SSH and transfer files efficiently"
datePublished: Tue Jul 09 2024 19:37:03 GMT+0000 (Coordinated Universal Time)
cuid: clyetbmtn00010aleej6qcihi
slug: day-4-part-2-connecting-two-ec2-instances-via-ssh-a-step-by-step-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720553764097/3dd7aae6-d579-407e-979b-67f3eca25c49.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1720553801901/a77e9423-5984-4773-95c6-cddcc2cbbcc1.png
tags: ubuntu, devops, ssh, 90daysofdevops, trainwithshubham

---

## • **How to Connect One EC2 Instance to Another EC2 Instance**

In this guide, we'll walk through the steps to connect one EC2 instance to another using SSH. This is a common task when you need to manage multiple instances or transfer files between them.

### **Prerequisites**

* Two running EC2 instances.
    
* SSH key pair for accessing the instances.
    
* Security group rules allowing SSH access.
    

### **Step-by-Step Guide**

In the example, we have two EC2 instances:

1. 172.31.33.186 (Linux)
    
2. 172.31.22.225 (Server) - We want to connect to this server.
    

First, on the 172.31.33.186 (Linux) instance, create an SSH private and public key using the following command:

```bash
ssh-keygen
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720548844228/b3adcd2d-30ef-41ea-b453-b762020aea6c.png align="left")

Navigate to the `.ssh` directory using the `cd` command:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720549238129/49192769-b472-4b60-b8b1-36eb7a4e23bd.png align="left")

Copy the public key (`id_`[`ed255519.pub`](http://ed255519.pub)):

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720549252656/b347c071-ab79-4f11-91d8-a6a6a2077099.png align="left")

Next, on the 172.31.22.225 (Server) instance, navigate to the `.ssh` directory and paste the public key from 172.31.33.186 (Linux) into the `authorized_keys` file:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720549868779/5f38770d-094c-4988-a12c-cf89757efe4a.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720549971974/9e67179f-cf64-4564-9766-fa0a4c77401c.png align="left")

Copy the public DNS of the 172.31.22.225 (Server):

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720550296870/dfe5ae39-91da-4d9d-ba32-45802b89d6fd.png align="left")

On the 172.31.33.186 (Linux) terminal, use the following command to connect:

```bash
ssh -i #private_key# ubuntu@public_dns#
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720550922652/7990bc93-d890-4bfd-b2a3-c26a247253c1.png align="left")

### • **How to Copy and Transfer Files to the Jump Server**

To transfer files to the jump server, use the following command:

```bash
scp -i #private_key# ubuntu@#public_dns#:/hpme/ubuntu/path
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720551654204/25e29426-4721-486f-be7a-a4fdd6fb870c.png align="left")

You can then verify the files on the server:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720551674623/6128eee2-f283-4500-839a-bc7aaa95b5f0.png align="left")

Thank you for reading!

<mark>© 2024 Anand Raval. All rights reserved.</mark>
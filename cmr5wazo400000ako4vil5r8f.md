---
title: "Day 27: Configuring a Public VPC with an EC2 Instance for Internet Access"
seoTitle: "AWS Day 27: Creating a Public VPC with an EC2 Instance"
seoDescription: "how to create a public VPC in AWS, configure a public subnet with automatic public IP assignment, launch an EC2 instance, and enable SSH access "
datePublished: 2026-07-04T05:02:04.600Z
cuid: cmr5wazo400000ako4vil5r8f
slug: day-27-configuring-a-public-vpc-with-an-ec2-instance-for-internet-access
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/90f9e3fa-6419-4813-9607-1d901c4b7383.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/fa2cf117-ecba-4ef5-a784-e8261552cf25.png
tags: aws, vpc, kodekloud, kodekloudengineer, anand-raval

---

## Introduction

During Day 27 of the KodeKloud 100 Days of Cloud Challenge, I explored one of the core networking concepts in AWS by creating a **Public Virtual Private Cloud (VPC)**.

Every AWS resource runs inside a network, and understanding how VPCs, subnets, and internet connectivity work is essential for building secure and scalable cloud infrastructure. In this lab, I created a public VPC, configured a public subnet with automatic public IP assignment, and launched an EC2 instance that could be accessed over the internet using SSH.

## Why Create a Public VPC?

A Virtual Private Cloud (VPC) allows you to build an isolated network inside AWS where you can launch and manage your resources securely.

Public VPCs are commonly used for hosting resources that need internet access, such as:

*   Web servers
    
*   Bastion hosts
    
*   Load Balancers
    
*   Public APIs
    
*   Development environments
    

By enabling automatic public IP assignment, every EC2 instance launched inside the subnet can receive a public IP address and communicate over the internet.

### Task Requirements

The following AWS resources needed to be configured:

*   Create a VPC named **xfusion-pub-vpc**
    
*   Create a subnet named **xfusion-pub-subnet**
    
*   Enable **Auto-Assign Public IPv4 Address** for the subnet
    
*   Launch an EC2 instance named **xfusion-pub-ec2**
    
*   Use **t2.micro** as the instance type
    
*   Allow inbound SSH traffic on **port 22**
    
*   Ensure the EC2 instance is accessible from the internet
    

## Step 1: Create a Public VPC

I opened the **VPC Dashboard** and clicked **Create VPC**.

The VPC was configured with the following details:

| Setting | Value |
| --- | --- |
| Name | xfusion-pub-vpc |
| IPv4 CIDR | Default (or as required) |

After reviewing the configuration, I created the VPC successfully.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/b4a5d53a-c47e-4172-a7a1-e96649230ff8.png align="center")

## Step 2: Create a Public Subnet

Inside the newly created VPC, I created a subnet with the following configuration:

<table style="min-width: 50px;"><colgroup><col style="min-width: 25px;"><col style="min-width: 25px;"></colgroup><tbody><tr><td colspan="1" rowspan="1"><p>Setting</p></td><td colspan="1" rowspan="1"><p>Value</p></td></tr><tr><td colspan="1" rowspan="1"><p>Name</p></td><td colspan="1" rowspan="1"><p>xfusion-pub-subnet</p></td></tr><tr><td colspan="1" rowspan="1"><p>VPC</p></td><td colspan="1" rowspan="1"><p>xfusion-pub-vpc</p></td></tr></tbody></table>

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/21963d02-d048-443f-9b49-af35e517d252.png align="center")

After creating the subnet, I enabled:

```plaintext
Auto-Assign Public IPv4 Address
```

This ensures that every EC2 instance launched in this subnet automatically receives a public IP address.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/1b21bda5-d685-4528-83c2-478a5ebf5e92.png align="center")

## Step 3: Attach an Internet Gateway to the VPC

To allow resources inside the VPC to communicate with the internet, I created an **Internet Gateway (IGW)** and attached it to the **xfusion-pub-vpc**.

Without an Internet Gateway, even an EC2 instance with a public IP address cannot send or receive traffic from the internet.

After attaching the Internet Gateway, I verified that its status showed **Attached**, confirming that it was successfully connected to the VPC.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/11774848-c4f0-414c-8a37-6a4e39bd951c.png align="center")

## Step 4: Configure the Route Table

The next step was to update the route table associated with the public subnet.

I added a new route with the following configuration:

| Destination | Target |
| --- | --- |
| 0.0.0.0/0 | Internet Gateway (IGW) |

This route tells AWS to forward all internet-bound traffic through the Internet Gateway, making the subnet publicly accessible.

After saving the changes, the route became active.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/8072abfb-b7ff-4566-a7e9-bc329710ee3f.png align="center")

## Step 5: Launch an EC2 Instance in the Public Subnet

With the networking configuration in place, I launched a new EC2 instance.

During the launch process, I configured the following:

| Setting | Value |
| --- | --- |
| Instance Name | xfusion-pub-ec2 |
| Instance Type | t2.micro |
| VPC | xfusion-pub-vpc |
| Subnet | xfusion-pub-subnet |

I also created a Security Group that allowed **SSH (Port 22)** access so the instance could be accessed remotely.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/0a52c9cf-6ec2-4bbe-8f2b-620c826f5bd5.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/9fa7473a-e447-4ddc-85a4-63b3be354145.png align="center")

## Step 6: Verify the EC2 Instance Deployment

After launching the instance, I navigated to the **EC2 Instances** dashboard to verify the deployment.

The instance appeared in the **Running** state with the correct VPC and subnet configuration, confirming that the infrastructure had been created successfully.

At this point, the EC2 instance was ready for SSH access once the status checks completed.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/8ab58c2b-ec4e-47b8-a6fc-05e8f977f45a.png align="center")

## What I Learned

This lab helped me understand how multiple AWS networking components work together.

Creating a VPC alone doesn't make an EC2 instance publicly accessible. The subnet must assign public IP addresses, and the Security Group must allow the required traffic. All of these configurations work together to enable internet connectivity.

I also learned why VPC design is one of the first steps when building AWS infrastructure, as it defines how resources communicate with each other and with the outside world.

## Conclusion

Day 27 provided hands-on experience with AWS networking by creating a public VPC, configuring a public subnet, and launching an internet-accessible EC2 instance.

Although the setup was simple, it introduced several fundamental networking concepts that are widely used in real-world AWS environments. Understanding VPCs, subnets, public IP assignment, and Security Groups is essential for designing secure and scalable cloud architectures.
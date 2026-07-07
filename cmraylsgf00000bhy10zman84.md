---
title: "AWS Day 30: Enable Internet Access for Private EC2 using NAT Instance "
seoTitle: "Enable Internet Access for a Private EC2 Using  NAT Instance"
seoDescription: "Learn how to configure a NAT Instance in AWS to provide internet access for a private EC2 instance. This step-by-step guide covers public subnet creat"
datePublished: 2026-07-07T18:05:18.583Z
cuid: cmraylsgf00000bhy10zman84
slug: aws-day-30-enable-internet-access-for-private-ec2-using-nat-instance
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/9404c4a3-71fa-4e36-856f-e4e0644b1566.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/7350db61-5478-49c7-bf93-7e53929d0a6d.png
tags: aws, nat-instance, kodekloudengineer, anand-raval

---

## Introduction

During Day 30 of the KodeKloud 100 Days of Cloud Challenge, I worked on one of the most interesting AWS networking concepts: **providing internet access to a private EC2 instance using a NAT Instance**.

In a well-designed AWS architecture, application servers are often deployed inside private subnets to improve security. Since these instances don't have public IP addresses, they cannot directly access the internet for tasks such as downloading software updates or communicating with AWS services.

To solve this problem, AWS provides two common solutions: **NAT Gateway** and **NAT Instance**. While NAT Gateway is the recommended managed service, this lab focused on configuring a **NAT Instance**, which is a cost-effective option for learning and small environments.

## Why Use a NAT Instance?

A NAT (Network Address Translation) Instance allows EC2 instances in a private subnet to initiate outbound internet connections while preventing inbound connections directly from the internet.

Common use cases include:

*   Downloading software packages
    
*   Installing application dependencies
    
*   Accessing Amazon S3
    
*   Retrieving updates from public repositories
    
*   Secure outbound internet connectivity
    

Although AWS recommends using a NAT Gateway for production workloads, understanding how a NAT Instance works provides valuable insight into AWS networking.

## Task Requirements

The objective of this lab was to:

*   Create a public subnet named **nautilus-pub-subnet**
    
*   Launch an Amazon Linux 2023 EC2 instance named **nautilus-nat-instance**
    
*   Configure the instance to function as a NAT Instance
    
*   Create and attach a custom Security Group
    
*   Enable internet access for the existing private EC2 instance
    
*   Verify that the file **nautilus-test.txt** was uploaded successfully to the S3 bucket **nautilus-nat-32360**
    

## Step 1: Create a Public Subnet

I opened the **VPC Console** and created a new public subnet inside the existing **nautilus-priv-vpc**.

The subnet was configured with the following details:

| Setting | Value |
| --- | --- |
| Name | nautilus-pub-subnet |
| VPC | nautilus-priv-vpc |

To make the subnet public, I associated it with a route table that routes internet-bound traffic through the Internet Gateway.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/40f875f5-c126-4a7a-8d1d-b4de3411b84b.png align="center")

## Step 2: Attach an Internet Gateway to the VPC

After creating the public subnet, I created a new **Internet Gateway** and attached it to the existing **nautilus-priv-vpc**. This allows resources inside the public subnet to communicate with the internet.

**Navigation:**

```plaintext
VPC → Internet Gateways → Create Internet Gateway → Attach to VPC
```

Once attached, the Internet Gateway status changed to **Attached**, confirming that the VPC now had internet connectivity.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/7a656bad-40a0-41e9-877a-87a8ffa6a731.png align="center")

## Step 3: Update the Public Route Table

Next, I modified the route table associated with the public subnet.

I added a new route so that all outbound internet traffic is forwarded through the Internet Gateway.

| Destination | Target |
| --- | --- |
| 0.0.0.0/0 | Internet Gateway (pub-ig) |

Without this route, instances in the public subnet would not be able to reach the internet.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/3fed9444-cc82-477b-9184-4e39820dfaeb.png align="center")

## Step 4: Launch the NAT Instance

Now I launched an EC2 instance that will act as the NAT Instance.

The configuration used was:

| Setting | Value |
| --- | --- |
| Name | nautilus-nat-instance |
| AMI | Amazon Linux 2023 |
| VPC | nautilus-priv-vpc |
| Subnet | nautilus-pub-subnet |
| Auto Assign Public IP | Enabled |
| Security Group | New Security Group |

The NAT Instance was launched inside the newly created public subnet so it could communicate with both the internet and the private subnet.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/a3a6800b-21a7-449b-99c6-f684ccba1bcb.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/45176130-7809-4bf8-b51d-fac14fb609a8.png align="center")

## Step 5: Disable Source/Destination Check

By default, every EC2 instance validates that network traffic is either coming from or intended for itself.

Since a NAT Instance forwards traffic on behalf of other EC2 instances, this feature must be disabled.

I selected the NAT instance and navigated to:

```plaintext
Actions → Networking → Change Source/Destination Check
```

Then I disabled **Source/Destination Check**.

This is one of the most important steps while configuring a NAT Instance.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/9f14d1f3-3d41-4dc8-aeff-f507035032a4.png align="center")

## Step 6: Configure the NAT Instance Security Group

To allow internet traffic to pass through the NAT Instance, I updated its Security Group.

The inbound rules included:

*   **SSH (22)** – for remote administration
    
*   **HTTP (80)** – to allow outbound web traffic
    
*   **HTTPS (443)** – for secure internet access
    
*   **Custom ICMP** – for connectivity testing
    

This ensures that the NAT Instance can communicate properly with both the internet and the private subnet.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/65633979-dc69-447d-a34e-1da6500ecbd1.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/3ce69c35-42b7-4859-a984-7d52abe3e5bd.png align="center")

## Step 7: Configure the NAT Instance

After connecting to the NAT Instance through SSH, I installed **iptables**, enabled IP forwarding, and configured NAT rules.

```shell
# 1. Install iptables
sudo yum install -y iptables-services

# 2. Enable IP forwarding
echo "net.ipv4.ip_forward = 1" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p

# 3. Find the network interface
ip addr

# 4. Add NAT rule (replace ens5 with your interface)
sudo iptables -t nat -A POSTROUTING -o ens5 -j MASQUERADE

# 5. Allow forwarding
sudo iptables -P FORWARD ACCEPT
sudo iptables -A FORWARD -i ens5 -j ACCEPT
sudo iptables -A FORWARD -o ens5 -j ACCEPT

# 6. Enable and save iptables
sudo systemctl enable iptables
sudo systemctl start iptables
sudo service iptables save

```

## Step 8: Update the Private Route Table

Finally, I updated the route table associated with the private subnet.

Instead of routing internet traffic directly to an Internet Gateway, I pointed the default route to the NAT Instance.

| Destination | Target |
| --- | --- |
| 0.0.0.0/0 | nautilus-nat-instance |

Now, whenever the private EC2 instance needs internet access, its traffic is first forwarded to the NAT Instance, which then sends it to the internet.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/550cb1e9-342c-4027-b7df-3304f3cea460.png align="center")

## Step 9: Verify Internet Connectivity

To verify the setup, I checked the Amazon S3 bucket.

The private EC2 instance was already configured with a cron job that attempted to upload a test file every minute.

After the NAT Instance was configured successfully, the file **nautilus-test.txt** appeared inside the S3 bucket, confirming that the private EC2 instance could now access the internet through the NAT Instance.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/da2858d1-df2b-4805-965e-953730d58159.png align="center")

### What I Learned

This lab helped me understand how outbound internet access works for resources deployed in private subnets.

One important lesson was that launching a NAT Instance alone is not enough. Several configurations—including disabling Source/Destination Check, enabling IP forwarding, configuring iptables, and updating the route table—must all work together before traffic can flow successfully.

I also learned why managed NAT Gateways are preferred in production environments, while NAT Instances remain a useful option for learning, testing, and cost-sensitive deployments.

## Conclusion

Day 30 introduced one of the most important networking concepts in AWS by enabling internet access for a private EC2 instance using a NAT Instance.

By creating a public subnet, configuring a NAT Instance, updating route tables, and verifying connectivity through an S3 upload, I gained practical experience with how private workloads securely access external services without being directly exposed to the internet.
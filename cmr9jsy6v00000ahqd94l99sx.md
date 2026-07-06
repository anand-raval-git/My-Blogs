---
title: "AWS Day 29: Establishing Secure Communication Between Public and Private VPCs via VPC Peering"
seoTitle: "AWS Day 29: Connect Public and Private VPCs Using VPC Peerin"
seoDescription: "Learn how to configure AWS VPC Peering between a public and private VPC, update route tables, configure security groups"
datePublished: 2026-07-06T18:23:12.194Z
cuid: cmr9jsy6v00000ahqd94l99sx
slug: aws-day-29-establishing-secure-communication-between-public-and-private-vpcs-via-vpc-peering
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/4d384801-69ce-4c1a-8356-142580159644.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/f07f741e-ae47-4f73-903c-46829e931120.png
tags: aws, vpc, kodekloudengineer, anand-raval

---

## Introduction

During Day 29 of the KodeKloud 100 Days of Cloud Challenge, I explored **AWS VPC Peering**, a networking feature that enables secure communication between two Virtual Private Clouds (VPCs).

In many AWS environments, applications are distributed across multiple VPCs to improve security and isolate workloads. However, there are situations where resources in different VPCs need to communicate privately without sending traffic over the public internet. AWS solves this using **VPC Peering**, which creates a private network connection between two VPCs.

In this lab, I configured a VPC Peering connection between the default public VPC and an existing private VPC, updated the route tables, configured security groups, and verified connectivity between two EC2 instances.

## What is AWS VPC Peering?

AWS VPC Peering allows two VPCs to communicate using private IPv4 or IPv6 addresses.

Unlike Internet Gateways or NAT Gateways, VPC Peering keeps traffic entirely within the AWS network, providing secure and low-latency communication between resources.

Some common use cases include:

*   Connecting public and private VPCs
    
*   Sharing services across multiple VPCs
    
*   Multi-tier application architectures
    
*   Cross-team or cross-environment communication
    
*   Secure backend connectivity
    

## Task Requirements

The following tasks needed to be completed:

*   Create a VPC Peering Connection named **nautilus-vpc-peering**
    
*   Connect the **Default Public VPC** and **nautilus-private-vpc**
    
*   Update the Route Tables in both VPCs
    
*   Configure Security Groups to allow communication
    
*   SSH into the public EC2 instance
    
*   Verify connectivity by pinging the private EC2 instance
    

## Step 1: Review the Existing Infrastructure

Before creating the peering connection, I verified the existing resources.

The lab already contained:

| Resource | Name |
| --- | --- |
| Public EC2 | nautilus-public-ec2 |
| Private VPC | nautilus-private-vpc |
| Private Subnet | nautilus-private-subnet |
| Private EC2 | nautilus-private-ec2 |

This saved time since only the networking configuration needed to be completed.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/05f0f519-3f68-46db-bee9-12c5070660cc.png align="center")

## Step 2: Create the VPC Peering Connection

I opened the **VPC Dashboard** and navigated to:

```plaintext
VPC → Peering Connections
```

Then I created a new peering connection with the following configuration:

<table style="min-width: 50px;"><colgroup><col style="min-width: 25px;"><col style="min-width: 25px;"></colgroup><tbody><tr><td colspan="1" rowspan="1"><p>Setting</p></td><td colspan="1" rowspan="1"><p>Value</p></td></tr><tr><td colspan="1" rowspan="1"><p>Name</p></td><td colspan="1" rowspan="1"><p>nautilus-vpc-peering</p></td></tr><tr><td colspan="1" rowspan="1"><p>Requester VPC</p></td><td colspan="1" rowspan="1"><p>Default VPC</p></td></tr><tr><td colspan="1" rowspan="1"><p>Accepter VPC</p></td><td colspan="1" rowspan="1"><p>nautilus-private-vpc</p></td></tr></tbody></table>

After creating the request, I accepted the peering connection.

Once accepted, the status changed to:

```plaintext
Active
```

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/dcb5c5e4-9e19-4433-b3d1-977b5ae6b2e2.png align="center")

## Step 3: Update the Route Tables

Creating a peering connection alone doesn't allow communication between VPCs.

I updated the route tables in both VPCs by adding routes for each other's CIDR blocks.

### Public VPC Route Table

<table style="min-width: 50px;"><colgroup><col style="min-width: 25px;"><col style="min-width: 25px;"></colgroup><tbody><tr><td colspan="1" rowspan="1"><p>Destination</p></td><td colspan="1" rowspan="1"><p>Target</p></td></tr><tr><td colspan="1" rowspan="1"><p>10.1.0.0/16</p></td><td colspan="1" rowspan="1"><p>nautilus-vpc-peering</p></td></tr></tbody></table>

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/fd60b94c-c8df-43cc-9044-cb7365e516e9.png align="center")

### Private VPC Route Table

<table style="min-width: 50px;"><colgroup><col style="min-width: 25px;"><col style="min-width: 25px;"></colgroup><tbody><tr><td colspan="1" rowspan="1"><p>Destination</p></td><td colspan="1" rowspan="1"><p>Target</p></td></tr><tr><td colspan="1" rowspan="1"><p>Default VPC CIDR</p></td><td colspan="1" rowspan="1"><p>nautilus-vpc-peering</p></td></tr></tbody></table>

These routes ensure that traffic between the two VPCs is forwarded through the VPC Peering connection.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/80b6b0ec-ad8f-4930-9b37-cc4ef9c88f12.png align="center")

## Step 4: Configure the Security Groups

To allow communication between the EC2 instances, I updated the Security Group attached to the private EC2 instance.

The following inbound rules were added:

<table style="min-width: 75px;"><colgroup><col style="min-width: 25px;"><col style="min-width: 25px;"><col style="min-width: 25px;"></colgroup><tbody><tr><td colspan="1" rowspan="1"><p>Protocol</p></td><td colspan="1" rowspan="1"><p>Port</p></td><td colspan="1" rowspan="1"><p>Source</p></td></tr><tr><td colspan="1" rowspan="1"><p>ICMP</p></td><td colspan="1" rowspan="1"><p>All</p></td><td colspan="1" rowspan="1"><p>Default VPC CIDR</p></td></tr><tr><td colspan="1" rowspan="1"><p>SSH (if required)</p></td><td colspan="1" rowspan="1"><p>22</p></td><td colspan="1" rowspan="1"><p>Default VPC CIDR</p></td></tr></tbody></table>

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/ed557267-42a5-4612-8ce3-80c883c3a116.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/f065d5f1-a6a4-4dff-8ad1-81f661122ede.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/2515e268-60a7-4fe9-a849-b9b84cd37090.png align="center")

## Step 5: Configure SSH Access

The lab required SSH access from the AWS client host to the public EC2 instance.

I copied the public key located at:

```plaintext
/root/.ssh/id_rsa.pub
```

and added it to the following file on the public EC2 instance:

```plaintext
~/.ssh/authorized_keys
```

This enabled passwordless SSH access from the AWS client host.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/e8b89ac4-acc2-434e-afe2-ca80494ef0ed.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/3385754a-c34c-4841-a76a-f10987730dd4.png align="center")

## Step 6: Verify Connectivity

Finally, I connected to the public EC2 instance using SSH.

```plaintext
ssh ec2-user@<Public-IP>
```

From the public EC2 instance, I pinged the private EC2 instance using its private IP address.

```plaintext
ping <Private-EC2-IP>
```

The ping responses confirmed that communication between the two VPCs was working successfully through the VPC Peering connection

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/4047d2c4-7007-41b5-bf26-f501818c7e95.png align="center")

### What I Learned

This lab helped me understand that **creating a VPC Peering connection is only one part of the setup**.

For communication to work successfully, route tables must be updated in both VPCs, and the Security Groups must explicitly allow the required traffic. Missing any one of these configurations can prevent connectivity, even if the peering connection is active.

I also learned how VPC Peering enables secure communication between isolated networks without exposing resources to the public internet.

## Conclusion

Day 29 provided hands-on experience with AWS networking by configuring a VPC Peering connection between a public and a private VPC.

By updating route tables, configuring Security Groups, and verifying connectivity between two EC2 instances, I gained a better understanding of how AWS enables secure communication across multiple VPCs. This is a common networking pattern used in production environments where applications are distributed across isolated VPCs while still requiring private communication.
---
title: "AWS Day 45: Configure NAT Gateway for Internet Access in a Private VPC"
seoTitle: "AWS NAT Gateway: Private Subnet Internet Access"
seoDescription: "Learn how to configure an AWS NAT Gateway, Internet Gateway, public subnet, route tables, and Elastic IP to provide internet access "
datePublished: 2026-08-21T18:01:24.461Z
cuid: cmt39a3td00000agsewc2cdze
slug: aws-day-45-configure-nat-gateway-for-internet-access-in-a-private-vpc
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/101e9112-5a5b-4e14-a2ee-1302942ddeef.png
tags: aws, vpc, kodekloud, kodekloudengineer, anand-raval

---

As part of my **KodeKloud 100 Days of Cloud** journey, Day 45 focused on configuring a **NAT Gateway** to provide outbound internet access to an EC2 instance running inside a private subnet.

The objective of this lab was to understand how resources in a private subnet can access the internet without being directly exposed to inbound internet traffic.

The existing environment already contained a VPC and a private EC2 instance. My task was to build the required public networking components, configure the NAT Gateway, update the private route table, and verify connectivity by checking for a test file uploaded from the private EC2 instance to an S3 bucket.

## Step 1: Use the Existing VPC

The VPC was already available:

```plaintext
datacenter-priv-vpc
```

Its IPv4 CIDR was:

```plaintext
10.1.0.0/16
```

The existing private subnet was also already created.

Therefore, I did not create another VPC or modify the existing private subnet.

Instead, I created the additional public networking components inside the same VPC.

The resulting structure would be:

```plaintext
datacenter-priv-vpc
CIDR: 10.1.0.0/16
```

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/573a4ffe-a947-4d9e-9a76-074db33c09d8.png align="center")

## Step 2: Create the Public Subnet

I opened:

**AWS Console → VPC → Subnets → Create subnet**

For the VPC, I selected:

```plaintext
datacenter-priv-vpc
```

The subnet was named:

```plaintext
datacenter-pub-subnet
```

The subnet must use an IPv4 CIDR block that is inside the VPC CIDR and does not overlap with the existing private subnet.

The Availability Zone can be selected according to the lab's networking requirements.

The important point is that this subnet will become the **public subnet used by the NAT Gateway**.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/bac14861-4123-47ef-a445-b61e732a1e82.png align="center")

## Step 3: Create the Internet Gateway

Next, I opened:

**VPC → Internet Gateways → Create internet gateway**

I created an Internet Gateway named:

```plaintext
datacenter-ig
```

The Internet Gateway is the component that provides a path between the VPC and the public internet.

However, simply creating an Internet Gateway is not enough.

It must also be **attached to the VPC**.

I attached:

```plaintext
datacenter-ig
        |
        v
datacenter-priv-vpc
```

After attachment, the VPC had a gateway capable of providing internet connectivity to subnets whose route tables point to it.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/c094fad2-a990-4a1e-a8a3-bd0c1adbf7ba.png align="center")

## Step 4: Create the Public Route Table

I then opened:

**VPC → Route Tables → Create route table**

The route table was named:

```plaintext
datacenter-pub-rt
```

I associated it with:

```plaintext
datacenter-priv-vpc
```

A route table determines where network traffic from associated subnets should be sent.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/50e6d272-f67a-4d30-ae70-3431737dcffa.png align="center")

## Step 5: Add the Internet Gateway Route

After creating the public route table, I added the default route:

```plaintext
Destination : 0.0.0.0/0
Target      : Internet Gateway
```

The route table therefore contained:

```plaintext
Destination     Target
10.1.0.0/16     local
0.0.0.0/0       datacenter-ig
```

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/f8726164-52d4-4a4a-a5b7-f4b5a05b1910.png align="center")

## Step 6: Create the NAT Gateway

With the public subnet and Internet Gateway configured, I created the NAT Gateway.

I opened:

**VPC → NAT Gateways → Create NAT Gateway**

The NAT Gateway was named:

```plaintext
datacenter-natgw
```

For the connectivity type, I selected:

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/a951aa75-afee-4b48-ad2c-f4b3ecc7a440.png align="center")

## Step 7: Allocate an Elastic IP

A public NAT Gateway requires a public IP address.

For the NAT Gateway, I selected the automatic Elastic IP allocation option.

The resulting architecture was:

```plaintext
NAT Gateway
    |
    v
Elastic IP
    |
    v
Internet Gateway
    |
    v
Internet
```

The Elastic IP provides a stable public IPv4 address for the NAT Gateway.

The private EC2 instance does **not** receive this public IP.

Instead, the NAT Gateway uses the public address when communicating with external destinations.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/5a638cc4-eb86-493e-8d15-ec80a85570d7.png align="center")

## Step 8: Place the NAT Gateway in the Public Subnet

The NAT Gateway was created in:

```plaintext
datacenter-pub-subnet
```

This is one of the most important parts of the configuration.

A NAT Gateway used for public internet access needs to be reachable through a route to an Internet Gateway.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/bc93820f-31f7-4ea5-ad64-ee27cf282165.png align="center")

## Step 9: Update the Private Route Table

The next and most important configuration was modifying the route table associated with the existing private subnet.

The private route table already had the local VPC route:

```plaintext
10.1.0.0/16 → local
```

I added the default route:

```plaintext
0.0.0.0/0 → NAT Gateway
```

The resulting private route table was:

```plaintext
Destination     Target
10.1.0.0/16     local
0.0.0.0/0       NAT Gateway
```

This single route is what tells the private EC2 instance:

> For any destination outside the VPC, send the traffic to the NAT Gateway.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/b6803063-4fbb-43b3-8932-d779240e4104.png align="center")

## Step 10: Verify the Private Route

Before testing the application, I verified that the private route table contained:

```plaintext
0.0.0.0/0
        |
        v
NAT Gateway
```

This is essential.

If the private route table instead pointed to the Internet Gateway:

```plaintext
0.0.0.0/0 → Internet Gateway
```

the private instance would not suddenly become internet-enabled because an Internet Gateway requires the instance to have a public IPv4 address for direct internet communication.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/6e6687ba-1442-446a-8c38-ba3c459a8749.png align="center")

## Conclusion

Day 45 focused on understanding one of the most common AWS VPC architectures: **providing outbound internet access to private resources using a NAT Gateway**.

I used the existing `datacenter-priv-vpc` and created a new public subnet named `datacenter-pub-subnet`. I then created and attached the `datacenter-ig` Internet Gateway and configured the `datacenter-pub-rt` route table with a default route to the Internet Gateway.

Next, I created the `datacenter-natgw` NAT Gateway in the public subnet and allocated an Elastic IP for it.
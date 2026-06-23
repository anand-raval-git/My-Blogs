---
title: "AWS Day 15: Creating an Amazon EBS Volume Snapshot | KodeKloud 100 Days of Cloud"
seoTitle: "AWS Day 15: Creating an EBS Volume Snapshot"
seoDescription: "Learn how to create an Amazon EBS snapshot in AWS, verify its status, and understand its role in backup and disaster recovery strategies."
datePublished: 2026-06-21T12:55:10.672Z
cuid: cmqnshbud00000bjk45y13x4p
slug: aws-day-15-creating-an-amazon-ebs-volume-snapshot-kodekloud-100-days-of-cloud
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/5463a85c-d1ae-41bf-9977-dfc6ad6dabbf.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/9ac800fd-1727-47c9-8fb2-f7fc2184843a.png
tags: aws, devops, ebs, kodekloud, 100daysofcloudaws

---

## Introduction

During Day 15 of the KodeKloud 100 Days of Cloud Challenge, I have done some work in creating Amazon EBS snapshot. It is one of the ways that snapshots can be created in AWS for backing up EBS volumes and recovering data in cases of data loss through deletion, corruption, or failure of infrastructures.

This lab aims at creating a snapshot of an already existing EBS volume known as xfusion-vol within us-east-1 region.

## What is an Amazon EBS Snapshot?

Amazon EBS Snapshot is a backup of an EBS volume that exists in Amazon S3. Amazon EBS Snapshots can be used for:

*   Backing up important data
    
*   Restoring deleted volumes
    
*   Creating new volumes out of existing data
    
*   Disaster Recovery strategies
    
*   Automation of the process of backup
    

## Lab Objective

The requirements of this task were:

*   Creation of a snapshot of the existing EBS volume xfusion-vol
    
*   Name of the snapshot is xfusion-vol-ss
    
*   Description of the snapshot is xfusion Snapshot
    
*   Ensure the status of the snapshot is Completed
    

## Steps Performed

### Step 1: Navigate to the EC2 Dashboard

I opened the AWS Management Console and selected the **us-east-1** region.

### Step 2: Locate the EBS Volume

From the EC2 console:

EC2 → Elastic Block Store → Volumes

I searched for the volume named: xfusion-vol

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1767340322606/716e995f-e4e8-4235-8804-6530893d66f4.png align="left")

### Step 3: Create the Snapshot

I selected the volume and clicked:

```plaintext
Actions → Create Snapshot
```

Then I entered:

| Field | Value |
| --- | --- |
| Name | xfusion-vol-ss |
| Description | xfusion Snapshot |

After verifying the details, I created the snapshot.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/52da0176-b6e7-4796-beb8-1e7b7c1b14bf.png align="center")

### Step 4: Verify Snapshot Creation

I navigated to:

```plaintext
EC2 → Snapshots
```

and monitored the snapshot status.

Initially the status showed:

```plaintext
Pending
```

After a short period, it changed to:

```plaintext
Completed
```

which confirmed that the snapshot was successfully created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1767340509382/2ebef1b8-d99d-4457-a7a0-78af58b715a8.png align="center")

## Conclusion

Day 15 introduced a fundamental AWS backup concept through Amazon EBS Snapshots. Although creating a snapshot is a simple task, it plays a critical role in protecting data and enabling recovery in real-world cloud environments.

As I continue the KodeKloud 100 Days of Cloud Challenge, I am gaining hands-on experience with core AWS services and operational best practices.
---
title: "AWS Day 23: Migrating Data Between S3 Buckets Using AWS CLI | KodeKloud 100 Days of Cloud"
seoTitle: "Day 23: Data Migration Between S3 Buckets Using AWS CLI"
seoDescription: "Day 23: Data Migration Between S3 Buckets Using AWS CLI"
datePublished: 2026-06-22T17:49:47.035Z
cuid: cmqpig1og00000aja03m78u5i
slug: aws-day-23-migrating-data-between-s3-buckets-using-aws-cli-kodekloud-100-days-of-cloud
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/4505a847-84c0-4803-8088-81e737db46ca.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/bd5a7a9f-441d-4474-ad42-f4b0750842ff.png
tags: aws, cloud-computing, devops, kodekloudengineer

---

## Introduction

During Day 23 of the KodeKloud 100 Days of Cloud Challenge, I worked on a practical data migration task using Amazon S3 and AWS CLI.

Data migration is a common activity in cloud environments. Organizations often need to move data between S3 buckets due to application migrations, environment changes, backup strategies, or restructuring of storage resources. In such cases, ensuring that all files are transferred successfully without data loss is critical.

In this lab, the goal was to create a new private S3 bucket and migrate all data from an existing bucket using AWS CLI.

## Lab Objective

The requirements for this task were:

*   Create a new private S3 bucket named **datacenter-sync-6301**
    
*   Copy all data from **datacenter-s3-25933**
    
*   Use AWS CLI for the migration process
    
*   Verify that both buckets contain the same data after migration
    

## Steps Performed

### Step 1: Verify the Existing Bucket

Before starting the migration, I checked the contents of the source bucket.

```plaintext
aws s3 ls s3://datacenter-s3-25933
```

This allowed me to confirm that the source bucket contained the files that needed to be migrated.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/0b5359ce-e602-4510-b05b-4a358f51c687.png align="center")

### Step 2: Create the Destination Bucket

I created a new private S3 bucket named:

```plaintext
datacenter-sync-6301
```

Using AWS CLI:

```plaintext
aws s3 mb s3://datacenter-sync-6301
```

After creation, I verified that the bucket was successfully created.

### Step 3: Migrate Data Using AWS CLI

To migrate all files from the source bucket to the destination bucket, I used the following command:

```plaintext
aws s3 sync s3://datacenter-s3-25933 s3://datacenter-sync-6301
```

AWS CLI started comparing the buckets and transferred all objects to the new bucket.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/a7771f73-c57d-4e7a-a655-2f06f649ce59.png align="center")

### Step 4: Verify Data Migration

Once the sync operation completed, I verified the contents of both buckets.

Source bucket:

```plaintext
aws s3 ls s3://datacenter-s3-25933 --recursive
```

Destination bucket:

```plaintext
aws s3 ls s3://datacenter-sync-6301 --recursive
```

I compared the results and confirmed that the files existed in both locations.

### Step 5: Validate Data Consistency

To ensure the migration was successful, I checked:

*   Total number of objects
    
*   Folder structure
    
*   File names
    
*   Overall data consistency
    

After verification, both buckets contained the same data, confirming that the migration had completed successfully.

## What I Learned

This lab demonstrated how powerful AWS CLI can be for managing S3 data.

Instead of manually downloading and uploading files, a single `aws s3 sync` command can migrate large amounts of data efficiently.

I also learned the importance of verifying the destination bucket after migration to ensure that no files were missed during the transfer process.

## Real-World Usage

In production environments, S3 bucket migrations are commonly performed when:

*   Moving data between environments
    
*   Migrating applications
    
*   Creating backups
    
*   Consolidating storage resources
    
*   Implementing disaster recovery strategies
    

The `aws s3 sync` command is widely used because it automates the transfer process and minimizes manual effort.

## Conclusion

Day 23 introduced a practical data migration scenario using Amazon S3 and AWS CLI.

By creating a new bucket and synchronizing data from an existing bucket, I gained hands-on experience with one of the most commonly used AWS CLI commands. Understanding how to migrate and validate data is an essential skill for cloud and DevOps engineers working with AWS storage services.

As I continue the KodeKloud 100 Days of Cloud Challenge, I am gaining valuable experience with real-world AWS operations and automation workflows.
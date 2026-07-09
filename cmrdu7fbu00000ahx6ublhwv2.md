---
title: "AWS Day 32: Backup and Restore an Amazon RDS Instance Using Snapshots | KodeKloud 100 Days of Cloud"
seoTitle: "AWS Day 32: Backup & Restore Amazon RDS Snapshot"
seoDescription: "Learn how to create and restore an Amazon RDS snapshot in AWS. This hands-on KodeKloud Day 32 guide covers RDS backups, snapshot restoration, disaster recovery, and database best practices using MySQL.

Tags"
datePublished: 2026-07-09T18:25:28.437Z
cuid: cmrdu7fbu00000ahx6ublhwv2
slug: aws-day-32-backup-and-restore-an-amazon-rds-instance-using-snapshots-kodekloud-100-days-of-cloud
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/0e6e05d7-82b3-498c-92a3-4d7058e88dfa.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/976986d1-a0fb-4bc2-94ba-704a731e3807.png
tags: aws, rds, kodekloud, anand-raval

---

## Protecting an Amazon RDS Database with Snapshots

One of the most important responsibilities in cloud infrastructure is making sure that critical data can be recovered if something goes wrong. Whether it's accidental deletion, a failed deployment, or database corruption, having a recent backup can significantly reduce downtime.

During **Day 32 of the KodeKloud 100 Days of Cloud Challenge**, I explored how **Amazon RDS Snapshots** work by creating a manual snapshot of an existing MySQL database and restoring it as a completely new RDS instance.

This lab demonstrates a common backup and recovery workflow that many DevOps engineers perform before major database upgrades, application releases, or migration activities.

## Why Are RDS Snapshots Important?

Amazon RDS snapshots are point-in-time backups of your database that are stored securely in Amazon S3 behind the scenes. Unlike automated backups, manual snapshots remain available until you delete them.

RDS snapshots are commonly used for:

*   Creating reliable database backups
    
*   Restoring data after accidental deletion
    
*   Testing application changes safely
    
*   Cloning production databases for development
    
*   Disaster recovery planning
    
*   Database migration between environments
    

Having a backup strategy is considered one of the fundamental best practices when managing production databases on AWS.

## Lab Objective

The goal of this lab was to complete the following tasks:

*   Create a manual snapshot of the existing RDS instance **xfusion-rds**
    
*   Name the snapshot **xfusion-snapshot**
    
*   Restore the snapshot to a new RDS instance named **xfusion-snapshot-restore**
    
*   Use the **db.t3.micro** instance class
    
*   Verify that the restored database reaches the **Available** state
    

### Step 1: Create a Manual Snapshot

After confirming that the **xfusion-rds** database was in the **Available** state, I selected the database from the Amazon RDS console.

From the **Actions** menu, I clicked **Take Snapshot** to begin creating a manual backup.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/c57c4c44-a6e1-4204-8152-32ea1bd568a4.png align="center")

### Step 2: Configure the Snapshot

Next, I entered the required snapshot details.

| Setting | Value |
| --- | --- |
| Source Database | xfusion-rds |
| Snapshot Name | xfusion-snapshot |

After verifying the information, I clicked **Take Snapshot**.

AWS immediately started creating the backup in the background.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/95e440e2-280d-4b03-8fd6-8af7d0d3f296.png align="center")

### Step 3: Restore the Snapshot

Once the snapshot creation was complete, I opened the **Snapshots** section, selected **xfusion-snapshot**, and chose **Restore Snapshot** from the **Actions** menu.

This launches the RDS restoration wizard, allowing a completely new database instance to be created using the backup.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/d097a701-05a1-4cfd-bf69-a55fb282779b.png align="center")

### Step 4: Configure the Restored Database

During the restore process, I configured the new database instance with the required settings.

| Setting | Value |
| --- | --- |
| DB Instance Identifier | xfusion-snapshot-restore |
| Instance Class | db.t3.micro |

The remaining settings were left at their default values, and I started the restore process.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/d8bc703c-5d58-4943-a9b9-e9eda01c6430.png align="center")

### Step 5: Verify the Restored RDS Instance

After waiting a few minutes, AWS finished provisioning the new database.

Returning to the **Databases** page, I verified that both database instances were available.

*   **xfusion-rds**
    
*   **xfusion-snapshot-restore**
    

Both instances displayed the **Available** status, confirming that the snapshot restoration completed successfully.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/cd96bdfe-f706-40a2-8a6f-e50f83154722.png align="center")

## What I Learned

This lab helped me understand how simple and reliable Amazon RDS backup and recovery can be.

Some important takeaways from this exercise include:

*   Manual snapshots remain available until they are deleted.
    
*   A snapshot can be restored as a completely new database without affecting the original instance.
    
*   Restoring from snapshots is useful for testing, migration, and disaster recovery.
    
*   Creating backups before making major database changes is a recommended DevOps practice.
    

Even though AWS automates most of the process, knowing when and how to use snapshots is an essential skill for anyone working with production databases.

## Conclusion

Day 32 provided practical experience with one of the most important database administration tasks on AWS **backing up and restoring an Amazon RDS instance**.

By creating a manual snapshot, restoring it as a new database, and verifying that both instances were available, I gained a better understanding of how AWS simplifies database recovery while helping teams protect critical application data.

Every cloud engineer should be comfortable with this workflow because backup and recovery are essential parts of running reliable applications in production.
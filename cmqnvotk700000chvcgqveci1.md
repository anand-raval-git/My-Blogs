---
title: "AWS Day 17: Creating an IAM Group | KodeKloud 100 Days of Cloud"
seoTitle: "AWS Day 17: Creating an IAM Group | KodeKloud Challenge"
seoDescription: "Learn how to create an IAM Group in AWS and understand its role in managing user permissions as part of Day 17 of the KodeKloud Cloud Challenge."
datePublished: 2026-06-21T14:24:59.076Z
cuid: cmqnvotk700000chvcgqveci1
slug: aws-day-17-creating-an-iam-group-kodekloud-100-days-of-cloud
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/46908dc9-5e48-4c67-a629-77bc7958d7ef.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/9852b4d7-209a-46eb-9dc9-16117d740fa7.png
tags: aws, iam, kodekloud, 100daysofcloudaws, anand-raval

---

## Introduction

During Day 17 of the KodeKloud 100 Days of Cloud Challenge, I worked with another important IAM feature in AWS: IAM Groups.

In the previous lab, I created an IAM user. However, managing permissions individually for every user can become difficult as the number of users grows. AWS IAM Groups help solve this problem by allowing multiple users to be managed together and assigned permissions as a group.

In this lab, the objective was to create an IAM group named **iamgroup\_kirsty**.

## What is an IAM Group?

An IAM Group is a collection of IAM users.

Instead of attaching permissions to each user separately, permissions can be assigned to a group, and all users within that group inherit those permissions automatically.

IAM Groups are commonly used to organize users based on their roles, such as:

*   Developers
    
*   DevOps Engineers
    
*   Database Administrators
    
*   Security Teams
    
*   Read-Only Users
    

This makes permission management much easier in larger AWS environments.

## Lab Objective

The requirement for this task was straightforward:

*   Create an IAM group named **iamgroup\_kirsty**
    

## Steps Performed

### Step 1: Open the IAM Console

I logged in to the AWS Management Console and searched for IAM.

From the AWS services menu, I opened the IAM Dashboard.

### Step 2: Navigate to User Groups

From the left navigation menu, I selected:

```plaintext
IAM → User Groups
```

This section displays all existing IAM groups within the AWS account.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1767341398673/fdf49c1a-0702-43c7-84f4-d0bbd9fad2e8.png align="center")

### Step 3: Create the IAM Group

I clicked on **Create Group** and entered the following details:

| Field | Value |
| --- | --- |
| Group Name | iamgroup\_kirsty |

For this lab, no policies needed to be attached. After reviewing the information, I created the group.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1767341460395/a7c82afb-c581-486c-8e44-849e3555e085.png align="center")

### Step 4: Verify Group Creation

After the group was created, I checked the User Groups section and confirmed that **iamgroup\_kirsty** appeared in the list.

This verified that the task had been completed successfully.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1767341476359/db30d2f7-d8b5-4ef0-9105-130d37b6d4a3.png align="center")

## What I Learned

This lab helped me understand why IAM Groups are useful when managing multiple users.

Creating a group may seem like a small task, but it becomes extremely valuable when an organization has dozens or even hundreds of users. Instead of updating permissions user by user, administrators can manage permissions at the group level.

This approach reduces operational effort and helps maintain consistent access control across teams.

## Real-World Usage

In production AWS environments, IAM Groups are commonly used to organize users based on their job responsibilities.

For example:

*   Developers may belong to a Developer Group
    
*   DevOps Engineers may belong to a DevOps Group
    
*   Auditors may belong to a ReadOnly Group
    

Permissions are assigned to the group, and every member automatically receives the appropriate access level.

This approach follows AWS security best practices and simplifies user management.

## Conclusion

Day 17 introduced IAM Groups, an important feature for managing user permissions efficiently in AWS.

While the task only involved creating a single group, it demonstrated how AWS helps organizations scale access management as teams grow. Understanding IAM users and groups is a key step toward building secure and well-organized AWS environments.

As I continue the KodeKloud 100 Days of Cloud Challenge, I am gaining hands-on experience with the core AWS services that are used daily in real-world cloud infrastructure.
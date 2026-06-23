---
title: "AWS Day 16: Creating an IAM User | KodeKloud 100 Days of Cloud"
seoTitle: "AWS Day 16: Creating an IAM User | KodeKloud Challenge"
seoDescription: "Learn how to create an IAM user in AWS as part of Day 16 of the KodeKloud 100 Days of Cloud Challenge. A beginner-friendly IAM hands-on walkthrough."
datePublished: 2026-06-21T14:17:34.492Z
cuid: cmqnvfail00000bjc654i2j47
slug: aws-day-16-creating-an-iam-user-kodekloud-100-days-of-cloud
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/c95f7b4b-45ea-4b2b-91c7-3d027eab10bc.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/99ac1fa3-5c0e-4554-a0da-649b4fdf6ffe.png
tags: aws, iam, kodekloud, 100daysofcloudaws, anand-raval

---

During Day 16 of the KodeKloud 100 Days of Cloud Challenge, I worked with AWS Identity and Access Management (IAM), one of the most important services in AWS.

Whenever we create infrastructure in AWS, managing access becomes a critical task. Instead of sharing the root account with everyone, AWS provides IAM to create users and control what actions they can perform.

In this lab, the objective was simple: create a new IAM user named **iamuser\_james**.

## What is AWS IAM?

AWS Identity and Access Management (IAM) is a service that helps manage access to AWS resources securely.

Using IAM, we can:

*   Create users for different team members
    
*   Assign permissions through policies
    
*   Organize users into groups
    
*   Create roles for services and applications
    
*   Follow security best practices by avoiding root account usage
    

One thing I have noticed while learning AWS is that IAM is usually one of the first services configured in a new AWS account because every other service depends on proper access control.

## Lab Objective

The requirement for this task was straightforward:

*   Create an IAM user named **iamuser\_james**
    

## Steps Performed

### Step 1: Open the IAM Console

I logged in to the AWS Management Console and searched for **IAM**.

From the AWS services menu, I opened the IAM Dashboard.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1767341094874/92ac0407-6988-4126-ad98-0b63c2d79425.png align="center")

### Step 2: Navigate to Users

From the left navigation menu, I selected:

```plaintext
IAM → Users
```

This section displays all IAM users available in the account.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1767341136379/7673c5c2-4e80-4d16-bd3f-e3c5fe2832a3.png align="center")

### Step 3: Create the IAM User

I clicked on **Create User** and entered the following details:

| Field | Value |
| --- | --- |
| User Name | iamuser\_james |

After reviewing the information, I proceeded with the user creation process.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1767341203947/2dfde802-1c9f-4273-9379-4147295fec2d.png align="center")

### Step 4: Verify User Creation

Once the user was created, I verified that **iamuser\_james** appeared in the Users list.

This confirmed that the task was completed successfully.

## What I Learned

Although this was a simple task, it reinforced an important AWS concept.

Instead of using the root account for daily operations, IAM users should be created for individuals who need access to AWS resources.

In real-world environments, IAM users are typically assigned permissions through IAM Groups and Policies, ensuring that users only have access to the resources they actually need.

## Real-World Usage

In production environments, organizations often have multiple developers, DevOps engineers, and administrators working within the same AWS account.

IAM helps enforce the principle of least privilege, where each user receives only the permissions required to perform their job.

This improves security and reduces the risk of accidental changes.

## Conclusion

Day 16 introduced another foundational AWS concept through IAM user management.

While creating an IAM user may seem like a small task, it is one of the building blocks of AWS security. Understanding IAM is essential because every AWS service relies on proper authentication and authorization.

As I continue the KodeKloud 100 Days of Cloud Challenge, I am gaining practical experience with the services that form the foundation of cloud infrastructure.
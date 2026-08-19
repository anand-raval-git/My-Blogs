---
title: "AWS Day 42: Building and Managing NoSQL Databases with AWS DynamoDB"
seoTitle: "Day 42 completed: DynamoDB table creation, item insertion"
seoDescription: "Learn how to create a DynamoDB table, configure a partition key, insert items, and verify task data using the AWS Management Console."
datePublished: 2026-08-19T18:31:11.670Z
cuid: cmt0fgpi200000akh50dj7fg9
slug: aws-day-42-building-and-managing-nosql-databases-with-aws-dynamodb
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/ad656e57-713a-4cd2-9f6d-b9afafffc323.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/e899c700-39b7-4b55-bf70-460db93ff313.png
tags: aws, dynamodb, kodekloud, anand-raval

---

As part of my **KodeKloud 100 Days of Cloud** journey, Day 42 focused on working with **Amazon DynamoDB**, AWS's fully managed NoSQL database service.

For this task, the Nautilus DevOps team needed a simple database for a To-Do application. The application required a table where each task could be uniquely identified and additional information such as its description and current status could be stored.

The main requirements were:

*   Create a DynamoDB table named `datacenter-tasks`
    
*   Configure `taskId` as the primary key
    
*   Use `String` as the data type for `taskId`
    
*   Insert two tasks into the table
    
*   Store the task description and status
    
*   Verify that both records were inserted correctly
    
*   Confirm the status of each task
    

This was a straightforward task, but it was useful for understanding how DynamoDB tables, partition keys, items, and attributes work.

## Step 1: Open DynamoDB

I opened the AWS Management Console and navigated to:

**AWS Console → DynamoDB → Tables**

From the Tables section, I selected:

**Create table**

AWS provides a simple interface for creating the table and defining its primary key.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/cf9b9b2d-9f0a-47ac-b818-6e27cf0a5130.png align="center")

## Step 2: Create the DynamoDB Table

Under **Table name**, I entered:

```plaintext
datacenter-tasks
```

For the partition key, I entered:

```plaintext
taskId
```

I selected:

```plaintext
String
```

as the data type.

The configuration was:

```plaintext
Table name  : datacenter-tasks
Partition key: taskId
Type        : String
Sort key    : Not configured
```

I did not configure a sort key because the task only required `taskId` to uniquely identify each task.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/8d436390-4cbb-43d9-a210-6c80fc4dbe62.png align="center")

## Step 3: Use Default Table Settings

For this lab, I kept the default table settings.

DynamoDB allows advanced configuration options for use cases that require additional control over capacity, backups, encryption, indexes, streams, and other features.

However, none of those additional settings were required for this task.

Using the default settings kept the table configuration simple and focused on the actual application requirement.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/ba2825d1-8869-4d8b-8140-eafc33b563fd.png align="center")

## Step 4: Verify the Table

After creating the table, I opened the `datacenter-tasks` table from the DynamoDB Tables section.

The table showed the following primary key configuration:

```plaintext
Partition key: taskId (String)
Sort key     : -
```

This confirmed that the table was created with the correct primary key.

The table was ready to store the To-Do application records.

* * *

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/1a1c38d7-0d39-4b2e-8a81-a55f96a34a2d.png align="center")

## Step 5: Create the First Task

Next, I opened the table and selected the option to create an item.

For the first item, I entered:

```plaintext
taskId     : 1
description: Learn DynamoDB
status     : completed
```

The item therefore contained three attributes:

<table style="min-width: 75px;"><colgroup><col style="min-width: 25px;"><col style="min-width: 25px;"><col style="min-width: 25px;"></colgroup><tbody><tr><td colspan="1" rowspan="1"><p>Attribute</p></td><td colspan="1" rowspan="1"><p>Value</p></td><td colspan="1" rowspan="1"><p>Type</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>taskId</code></p></td><td colspan="1" rowspan="1"><p><code>1</code></p></td><td colspan="1" rowspan="1"><p>String</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>description</code></p></td><td colspan="1" rowspan="1"><p><code>Learn DynamoDB</code></p></td><td colspan="1" rowspan="1"><p>String</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>status</code></p></td><td colspan="1" rowspan="1"><p><code>completed</code></p></td><td colspan="1" rowspan="1"><p>String</p></td></tr></tbody></table>

I saved the item successfully.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/ae9c2f87-d599-4a39-a593-d6daf4e33663.png align="center")

## DynamoDB vs Traditional Relational Databases

One of the key differences between DynamoDB and relational databases is the data model.

A relational database might have a table such as:

```plaintext
tasks
--------------------------------
id | description | status
--------------------------------
1  | Learn ...   | completed
2  | Build ...   | in-progress
```

DynamoDB instead stores each record as an item containing attributes.

For example:

```plaintext
{
  "taskId": "1",
  "description": "Learn DynamoDB",
  "status": "completed"
}
```

This model makes DynamoDB particularly useful for applications where flexible attributes and predictable key-based access are important.

## Conclusion

Day 42 focused on building a simple task management database using **Amazon DynamoDB**.

I created the `datacenter-tasks` table with `taskId` as the String partition key, then inserted two task records:

```plaintext
Task 1 → Learn DynamoDB → completed
Task 2 → Build To-Do App → in-progress
```

After inserting the records, I used the DynamoDB console to verify that both items were present and that their statuses matched the requirements.

Although this was a simple lab, it provided practical experience with the core DynamoDB concepts that are important when building serverless and cloud-native applications.

The key lesson from this task was that DynamoDB table design should be driven by **access patterns, partition-key design, scalability, and application requirements** rather than by simply trying to model a relational database in a NoSQL service.

Another AWS task completed in my **KodeKloud 100 Days of Cloud** journey, with a better understanding of how DynamoDB can be used to build scalable NoSQL applications.

* * *
---
title: "AWS Day 25: Monitoring EC2 CPU Utilization with CloudWatch Alarms | Kodekloud Challenge"
seoTitle: "Monitoring EC2 CPU Utilization with CloudWatch Alarms "
seoDescription: "Learn how to create a CloudWatch Alarm for EC2 CPU Utilization in AWS. Step-by-step guide covering EC2 monitoring, SNS notifications."
datePublished: 2026-06-24T17:59:18.897Z
cuid: cmqsdo09000000ajr2rmc7sbi
slug: aws-day-25-monitoring-ec2-cpu-utilization-with-cloudwatch-alarms-kodekloud-challenge
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/401c5563-582f-4e80-9df3-a2bf2ae8a7f6.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/340850af-9801-4525-8cc1-54f3887a3fcc.png
tags: aws, amazon-ec2, cloudwatch, kodekloud, anand-raval

---

## Introduction

During Day 25 of the KodeKloud 100 Days of Cloud Challenge, I worked with two essential AWS services: Amazon EC2 and Amazon CloudWatch.

Launching an EC2 instance is usually the easy part. The real challenge begins when you need to monitor the health and performance of your infrastructure. In production environments, high CPU usage can impact application performance and user experience. This is where CloudWatch Alarms become useful.

In this lab, I launched an EC2 instance and configured a CloudWatch Alarm to notify the team whenever CPU utilization exceeded 90%.

## Why CloudWatch Alarms Matter

Amazon CloudWatch continuously monitors AWS resources and allows us to create alarms based on specific metrics.

Some common use cases include:

*   High CPU utilization alerts
    
*   Low disk space notifications
    
*   Memory monitoring
    
*   Application health monitoring
    
*   Automated scaling decisions
    

For this task, the alarm was configured to monitor CPU Utilization on an EC2 instance.

## Task Requirements

The following resources needed to be configured:

*   Create an EC2 instance named **devops-ec2**
    
*   Use an Ubuntu AMI
    
*   Create a CloudWatch Alarm named **devops-alarm**
    
*   Monitor **CPU Utilization**
    
*   Trigger the alarm when CPU usage is greater than or equal to 90%
    
*   Evaluation period: 1 consecutive period of 5 minutes
    
*   Send notifications through the SNS topic **devops-sns-topic**
    

## Step 1: Launch an EC2 Instance

I started by navigating to the EC2 Dashboard and selecting **Launch Instance**.

For the instance configuration:

| Setting | Value |
| --- | --- |
| Name | devops-ec2 |
| AMI | Ubuntu |
| Instance Type | t2.micro (default) |

After reviewing the configuration, I launched the instance successfully.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/c0365106-4017-45b4-b186-c303e927d781.png align="center")

## Step 2: Verify the EC2 Instance

Once the instance was launched, I confirmed that its status changed to:

```plaintext
Running
```

This verified that the EC2 instance was available for monitoring.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/20b89bde-5219-4894-90bf-d34ae4dc2dac.png align="center")

## Step 3: Navigate to CloudWatch

Next, I opened the CloudWatch Console and selected:

```plaintext
CloudWatch → Alarms
```

Then clicked:

```plaintext
Create Alarm
```

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/6dafef02-e50b-4055-a28a-49dcf1b7b79a.png align="center")

## Step 4: Select the CPU Utilization Metric

To monitor CPU usage, I selected:

```plaintext
EC2 → Per-Instance Metrics → CPUUtilization
```

Then I chose the metric associated with the **devops-ec2** instance.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/51c1dc46-ae07-4a74-8406-e1a22c3e12d2.png align="center")

## Step 5: Configure the Alarm Threshold

The alarm was configured using the following settings:

<table style="min-width: 50px;"><colgroup><col style="min-width: 25px;"><col style="min-width: 25px;"></colgroup><tbody><tr><td colspan="1" rowspan="1"><p>Setting</p></td><td colspan="1" rowspan="1"><p>Value</p></td></tr><tr><td colspan="1" rowspan="1"><p>Metric</p></td><td colspan="1" rowspan="1"><p>CPU Utilization</p></td></tr><tr><td colspan="1" rowspan="1"><p>Statistic</p></td><td colspan="1" rowspan="1"><p>Average</p></td></tr><tr><td colspan="1" rowspan="1"><p>Threshold Type</p></td><td colspan="1" rowspan="1"><p>Static</p></td></tr><tr><td colspan="1" rowspan="1"><p>Condition</p></td><td colspan="1" rowspan="1"><p>Greater than or equal to</p></td></tr><tr><td colspan="1" rowspan="1"><p>Threshold Value</p></td><td colspan="1" rowspan="1"><p>90</p></td></tr><tr><td colspan="1" rowspan="1"><p>Evaluation Period</p></td><td colspan="1" rowspan="1"><p>1</p></td></tr><tr><td colspan="1" rowspan="1"><p>Period</p></td><td colspan="1" rowspan="1"><p>5 Minutes</p></td></tr></tbody></table>

This configuration ensures that the alarm triggers if CPU utilization remains above 90% for one consecutive 5-minute period.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/629e1b7d-6a0f-47ee-b8ef-2cc2363e7f6b.png align="center")

## Step 6: Configure SNS Notifications

For notifications, I selected the existing SNS topic:

```plaintext
devops-sns-topic
```

This allows CloudWatch to send alerts whenever the alarm enters the ALARM state.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/934ea65c-5ece-4264-9d62-5fa55653cf76.png align="center")

## Step 7: Create the CloudWatch Alarm

Finally, I provided the alarm name:

```plaintext
devops-alarm
```

After reviewing the configuration, I created the alarm successfully.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/8bf859e6-0c33-41e3-8484-003785a97e3d.png align="center")

## Verifying the Configuration

After the alarm was created, it appeared in the CloudWatch Alarms dashboard.

The alarm state initially showed:

```plaintext
OK
```

This indicated that CPU utilization was below the configured threshold and monitoring was working correctly.

## What I Learned

This challenge helped me understand that monitoring is just as important as deploying infrastructure.

Creating an EC2 instance only provides compute resources. To maintain reliability and performance, we also need visibility into system metrics. CloudWatch Alarms make it possible to proactively detect issues before they impact applications.

I also learned how SNS integrates with CloudWatch to deliver notifications automatically whenever a threshold is breached.

## Conclusion

Day 25 introduced a practical monitoring use case using Amazon EC2, Amazon CloudWatch, and Amazon SNS.

By creating a CPU Utilization alarm, I gained hands-on experience with AWS monitoring and alerting. These services play an important role in production environments where quick detection and response to performance issues are critical for maintaining application availability.
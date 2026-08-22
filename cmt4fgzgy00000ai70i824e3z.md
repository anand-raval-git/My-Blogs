---
title: "AWS Day 46: Event-Driven Processing with Amazon S3 and Lambda"
seoTitle: "AWS Day 46: S3 Event-Driven Processing with Lambda"
seoDescription: "Learn how to build an event-driven AWS workflow using S3, Lambda, IAM, and DynamoDB to automatically copy uploaded files to a private S3 bucket"
datePublished: 2026-08-22T13:42:29.293Z
cuid: cmt4fgzgy00000ai70i824e3z
slug: aws-day-46-event-driven-processing-with-amazon-s3-and-lambda
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/27ab29dc-f8cd-401b-957e-89b2409db976.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/f8d68289-448d-47b0-8daf-525c7aafbeed.png
tags: aws, dynamodb, s3, kodekloudengineer, anand-raval

---

As part of my **KodeKloud 100 Days of Cloud** journey, Day 46 focused on building an **event-driven file processing workflow using Amazon S3, AWS Lambda, and Amazon DynamoDB**.

The objective was to automate file movement between two S3 buckets. Whenever a file was uploaded to a public S3 bucket, an S3 event notification would automatically trigger a Lambda function. The Lambda function would then copy the uploaded object to a private S3 bucket and record the operation details in DynamoDB.

This lab demonstrated how AWS managed services can be combined to create an automated workflow without requiring a continuously running server.

## Step 1: Create the Public S3 Bucket

I started by opening:

**AWS Console → S3 → Buckets → Create bucket**

The public bucket was named:

```plaintext
nautilus-public-1219
```

The purpose of this bucket was to act as the source location for uploaded files.

The task specifically required public access to the objects in this bucket.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/9cd0de3b-3f5a-4b99-8473-b570476b3bcc.png align="center")

## Step 2: Create the Private S3 Bucket

Next, I created the destination bucket:

```plaintext
nautilus-private-27631
```

This bucket was intentionally configured differently from the source bucket.

The private bucket retained:

```plaintext
Block all public access: Enabled
```

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/b9acaad4-c733-43d9-88a6-b126b75f1172.png align="center")

## Step 3: Create the DynamoDB Table

The next component was Amazon DynamoDB.

I opened:

**AWS Console → DynamoDB → Tables → Create table**

The table name was:

```plaintext
nautilus-S3CopyLogs
```

The partition key was:

```plaintext
LogID
```

The data type was:

```plaintext
String
```

No sort key was required.

The resulting primary key configuration was:

```plaintext
Table Name : nautilus-S3CopyLogs
Partition Key : LogID
Type : String
```

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/b5e25415-41e0-4bef-99b0-742f7a903e76.png align="center")

## Step 6: Configure the Lambda Function Code

The lab provided a Python file under:

```plaintext
/root/lambda_function.py
```

The function uses:

```plaintext
import json
import boto3
from datetime import datetime
import uuid
```

It initializes the AWS service clients:

```plaintext
s3 = boto3.client("s3")
dynamodb = boto3.resource("dynamodb")
table = dynamodb.Table("nautilus-S3CopyLogs")
```

The DynamoDB table is therefore configured as:

```plaintext
nautilus-S3CopyLogs
```

The destination bucket is configured as:

```plaintext
destination_bucket = "nautilus-private-27631"
```

These values connect the Lambda function to the resources created earlier.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/823f39b9-7a9c-4203-b03c-16c9e47c6412.png align="center")

```shell
import json
import boto3
from datetime import datetime
import uuid

# Initialize the S3 and DynamoDB clients
s3 = boto3.client("s3")
dynamodb = boto3.resource("dynamodb")
table = dynamodb.Table("nautilus-S3CopyLogs")


def lambda_handler(event, context):
    try:
        # Get the source bucket and object key from the event
        source_bucket = event["Records"][0]["s3"]["bucket"]["name"]
        object_key = event["Records"][0]["s3"]["object"]["key"]

        # Hardcoded destination bucket name
        destination_bucket = "nautilus-private-27631"

        # Log the event details for debugging
        print(f"[INFO] Source bucket: {source_bucket}, Object key: {object_key}")
        print(f"[INFO] Destination bucket: {destination_bucket}")

        # Copy the file from source bucket to destination bucket
        copy_source = {
            "Bucket": source_bucket,
            "Key": object_key,
        }

        print(
            f"[INFO] Attempting to copy object from {source_bucket}/{object_key} "
            f"to {destination_bucket}/{object_key}"
        )

        s3.copy_object(
            CopySource=copy_source,
            Bucket=destination_bucket,
            Key=object_key,
        )

        print(
            f"[INFO] File successfully copied from "
            f"{source_bucket}/{object_key} "
            f"to {destination_bucket}/{object_key}"
        )

        # Create log entry for DynamoDB
        log_entry = {
            "LogID": str(uuid.uuid4()),
            "SourceBucket": source_bucket,
            "DestinationBucket": destination_bucket,
            "ObjectKey": object_key,
            "Timestamp": datetime.now().strftime("%Y-%m-%d %H:%M:%S"),
            "Status": "Success",
        }

        # Log the log entry before attempting to write to DynamoDB
        print(
            f"[INFO] Writing the following log entry to DynamoDB:\n"
            f"{json.dumps(log_entry, indent=4)}"
        )

        table.put_item(Item=log_entry)

        print("[INFO] Successfully wrote log entry to DynamoDB")

        return {
            "statusCode": 200,
            "body": json.dumps(
                f"File successfully copied to {destination_bucket}"
            ),
        }

    except Exception as e:
        # Store error log in DynamoDB in case of failure
        log_entry = {
            "LogID": str(uuid.uuid4()),
            "SourceBucket": source_bucket,
            "DestinationBucket": destination_bucket,
            "ObjectKey": object_key,
            "Timestamp": datetime.now().strftime("%Y-%m-%d %H:%M:%S"),
            "Status": "Failure",
            "Error": str(e),
        }

        # Log the error log entry before attempting to write to DynamoDB
        print(
            f"[ERROR] Writing the following error log entry to DynamoDB:\n"
            f"{json.dumps(log_entry, indent=4)}"
        )

        try:
            table.put_item(Item=log_entry)
            print("[INFO] Successfully wrote error log entry to DynamoDB")
        except Exception as db_error:
            print(
                f"[ERROR] Failed to write error log entry to DynamoDB: {str(db_error)}"
            )

        # Log the error in CloudWatch
        print(f"[ERROR] Error during file copy or DynamoDB operation: {str(e)}")

        return {
            "statusCode": 500,
            "body": json.dumps(f"Error copying file: {str(e)}"),
        }
```

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/0faeb711-b407-4e0c-ab20-6cc36f4dd432.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/7bbca907-a408-41ea-87bb-cd603dafec04.png align="center")

## Step 7: Understand How Lambda Reads the S3 Event

When an object is uploaded to S3, the event payload contains information about the bucket and object.

The Lambda function extracts the source bucket:

```plaintext
source_bucket = event["Records"][0]["s3"]["bucket"]["name"]
```

It then extracts the object key:

```plaintext
object_key = event["Records"][0]["s3"]["object"]["key"]
```

For this lab, the uploaded object was:

```plaintext
sample.zip
```

So the Lambda function effectively receives:

```plaintext
Source Bucket : nautilus-public-1219
Object Key    : sample.zip
```

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/8f89d752-d41e-4411-aacc-af0bf6d213da.png align="center")

## Step 9: Create the DynamoDB Log Entry

After the S3 copy succeeds, the function creates a log entry.

The code generates a unique identifier:

```plaintext
"LogID": str(uuid.uuid4())
```

It also records:

```plaintext
SourceBucket
DestinationBucket
ObjectKey
Timestamp
Status
```

The status is:

```plaintext
Success
```

The resulting DynamoDB record looks similar to:

```plaintext
{
  "LogID": "77d60216-0afc-45e0-bfcd-7aae031a4ae9",
  "SourceBucket": "nautilus-public-1219",
  "DestinationBucket": "nautilus-private-27631",
  "ObjectKey": "sample.zip",
  "Timestamp": "2026-07-26 14:21:04",
  "Status": "Success"
}
```

The function then writes it using:

```plaintext
table.put_item(Item=log_entry)
```

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/dfa0487b-2cb0-4db3-888d-84c8e20ddb4d.png align="center")

## Final Configuration

```plaintext
Source S3 Bucket
Name            : nautilus-public-1219
Access          : Public as required by lab
Purpose         : File upload source

Destination S3 Bucket
Name            : nautilus-private-27631
Access          : Private
Purpose         : Secure file storage

Lambda
Function        : nautilus-copyfunction
Runtime         : Python 3.14
Execution Role  : lambda_execution_role
Trigger         : S3 Object Created

DynamoDB
Table           : nautilus-S3CopyLogs
Partition Key   : LogID
Key Type        : String

Test File
File            : sample.zip
Source          : nautilus-public-1219
Destination     : nautilus-private-27631
Status          : Success

Logging
Source Bucket      : nautilus-public-1219
Destination Bucket : nautilus-private-27631
Object Key         : sample.zip
Status              : Success
```

Day 46 completed: **Event-driven S3 file processing with AWS Lambda, private S3 storage, IAM permissions, and DynamoDB logging.**
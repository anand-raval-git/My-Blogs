---
title: "AWS Day 34: Create an AWS Lambda Function Using AWS CLI | KodeKloud 100 Days of Cloud"
seoTitle: "AWS Day 34: Create an AWS Lambda Function Using AWS CLI "
seoDescription: "Learn how to create an AWS Lambda function using the AWS CLI. This beginner-friendly guide covers writing Python code"
datePublished: 2026-07-14T18:24:50.852Z
cuid: cmrkzdvnl00000bhy74pl99ly
slug: aws-day-34-create-an-aws-lambda-function-using-aws-cli-kodekloud-100-days-of-cloud
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/d5b18581-1ac4-42b5-9946-a61de6d6b43c.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/dfebad6e-807a-43ae-95f9-baee91ca585e.png
tags: lambda, aws, devops, kodekloudengineer, anand-raval

---

## Introduction

After creating a Lambda function using the AWS Management Console in the previous lab, Day 34 focused on deploying the same serverless application **using the AWS Command Line Interface (AWS CLI)**.

In real-world DevOps environments, infrastructure is rarely created manually through the console. Instead, engineers automate deployments using tools such as the AWS CLI, Terraform, CloudFormation, or CI/CD pipelines.

This lab introduced the complete workflow of creating a Lambda deployment package, uploading it through the AWS CLI, and invoking the function—all without opening the AWS Console.

## Why Use AWS CLI for Lambda?

While the AWS Console is useful for learning and quick testing, the AWS CLI offers several advantages:

*   Faster deployments
    
*   Easy automation in CI/CD pipelines
    
*   Scriptable infrastructure
    
*   Consistent deployments across environments
    
*   Better integration with Infrastructure as Code (IaC)
    

Using the AWS CLI is an essential skill for DevOps and Cloud Engineers managing serverless applications at scale.

## Lab Objective

The objective of this lab was to:

*   Create a Python script named **lambda\_**[**function.py**](http://function.py)
    
*   Package the script into [**function.zip**](http://function.zip)
    
*   Create a Lambda function named **nautilus-lambda-cli**
    
*   Use the **Python runtime**
    
*   Attach the existing IAM role **lambda\_execution\_role**
    
*   Verify the Lambda function by invoking it through the AWS CLI
    

## Step 1: Create the Python Lambda Function

I first created a file named **lambda\_**[**function.py**](http://function.py) with the following code:

```plaintext
def lambda_handler(event, context):
    return {
        "statusCode": 200,
        "body": "Welcome to KKE AWS Labs!"
    }
```

This simple Lambda function returns an HTTP status code of **200** along with a custom welcome message.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/b1ab5bc3-4754-44b2-af10-0f72f0681f5a.png align="center")

## Step 2: Package the Function

AWS Lambda requires the source code to be uploaded as a ZIP archive.

I packaged the Python file using the following command:

```plaintext
zip function.zip lambda_function.py
```

This created a deployment package named:

```plaintext
function.zip
```

which was later uploaded to AWS Lambda.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/e317daa2-a304-40af-9080-ea2bdb40f90e.png align="center")

## Step 3: Verify the AWS Account

Before creating the Lambda function, I verified that my AWS CLI was authenticated by checking the active AWS account.

```plaintext
aws sts get-caller-identity
```

The command returned the current AWS Account ID and IAM user details, confirming that the CLI was configured correctly.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/e7bc8926-4313-422c-8254-824acc317eaa.png align="center")

Step 4: Create the Lambda Function Using AWS CLI

Next, I created the Lambda function directly from the command line.

```python
aws lambda create-function 
--function-name nautilus-lambda-cli 
--runtime python3.9 
--role arn:aws:iam::<ACCOUNT_ID>:role/lambda_execution_role 
--handler lambda_function.lambda_handler 
--zip-file fileb://function.zip
```

Command Breakdown

| Parameter | Description |
| --- | --- |
| `--function-name` | Name of the Lambda function |
| `--runtime` | Python runtime |
| `--role` | IAM execution role |
| `--handler` | Entry point of the Python function |
| `--zip-file` | Deployment package |

After a few seconds, AWS returned the Lambda function details, confirming that the function had been created successfully.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/9979d791-d7e8-493a-b67f-3ebaa9b37b46.png align="center")

## Step 5: Invoke the Lambda Function

Finally, I tested the function directly from the command line.

```plaintext
aws lambda invoke \
    --function-name nautilus-lambda-cli \
    response.json
```

The CLI returned:

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/20a19358-c510-4027-9b4f-0d30200cd665.png align="center")

# What I Learned

This lab helped me understand how Lambda deployments are automated using the AWS CLI instead of the AWS Management Console.

Some of my key takeaways were:

*   How to package Lambda code into a ZIP archive.
    
*   How to authenticate and verify AWS CLI credentials.
    
*   How to create Lambda functions using command-line commands.
    
*   How IAM execution roles are attached during deployment.
    
*   How to invoke and test Lambda functions directly from the terminal.
    

These are the same concepts commonly used in DevOps automation and CI/CD pipelines.

# Conclusion

Day 34 introduced a more practical approach to deploying serverless applications by using the **AWS CLI** instead of the AWS Management Console.

From writing the Python function and packaging it into a deployment ZIP file to creating and testing the Lambda function entirely through the command line, this lab demonstrated how serverless deployments can be automated efficiently.

As applications grow and deployments become more frequent, using tools like the AWS CLI becomes an essential skill for every DevOps and Cloud Engineer.
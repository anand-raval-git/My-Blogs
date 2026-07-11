---
title: "AWS Day 33: Create a Lambda Function | KodeKloud 100 Days of Cloud"
seoTitle: "AWS Day 33: Create Your First AWS Lambda Function "
seoDescription: "Learn how to create your first AWS Lambda function using Python, configure an IAM execution role, deploy serverless code,"
datePublished: 2026-07-11T16:00:07.404Z
cuid: cmrgjw7gj00000ahs0hwlatn9
slug: aws-day-33-create-a-lambda-function-kodekloud-100-days-of-cloud
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/156f4414-11ea-4121-9722-c36d2b9c7988.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/1afacbb1-295f-4a4d-ba72-d6e3b7176ac0.png
tags: aws, devops, kodekloudengineer, anand-raval

---

## Introduction

As cloud applications continue to evolve, **serverless computing** has become one of the most popular ways to build scalable applications without managing servers. Instead of provisioning EC2 instances or maintaining infrastructure, developers can focus entirely on writing code while AWS automatically handles execution, scaling, availability, and maintenance.

During **Day 33 of the KodeKloud 100 Days of Cloud Challenge**, I explored **AWS Lambda**, one of AWS's core serverless services.

The objective of this lab was simple but practical—create a Python Lambda function that returns a custom greeting with an HTTP status code of **200**, while using a dedicated IAM execution role.

Although this example is small, it introduces the basic workflow you'll use when building serverless applications on AWS.

## What is AWS Lambda?

AWS Lambda is a **serverless compute service** that lets you run code without provisioning or managing servers.

You simply upload your code, configure the runtime, and AWS automatically executes your function whenever it is triggered by an event.

Some common Lambda use cases include:

*   REST APIs with API Gateway
    
*   Processing files uploaded to Amazon S3
    
*   Scheduled automation using EventBridge
    
*   Infrastructure automation
    
*   Real-time event processing
    
*   Backend services for web and mobile applications
    

One of Lambda's biggest advantages is its **pay-as-you-go pricing**, where you only pay for the time your code actually runs.

## Lab Objective

The goal of this hands-on lab was to:

*   Create a Lambda function named **devops-lambda**
    
*   Use the **Python** runtime
    
*   Create an IAM role named **lambda\_execution\_role**
    
*   Attach the IAM role to the Lambda function
    
*   Deploy the function successfully
    
*   Return an HTTP status code **200**
    
*   Display the message:
    

```plaintext
Welcome to KKE AWS Labs!
```

## Step 1: Create the Lambda Function

I started by opening the **AWS Lambda Console** and selecting **Author from scratch**.

The function was configured with the following details:

| Setting | Value |
| --- | --- |
| Function Name | devops-lambda |
| Runtime | Python 3.10 |
| Architecture | x86\_64 (Default) |

Instead of using the default execution role, I selected **Custom execution role** because the lab required a dedicated IAM role.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/46ecf4c5-cae9-4af6-aae2-c7f591acf5a9.png align="center")

## Step 2: Create the IAM Execution Role

Next, I created a new IAM role named:

```plaintext
lambda_execution_role
```

The role automatically included the **AWSLambdaBasicExecutionRole** managed policy.

This policy allows the Lambda function to write execution logs to **Amazon CloudWatch Logs**, which is essential for monitoring and debugging.

Using a dedicated IAM role also follows AWS security best practices by granting only the permissions required for the function.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/5ed24870-cd40-4dc9-b076-28ce87471f9c.png align="center")

## Step 3: Write the Python Function

After the Lambda function was created successfully, I replaced the default code with the following Python function:

This simple function returns:

*   HTTP Status Code: **200**
    
*   Response Body: **Welcome to KKE AWS Labs!**
    

Once the code was updated, I clicked **Deploy** to publish the latest version.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/2e115ae3-0f5e-4344-bdc1-dbd27a12f49a.png align="center")

```python
def lambda_handler(event, context):
    return {
        "statusCode": 200,
        "body": "Welcome to KKE AWS Labs!"
    }
```

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/fce9b430-9cfc-440d-8e4e-e552d1d19e16.png align="center")

## Step 4: Test the Lambda Function

To verify everything was working correctly, I created a new **Test Event** inside the Lambda console and invoked the function.

The execution completed successfully and returned the following response:

```plaintext
{
  "statusCode": 200,
  "body": "Welcome to KKE AWS Labs!"
}
```

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/5a4e1844-bb9d-4a53-b7b9-6b1f10602192.png align="center")

## What I Learned

Although this lab involved a simple Python function, it helped me understand several important AWS concepts.

Some key takeaways include:

*   How AWS Lambda enables serverless application development.
    
*   Why IAM execution roles are required for secure access to AWS services.
    
*   How to deploy Python code directly from the AWS Management Console.
    
*   How to test Lambda functions using built-in test events.
    
*   How Lambda automatically manages scaling and infrastructure.
    

This hands-on exercise provided a solid foundation for building more advanced serverless applications in the future.

## Conclusion

Day 33 was my first practical experience working with **AWS Lambda**, and it demonstrated how quickly serverless applications can be developed and deployed.

By creating a Lambda function, configuring a custom IAM execution role, deploying Python code, and testing the function successfully, I gained a better understanding of how AWS simplifies application development without requiring server management.

This lab serves as an excellent introduction to the AWS serverless ecosystem and prepares the way for integrating Lambda with services such as **Amazon API Gateway**, **Amazon S3**, **Amazon DynamoDB**, **Amazon EventBridge**, and **Amazon CloudWatch**.
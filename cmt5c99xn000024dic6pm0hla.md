---
title: "AWS Day 47: Integrating AWS SQS and SNS for Reliable Messaging"
seoTitle: "Integrating SQS and SNS for Reliable Messaging"
seoDescription: "Integrating SQS and SNS for Reliable Messaging in aws"
datePublished: 2026-08-23T05:00:00.000Z
cuid: cmt5c99xn000024dic6pm0hla
slug: aws-day-47-integrating-aws-sqs-and-sns-for-reliable-messaging
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/acdc558c-799f-4135-a895-349ed6c4ec51.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/b9494e38-1558-4242-8ddc-17f2aa20a646.png
tags: aws, sqs, s3, sns, anand-raval

---

Continuing my **KodeKloud 100 Days of Cloud** journey, Day 47 focused on building a **priority-based messaging system using Amazon SNS, Amazon SQS, AWS Lambda, and CloudFormation**.

The goal was simple: messages marked as **high priority** should be processed before low-priority messages.

The architecture was:

```plaintext
                 SNS Topic
                    |
          +---------+---------+
          |                   |
     priority=high       priority=low
          |                   |
          v                   v
   High Priority SQS    Low Priority SQS
          |                   |
          +---------+---------+
                    |
                    v
              AWS Lambda
```

## What I Built

Using AWS CloudFormation, I created:

*   `nautilus-High-Priority-Queue` — SQS queue for high-priority messages
    
*   `nautilus-Low-Priority-Queue` — SQS queue for low-priority messages
    
*   `nautilus-Priority-Queues-Topic` — SNS topic
    
*   `nautilus-priorities-queue-function` — Lambda function
    
*   `lambda_execution_role` — IAM execution role
    

The SNS topic uses **message attributes** to decide which SQS queue should receive a message.

For example:

```plaintext
priority = high
```

goes to:

```plaintext
High Priority Queue
```

while:

```plaintext
priority = low
```

goes to:

```plaintext
Low Priority Queue
```

## Step 1: Create the CloudFormation Template

I created the CloudFormation template on the AWS client host:

```plaintext
/root/nautilus-priority-stack.yml
```

The template defines the SNS topic, both SQS queues, queue policies, SNS subscriptions, IAM role, and Lambda function.

CloudFormation is useful here because the complete messaging infrastructure can be created from a single template instead of manually creating every AWS resource.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/c34b9854-4f03-4a1a-816b-eb4dddc121e3.png align="center")

Step 2: Configure SNS and SQS

The SNS topic acts as the publisher layer, while SQS provides reliable message queues.

The important part is the SNS subscription filter policy:

FilterPolicy: priority: - high

for the high-priority queue, and:

FilterPolicy: priority: - low

for the low-priority queue.

This means SNS automatically routes messages to the correct SQS queue based on the priority message attribute.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/7c1e4d29-ae01-4105-9d08-78a387902f63.png align="center")

## Step 3: Configure Lambda

The Lambda function consumes messages from the queues.

The Lambda execution role provides permissions such as:

```plaintext
sqs:ReceiveMessage
sqs:DeleteMessage
sqs:GetQueueAttributes
```

This allows Lambda to receive messages from SQS and delete them after successful processing.

The Lambda function was configured as:

```plaintext
nautilus-priorities-queue-function
```

Save this template as /root/datacenter-priority-stack.yml AWSTemplateFormatVersion: '2010-09-09' Description: Priority Queue Processing Stack

Resources:

HighPriorityQueue: Type: AWS::SQS::Queue Properties: QueueName: datacenter-High-Priority-Queue VisibilityTimeout: 30

LowPriorityQueue: Type: AWS::SQS::Queue Properties: QueueName: datacenter-Low-Priority-Queue VisibilityTimeout: 30

PriorityTopic: Type: AWS::SNS::Topic Properties: TopicName: datacenter-Priority-Queues-Topic

HighPriorityQueuePolicy: Type: AWS::SQS::QueuePolicy Properties: Queues: - !Ref HighPriorityQueue PolicyDocument: Version: '2012-10-17' Statement: - Effect: Allow Principal: Service: sns.amazonaws.com Action: sqs:SendMessage Resource: !GetAtt HighPriorityQueue.Arn Condition: ArnEquals: aws:SourceArn: !Ref PriorityTopic

LowPriorityQueuePolicy: Type: AWS::SQS::QueuePolicy Properties: Queues: - !Ref LowPriorityQueue PolicyDocument: Version: '2012-10-17' Statement: - Effect: Allow Principal: Service: sns.amazonaws.com Action: sqs:SendMessage Resource: !GetAtt LowPriorityQueue.Arn Condition: ArnEquals: aws:SourceArn: !Ref PriorityTopic

HighPrioritySubscription: Type: AWS::SNS::Subscription DependsOn: HighPriorityQueuePolicy Properties: TopicArn: !Ref PriorityTopic Protocol: sqs Endpoint: !GetAtt HighPriorityQueue.Arn FilterPolicy: priority: - high

LowPrioritySubscription: Type: AWS::SNS::Subscription DependsOn: LowPriorityQueuePolicy Properties: TopicArn: !Ref PriorityTopic Protocol: sqs Endpoint: !GetAtt LowPriorityQueue.Arn FilterPolicy: priority: - low

LambdaExecutionRole: Type: AWS::IAM::Role Properties: RoleName: lambda\_execution\_role AssumeRolePolicyDocument: Version: '2012-10-17' Statement: - Effect: Allow Principal: Service: - lambda.amazonaws.com Action: - sts:AssumeRole

```plaintext
  ManagedPolicyArns:
    - arn:aws:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole

  Policies:
    - PolicyName: LambdaSQSPermissions
      PolicyDocument:
        Version: '2012-10-17'
        Statement:
          - Effect: Allow
            Action:
              - sqs:ReceiveMessage
              - sqs:DeleteMessage
              - sqs:GetQueueAttributes
            Resource:
              - !GetAtt HighPriorityQueue.Arn
              - !GetAtt LowPriorityQueue.Arn
```

PriorityLambdaFunction: Type: AWS::Lambda::Function Properties: FunctionName: datacenter-priorities-queue-function Runtime: python3.9 Handler: index.lambda\_handler Timeout: 30 Role: !GetAtt LambdaExecutionRole.Arn

```plaintext
  Environment:
    Variables:
      high_priority_queue: !Ref HighPriorityQueue
      low_priority_queue: !Ref LowPriorityQueue

  Code:
    S3Bucket: <your-bucket-name>
    S3Key: function.zip
```

LambdaPermission: Type: AWS::Lambda::Permission Properties: Action: lambda:InvokeFunction FunctionName: !Ref PriorityLambdaFunction Principal: sns.amazonaws.com

Outputs:

TopicArn: Value: !Ref PriorityTopic

HighPriorityQueueURL: Value: !Ref HighPriorityQueue

LowPriorityQueueURL: Value: !Ref LowPriorityQueue

LambdaName: Value: !Ref PriorityLambdaFunction

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/d61e6c47-c0b2-4683-b1e2-c45e38889caa.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/e84fc719-6b47-4be7-8f05-e78eeb8f2f5a.png align="center")

AWS Day 47 completed: SNS, SQS, Lambda, CloudFormation, IAM, and priority-based message routing.
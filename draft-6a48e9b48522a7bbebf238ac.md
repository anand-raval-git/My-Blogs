---
title: "AWS Day 33: Create a Lambda Function"

---

The Nautilus DevOps team is embracing serverless architecture by integrating AWS Lambda into their operational tasks. They have decided to deploy a simple Lambda function that will return a custom greeting to demonstrate serverless capabilities effectively. This function is crucial for showcasing rapid deployment and easy scalability features of AWS Lambda to the team.

1.  **Create Lambda Function:** Create a Lambda function named `devops-lambda`.
    
2.  **Runtime:** Use the Runtime `Python`.
    
3.  **Deploy:** The function should print the body `Welcome to KKE AWS Labs!`.
    
4.  **Status Code:** Ensure the status code is `200`.
    
5.  **IAM Role:** Create and use the IAM role named `lambda_execution_role`.
    

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/46ecf4c5-cae9-4af6-aae2-c7f591acf5a9.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/5ed24870-cd40-4dc9-b076-28ce87471f9c.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/2e115ae3-0f5e-4344-bdc1-dbd27a12f49a.png align="center")

```python
def lambda_handler(event, context):
    return {
        "statusCode": 200,
        "body": "Welcome to KKE AWS Labs!"
    }
```

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/fce9b430-9cfc-440d-8e4e-e552d1d19e16.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/5a4e1844-bb9d-4a53-b7b9-6b1f10602192.png align="center")
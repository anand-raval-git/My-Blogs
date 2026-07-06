---
title: "AWS Day 34: Create a Lambda Function Using CLI"

---

The Nautilus DevOps team continues to explore serverless architecture by setting up another Lambda function. This time, the task must be completed using the AWS Console to familiarize the team with the web interface. The function will return a custom greeting and demonstrate the capabilities of AWS Lambda effectively.

1.  **Create Python Script:** Create a Python script named `lambda_`[`function.py`](http://function.py) with a function that returns the body `Welcome to KKE AWS Labs!` and status code `200`.
    
2.  **Zip the Python Script:** Zip the script into a file named [`function.zip`](http://function.zip).
    
3.  **Create Lambda Function:** Create a Lambda function named `nautilus-lambda-cli` using the zipped file and specify `Python` as the runtime.
    
4.  **IAM Role:** Use the IAM role named `lambda_execution_role`.
    

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/b1ab5bc3-4754-44b2-af10-0f72f0681f5a.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/e317daa2-a304-40af-9080-ea2bdb40f90e.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/e7bc8926-4313-422c-8254-824acc317eaa.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/9979d791-d7e8-493a-b67f-3ebaa9b37b46.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/20a19358-c510-4027-9b4f-0d30200cd665.png align="center")
---
title: "Python Script Reading Files From Amazon S3 (Using IAM ROLE + EC2)
"
seoTitle: "Python Script Reading Files From Amazon S3 (Using IAM ROLE +"
seoDescription: "This project demonstrates how an EC2 instance securely accesses Amazon S3 using an IAM Role without storing access keys. A Python script built with th"
datePublished: 2026-02-27T11:13:51.518Z
cuid: cmm4snx5o006o2em3fg6d1jej
slug: python-script-reading-files-from-amazon-s3-using-iam-role-ec2
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/66503d3b-200c-4d58-ba23-b25c747c844c.gif
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/f8154d00-846e-412e-9ac0-ff16c56a7585.gif
tags: aws, projects, cloud-computing, devops, 90daysofdevops

---

## Overview:-

### 1.First Create S3 Bucket

### 2.Then create i am role permission

### 3.Create ec2 instance and attach i am permission

### 4.Connect With Ec2 instance and run python script That's all

So motive of this project is We can access s3 bucket from ec2 instance without login any aws sdk or amazon login or any amazon accesss key(we can make access key from account then in ec2 we will use aws config and use our access key then we can acess s3)

### Step 1: Create an S3 Bucket

1.  Go to **AWS Console**
    
2.  Open **S3**
    
3.  Click **Create Bucket**
    

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/f10ce0fb-b96d-4e38-aa99-901f361ba7ce.png align="center")

4.  Give unique name (example: `anand-raval-bucket`) in below ss i used anand-bucket but later i released that's not available that's why i used anand-raval-bucket
    

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/64a9c934-854e-4e3b-af00-267834611b66.png align="center")

5.  Click on Creat Bucket
    

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/e24e7a46-3ba6-4ed8-837d-e3bed427172b.png align="center")

6.  Upload File i.e. anand-raval.txt in bucket
    
7.  Add some text inside (i added text nothing)
    

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/0fcb51b0-ab79-466a-959a-58f7b54fd2b2.png align="center")

### Step 2: Create IAM Role for EC2

1.  Go to IAM
    
2.  Click on Roles
    

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/91bd044b-1bb3-46d5-b6d0-34d1f04de5cf.png align="center")

3.  Click on Create Role
    

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/43d9fca1-ce78-4ae7-ba40-0a3db073c9b1.png align="center")

4.  Choose Aws Service
    
5.  Choose EC2 in Use Case
    

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/88b2980a-6d4e-4256-a7f3-2862b28f25df.png align="center")

6.  Attach Full Access s3 permission (For production attach at least privilege permission )
    

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/8e370791-a546-4b26-990e-e27ceae900f8.png align="center")

7.  You can give any role (I gave EC2-Acess-Full-S3)
    

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/2c530283-1927-4820-aeed-08c065cc6879.png align="center")

### Step 3: Launch EC2 Instance

*   AMI: Ubuntu 22.04
    
*   Instance Type: t2.micro (Free tier)
    
*   Allow SSH (Port 22)
    
*   Launch instance
    

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/918e4d23-ae57-4702-b608-4a89c69704ae.png align="center")

\-> Select ec2 and click on action > Security > Modify IAM role

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/3d0c364b-7dad-4fca-b11d-5b5c13e1fc9b.png align="center")

\-> Select EC2-Access-Full-S3 role which we already created in previous steps

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/d3a4e3d8-45a2-4121-82d2-4bcac6e8fb1b.png align="center")

\-> Open Ec2 instance run below code

```shell
sudo apt update
sudo apt install python3-pip -y
pip3 install boto3
```

You will phase some error cause while install things using previous command basically Ubuntu 22.04/24.04 security feature (PEP 668).AWS Ubuntu AMIs now block global `pip install` to protect system Python for this solution we will make virtual environment in linux using python then we can install boto3 let's run below command

```python
sudo apt install python3-venv python3-full -y
python3 -m venv myenv #creating venv
source myenv/bin/activate #acitivng venev
pip install boto3
```

```python
import boto3

# Create S3 client (IAM Role automatically used)
s3 = boto3.client('s3')

bucket_name = "anand-raval-bucket" #Use your bucket name

# List objects
response = s3.list_objects_v2(Bucket=bucket_name)

print("Files inside bucket:\n")

for obj in response.get('Contents', []):
    print(obj['Key'])

# Read a specific file
file_key = "anand-raval-file.txt" #change file name if you use another name

file_obj = s3.get_object(Bucket=bucket_name, Key=file_key)

content = file_obj['Body'].read().decode('utf-8')

print("\nFile Content:\n")
print(content)
```

\-> Now run file python3 file\_name

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/bf39812a-0cec-4636-8eac-e22460342a73.png align="center")

Congratulations If you able to access s3 from ec2 instance you worked fantastic and from this project you learnt small about s3, i am role and ec2 and how it's work and other projects are there in my blog where you can learn more about aws
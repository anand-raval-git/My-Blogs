---
title: "Day 44: Relational Database Service in AWS"
seoTitle: "AWS RDS: Relational Database Service Overview"
seoDescription: "Learn to set up and connect an AWS RDS MySQL instance and EC2 with IAM roles securely"
datePublished: 2024-09-27T15:02:11.138Z
cuid: cm1kuqaiq003h09ia33t2fzqo
slug: day-44-relational-database-service-in-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1727449267323/31fac968-b957-4119-9fc1-4239623a3eb8.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1727449304745/58eefe63-f782-46be-ac68-499a990c7a92.png
tags: aws, amazon-web-services, rds, 90daysofdevops, trainwithshubham

---

Amazon Relational Database Service (Amazon RDS) is a collection of managed services that makes it simple to set up, operate, and scale databases in the cloud

## Task-01

* Create a Free tier RDS instance of MySQL
    
* Create an EC2 instance
    
* Create an IAM role with RDS access
    
* Assign the role to EC2 so that your EC2 Instance can connect with RDS
    
* Once the RDS instance is up and running, get the credentials and connect your EC2 instance using a MySQL client.
    

### Let’s begin with task 1

### **Steps to Create RDS Instance of MySQL**

1. **Login to AWS Console** and search for "RDS".
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727446762515/fb196ad2-a44a-4af9-b858-7b36179c6536.png align="center")
    
2. **Click on "RDS"** and navigate to the RDS dashboard.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727446893587/c72330fe-25d2-42f1-9ca0-08867eb0e1c2.png align="center")
    
3. **Create a database** using the "Standard create" method and select "MySQL" under Engine options.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727446955599/cc430bed-5f9a-4f44-8f86-002f5fb3600b.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727446977269/707bd9b0-b079-4033-927d-524637602137.png align="center")
    
4. **Select "Free Tier"** under Templates.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727447030634/53cadb22-3e28-4aa8-ad36-09b6cee42671.png align="center")
    
5. **Configure settings**:
    
    * DB instance identifier: mydatabase-1
        
    * Master username: manager
        
    * Provide a password
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727447134705/a13b1904-783d-40c8-aead-835ee0d2378d.png align="center")
    
6. **Configure additional settings** like storage, backups, VPC, and security groups.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727447211688/7202067a-e3d8-4c5b-853d-0aa7307a609d.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727447258840/a935966e-89c1-4616-bd4e-0fd94615d9bd.png align="center")
    
7. **Review and create the database**. This process may take a few minutes.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727447388981/4ae9b931-0441-4dcf-b8b6-2da7604819f6.png align="center")
    
8. **Create an EC2 instance** named RDS.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727447493509/ffb5a82b-cb67-4ec4-b91d-c87867c0f1e7.png align="center")
    
9. **Configure the security group** to allow inbound traffic on the MySQL port (default is 3306).
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727447552948/0e6bcc43-c8fc-470b-907d-444a9f4758c9.png align="center")
    
10. **Create an IAM role** with RDS access and assign it to the EC2 instance.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727447617972/f24080a9-3deb-43f5-8be6-ea38694c264d.png align="center")
    
    Click on create role
    
11. **Copy the RDS instance endpoint** and other details.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727447691402/e0a34536-ac2a-40ef-a40a-056d0356e284.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727447724923/a1977f54-f07c-43a3-b6db-abd012999d03.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727447776744/7ec9d1b6-5e4e-4d71-a7da-9e0bef7b00dc.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727447827789/3dd0271a-8059-4984-b0dd-b1d41f9ae81a.png align="center")
    
12. **Connect to the EC2 instance using SSH**.
    
13. **Install the MySQL client** on the EC2 instance:
    

```bash
sudo apt-get update
sudo apt-get install mysql-client
mysql --version
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727447983635/b1add951-c413-40ed-8da3-181155806342.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727448052209/db4a8828-1f0d-43e0-a06b-3567713f3877.png align="center")

14. **Connect to the RDS instance** using the MySQL client:
    

```bash
mysql -h <RDS_ENDPOINT> -P <RDS_PORT> -u <MASTER_USERNAME> -p
```

Thankyou for reading !!!!!
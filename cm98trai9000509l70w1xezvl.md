---
title: "Day 45: Deploy Wordpress website on AWS"
seoTitle: "Deploy WordPress on AWS in Simple Steps"
seoDescription: "Learn essential steps to deploy a WordPress site on AWS using Amazon EC2 and RDS for MySQL"
datePublished: Tue Apr 08 2025 18:19:22 GMT+0000 (Coordinated Universal Time)
cuid: cm98trai9000509l70w1xezvl
slug: day-45-deploy-wordpress-website-on-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1744136310464/dc835966-deb1-4720-b6f6-37a17e242855.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1744136345213/13f81189-33d2-41e1-934b-0c8a3c7a5b85.png
tags: aws, wordpress, devops, 90daysofdevops, trainwithshubham

---

Over 30% of all websites on the internet use WordPress as their content management system (CMS). It is most often used to run blogs, but it can also be used to run e-commerce sites, message boards, and many other popular things. This guide will show you how to set up a WordPress blog site.

## **Task-01**

* As WordPress requires a MySQL database to store its data ,create an RDS as you did in Day 44
    

To configure this WordPress site, you will create the following resources in AWS:

* An Amazon EC2 instance to install and host the WordPress application.
    
* An Amazon RDS for MySQL database to store your WordPress data.
    
* Setup the server and post your new Wordpress app.
    

Here's the guide to official documentation from AWS [**to deploy this project.**](https://aws.amazon.com/getting-started/hands-on/deploy-wordpress-with-amazon-rds/)

## [Let’s begin task-01](https://aws.amazon.com/getting-started/hands-on/deploy-wordpress-with-amazon-rds/)

Before getting ahead, let us know why we need to use RDS:

* Database maintenance for your WordPress site is critical. Your database instance holds all of your important data for your WordPress site. If the database goes down, your website may go down with it, and you could even lose your data.
    
* Database maintenance can also be difficult, and database administrators have years of specialized experience. When setting up a WordPress site, you want to stay focused on designing your page and generating your content, not worrying about database performance and backups.
    

Amazon RDS for MySQL helps with both of these problems. Amazon RDS for MySQL is a managed database offering from AWS. With Amazon RDS for MySQL, you get:

* Automated backup and recovery so that you won’t lose data in the event of an accident
    
* Regular updates and patches, keeping your database secure and performant
    
* Easy installation with smart default parameters.
    

Let's start the project now.

We can divide this project into five sections, for us to make it easy to understand:

1. Create a MySQL Database with Amazon RDS.
    
2. Create an EC2 Instance.
    
3. Configure the Amazon RDS Database.
    
4. Configure WordPress on EC2.
    
5. Explore the newly set Website and clean up.
    

# **Create a MySQL Database with Amazon RDS**

***Services Used:*** Amazon RDS

Go to AWS Management Console &gt; Search and Select RDS &gt; Click on Create Database.

**Choose a database creation method:** Standard create

**Engine options: MySQL**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1744132077647/5e8b34a6-7d19-498f-9131-46c5047448db.png align="center")

Select latest version of MySQL

**Templates:** Free tier

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1744132111423/ee2ae4bd-72e8-4de4-a1ba-e7022ba5e6ad.png align="center")

**Settings:**

DB instance identifier: wpadmin

**Credentials management: Self Managed**

Master username: admin

Give the password.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1744132264893/79ae1b47-0e39-4bcd-b7e9-9d1286c34dd0.png align="center")

Let the Instance Configuration & Storage be the default for this project.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1744132312220/97d248d2-9b4e-49be-9cf4-0e622e3be270.png align="center")

> ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1744132331797/9ac7e298-b477-418c-9562-c5cfb207c51a.png align="center")

Now in the Connectivity section:

Compute resource: Don’t connect to an EC2 compute resource

Virtual private cloud (VPC): Select the default VPC

DB subnet group: Default

public access: yes

And let the other Options be the default.

Scroll down to Additional Configuration after the Monitoring section:

Initial Database name: wordpress

And retain the default settings.

> ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1744132453622/0daaecd8-c6b1-43d1-8cd2-4af8b080dc9f.png align="center")

Click on Create Database:

The creation of this RDS might take place few mins. After few minutes, you can observe that the RDS is created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1744132710323/b17111d3-ab15-4412-b593-ef08b512e47c.png align="left")

Now let's go to the second section.

1. **To configure this WordPress site, you will create the following resources in AWS:**
    
2. **An Amazon EC2 instance to install and host the WordPress application.**
    
    **Run the following command in your terminal to install a MySQL client to interact with the database.**
    
    ```bash
       sudo apt install mysql-client -y
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1744132796201/f1c23b37-38da-4839-bb25-e345775efd70.png align="center")
    
3. **Run the following command in your terminal to connect to your MySQL database. Replace “&lt;user&gt;” and “&lt;password&gt;” with the master username and password you configured when creating your Amazon RDS database. -h is the host which is the RDS database endpoint.**
    
    ```bash
      mysql -h <RDS hostname> -u <master username> -p
    ```
    
    **Finally, create a database user for your WordPress application and give the user permission to access the WordPress database.**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1744133686874/68bb6d1a-dd8e-4ddc-8ffc-bed54473566f.png align="center")
    
    **Run the following commands in your terminal:**
    
    ```bash
       CREATE DATABASE wordpress;
       CREATE USER 'wordpress' IDENTIFIED BY 'wordpress-pass';
       GRANT ALL PRIVILEGES ON wordpress.* TO wordpress;
       FLUSH PRIVILEGES;
       Exit
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1744134276637/432ccfde-8135-4368-88a5-5247fadee215.png align="center")

**To run WordPress, you need to run a web server on your EC2 instance. To install Apache on your EC2 instance, run the following command in your terminal:**

```bash
 sudo apt install apache2 
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1744134366340/c6724572-2abf-4075-9634-6a4d96a4ca7a.png align="center")

**You can see that your Apache web server is working by browsing the public IP of your ec2 instance.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1744134408394/af57b8d9-d860-4be0-83ee-afdc14cade39.png align="center")

**First, download and uncompress the software by running the following commands in your terminal:**

```bash
 wget https://wordpress.org/latest.tar.gz 
 tar -xzf latest.tar.gz
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1744134478342/d6cfe903-413d-4f3c-8424-35086bfa99ec.png align="center")

**You will see a tar file and a directory called WordPress with uncompressed contents using the ls command.**

```bash
cp wp-config-sample.php wp-config.php
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1744134545644/c9250d77-c771-47d0-984b-834c6b5d3bea.png align="center")

**<mark>Open the wp-config-sample.php file</mark>**

* **<mark>DB_NAME: your RDS database name</mark>**
    
* **<mark>DB_USER: The name of the user you created in the database in the previous steps</mark>**
    
* **<mark>DB_PASSWORD: The password for the user you created in the previous steps</mark>**
    
* **<mark>DB_HOST: The hostname of the database means your database endpoint</mark>**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1744134933979/cb495719-d152-4624-876b-da09abee634d.png align="center")

**First, install the application dependencies you need for WordPress.**

**In your terminal, run the following command.**

```bash
 sudo apt install php libapache2-mod-php php-mysql -y
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1744135142966/8850ffa8-c86e-47b2-8254-5eef9b65e919.png align="center")

**Copy your WordPress application files into the /var/www/html directory used by Apache.**

```bash
 sudo cp -r wordpress/* /var/www/html/
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1744135209646/15c117be-da77-482b-810f-bf93dc9e20c1.png align="center")

**To restart the Apache web server**

```bash
 sudo systemctl restart apache2
```

**To access the WordPress admin dashboard, open a web browser and enter the following URL:** [`http://ec2-public-ip/wp-admin/`](http://ec2-public-ip/wp-admin/)**, where**`ec2-public-ip` **should be replaced with the public IP address or domain name of your Amazon EC2 instance.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1744135326612/8952aa43-d601-4560-bdfe-f63683242c94.png align="center")

* **An Amazon RDS for MySQL database to store your WordPress data.**
    
* **Set up the server and post your new WordPress app.**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1744135530858/d5bbc43e-409d-472d-9c1d-26135a1c7bd4.png align="center")
    
    Thankyou !!!!!!!!!!!!!!!!!!!
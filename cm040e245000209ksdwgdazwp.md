---
title: "Day 24: 🚀Mastering Webhooks for Jenkins and GitHub Integration 🔗"
seoTitle: "Master Webhooks for Jenkins and GitHub"
seoDescription: "Master Jenkins-GitHub integration with webhooks for automated CI/CD. This guide covers setup, SSH keys, and Docker Compose usage"
datePublished: Wed Aug 21 2024 15:28:50 GMT+0000 (Coordinated Universal Time)
cuid: cm040e245000209ksdwgdazwp
slug: day-24-mastering-webhooks-for-jenkins-and-github-integration
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1724254090133/44b4cfe1-1273-495e-b2f5-feacb5489a19.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1724254117133/b8c696f1-5511-4b66-8869-570f0be1491f.png
tags: devops, jenkins, ci-cd, 90daysofdevops, trainwithshubham

---

### What is Web hooks ?

Webhooks are a way for one system to send real-time data to another system when a specific event happens. In the context of Jenkins and GitHub, webhooks are used to automatically trigger Jenkins jobs when changes are made in a GitHub repository.

Here's a simple explanation of how it works:

1. **Set Up Webhook in GitHub**: You configure a webhook in your GitHub repository settings. This webhook will point to your Jenkins server.
    
2. **Specify Events**: You specify which events should trigger the webhook. Common events include code pushes, pull requests, or branch merges.
    
3. **Jenkins Receives Notification**: When one of these events occurs, GitHub sends a payload of data to the Jenkins server via the webhook URL.
    
4. **Trigger Jenkins Job**: Jenkins receives this data and triggers the corresponding job. This job can then perform tasks like building the project, running tests, or deploying the application.
    

In essence, webhooks automate the process of starting Jenkins jobs based on changes in your GitHub repository, enabling continuous integration and continuous deployment (CI/CD).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724253395869/ad66dcb2-ca7d-4656-b2fe-42ce2781b072.webp align="center")

## Task 1

* Fork [this repository](https://github.com/LondheShubham153/node-todo-cicd).
    
* Set up a connection between your Jenkins job and your GitHub repository through GitHub Integration.
    

1. We want to create bridge between github and jenkins if repository is private let's begin , first create ssh key of your ubuntu instance using below command and you will get private or public key
    
    ```bash
    ssh-keygen
    ```
    
2. you have to save public key in github so follow below steps
    
    github -&gt; settings -&gt; SSH and GPG Keys -&gt; Click on New SSH KEY and add public key here
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724221989726/dcf72e73-f5ad-4af7-8dad-e60480aedee0.png align="center")
    
3. Now login into jenkins and create free style project and in source code section enter github url Now we have a remaining private key so we have to add private key in Credentials so Click on add
    
4. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724222123793/d994a462-cf2e-4d64-bc25-8df593ed09ba.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724222428347/54136ab6-1f2f-4ac8-9685-4499497ad66c.png align="center")
    
    Now select created credentials
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724222516137/9b3ba64e-9e84-4aa3-87f3-36ee89d2ed59.png align="center")
    
    We successfully created bridge between gihub and jenkins (continous integration) and click on build now
    

* Checkout code (Run in your ubuntu machine) who given by devloper
    

1. Copy path of Building in workspace path
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724222926137/170a8b39-786c-4307-960b-fe7f5a1228e4.png align="left")
    
2. Run these command in ubuntu instance
    

```bash

sudo apt install nodejs

sudo apt install npm

sudo npm install

node app.js
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724223298862/12c0c216-0396-4021-bdf3-0596959933d4.png align="center")

Open 8000 port (mention in below image) and now access it instancepublickey:8000

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724223463213/d452376f-0045-4a57-ab2e-d07779067ab7.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724223545439/5a307817-5acd-42c5-a935-cf56731b627a.png align="center")

```bash
^c #You can stop it
```

* Now automate this job using jenkins
    

1. Go to jenkins job and execute shell using below command and save it build now
    
    ```bash
    docker build -t node-app-todo .
    docker run -d --name app -p 8000:8000 node-app-todo:latest
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724224531690/40654cef-58ea-48c9-b1a4-d4e4cee2cba9.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724225152545/295b176a-4ec0-4d31-9c9f-542828a29d00.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724225197390/5786cc30-5f3d-44f1-bb63-5fd4c7480746.png align="center")
    

* Now creating a job if devloper push code into github then jenkins will automatic start pipeline (using web hook concept)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724225300296/eb368198-b601-4844-8b65-b2f0b5b2c43a.png align="center")
    

1. First we have to install plugins in jenkins so follow steps Jenkins -&gt; Manage jenkins -&gt; plugins -&gt; Available plugins and search github integration and install it
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724225606059/ce41a7ec-3328-4dab-88d6-db69d6d2dc86.png align="center")

2. Now go into github -&gt; settings -&gt; Webhooks and click on Add webhooks
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724225804157/a013ccd9-012a-4d82-8d25-fdf7e99400ec.png align="center")

3. Jn
    
    ```bash
    jenkins url/github-webhook/ #paste into payload url
    #selet application/json
    #and remember go into security group and 
    #give permission anywhere to port 8080 so github can access it
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724226360766/74285d97-0db8-4ee9-8ff6-869305ec4e32.png align="center")
    
    if there is green tick mark web hooks created successfully
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724226444900/9ae61c44-1b13-4faa-adf5-bc1add555b80.png align="left")
    
4. **GitHub hook trigger for GITScm polling and save it**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724226688284/468d3933-14de-4b44-9449-94d31bffa740.png align="center")
    
5. We are changing heading in github repo
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724226890390/9fc75f8c-95c1-43d2-bf2b-d373952891a6.png align="center")
    
    You can see in build history (finally we created continuous deployment if devloper will push code into github then jenkins will automatic build the project)
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724227118899/7fac37f3-a941-4fe5-bcef-8326e927a89c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724227055456/e8eae941-9f3e-4cfb-84ee-592377d6b713.png align="center")

## Task 2

1. In the "Execute Shell" section of your Jenkins job, run the application using Docker Compose.
    
2. Create a Docker Compose file for this project (a valuable open-source contribution).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724253838981/b822c2c3-a2ac-4989-b889-8eee7720ea5d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724253752616/2aaa1ae2-ee65-42ef-9d84-cb5196e04e3f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724253800812/eecca5b8-b5c4-40e9-8e07-c844f7999476.png align="center")

Thankyou for reading !!!!!
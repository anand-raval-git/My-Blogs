---
title: "Day-22 [part-1]:  Mastering Jenkins: A Step-by-Step Guide to CI/CD Automation 🛠️"
seoTitle: "Master Jenkins: Step-by-Step CI/CD Guide"
seoDescription: "Master Jenkins CI/CD automation with this comprehensive step-by-step guide, including installation instructions and setup tips"
datePublished: Fri Aug 16 2024 11:59:12 GMT+0000 (Coordinated Universal Time)
cuid: clzwnp7l4000109kze3ps7mv7
slug: day-22-part-1-mastering-jenkins-a-step-by-step-guide-to-cicd-automation
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1723865573331/4703b116-18c5-462b-bede-abb0e78ea43e.png
tags: devops, jenkins, cicd-cjy1vtdk2005kjjs17n8couc3, 90daysofdevops, trainwithshubham

---

## • What is Jenkins ?

* Jenkins is an open source continuous integration-continuous delivery and deployment (CI/CD) automation software DevOps tool written in the Java programming language. It is used to implement CI/CD workflows, called pipelines.
    
* Jenkins is a tool that is used for automation, and it is an open-source server that allows all the developers to build, test and deploy software. It works or runs on java as it is written in java. By using Jenkins we can make a continuous integration of projects(jobs) or end-to-endpoint automation.
    
* Jenkins achieves Continuous Integration with the help of plugins. Plugins allow the integration of Various DevOps stages. If you want to integrate a particular tool, you need to install the plugins for that tool. For example Git, Maven 2 project, Amazon EC2, HTML publisher etc.
    

## • Let us do discuss the necessity of this tool before going ahead to the procedural part for installation:

* Nowadays, humans are becoming lazy😴 day by day so even having digital screens and just one click button in front of us then also need some automation.
    
* Here, I’m referring to that part of automation where we need not have to look upon a process(here called a job) for completion and after it doing another job. For that, we have Jenkins with us.
    

## • Jenkins installtion process

Click on this documentation [Jenkins installation](https://www.jenkins.io/doc/book/installing/linux/)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723782868872/dd24e337-8ad7-4ab9-83b4-699983ce097a.png align="center")

First copy command of installation of java

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723788912532/dc491c61-02bd-4b3f-8a47-cab1a7ca700b.png align="center")

Now

LTS releases prioritize stability and long-term support, making them ideal for production use, while Weekly releases offer the latest features and updates at the cost of potential instability.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723782985469/34a60951-d8c6-48d2-89c4-f4f3b10554ea.png align="center")

First install java

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723788912532/dc491c61-02bd-4b3f-8a47-cab1a7ca700b.png align="center")

```bash
systemctl status jenkins
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723788965607/cf80313d-003d-4023-acf2-251a1cb38f2d.png align="center")

Jenkins is successfully installed now question is how to access it ? Let’s move further how to access jenkins on web page basically jenkins runs on port 8080 so we have to open this port for my ip 

Now go into EC2 &gt; Security Group &gt; inbound rules 

Click on Edit inbound rules 

![](https://media.licdn.com/dms/image/v2/D4D12AQGUvGzmV6nr9Q/article-inline_image-shrink_400_744/article-inline_image-shrink_400_744/0/1723809406491?e=1729123200&v=beta&t=XP7aHcAhESEwdJBrUq3MOHkcKHFkeJwAIPht7aRmlmo align="left")

Inport range oepn 8080 port 

And click on my ip in source 

![](https://media.licdn.com/dms/image/v2/D4D12AQHuf49lvbw0qg/article-inline_image-shrink_400_744/article-inline_image-shrink_400_744/0/1723809407707?e=1729123200&v=beta&t=UVPHxNfdprRx1r_YWvGR3Y8DPnQOpqSKYUzHdnIq_Zc align="left")

Jenkins link :- public Ip of istance:8080 

Now copy path and paste into ec2 ubuntu cli with this command  

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword 
```

You will get **Administrator password and copy it and paste on jenkins** 

Click on install suggested plugins 

![](https://media.licdn.com/dms/image/D4D12AQGXdrnFYWGQKw/article-inline_image-shrink_400_744/0/1723809406947?e=1729123200&v=beta&t=7rys3usC3qJ-YxaWXwHOiFAZPSRdD8VRWox4BJ-UKBg align="left")

![](https://media.licdn.com/dms/image/D4D12AQH6tuYtONmJlw/article-inline_image-shrink_400_744/0/1723809407078?e=1729123200&v=beta&t=gE-F7jfxyrU985yPRewkLhu9jopCBB0LutzhnzjW0xo align="left")

You have to Fill this given form  

![](https://media.licdn.com/dms/image/v2/D4D12AQEdHaD1DA4V7Q/article-inline_image-shrink_400_744/article-inline_image-shrink_400_744/0/1723809406966?e=1729123200&v=beta&t=l6atnJX_x3kdAgRdtJ4TZvRfHphu0vxeEGdtQiMnGm0 align="left")

You can set jenkins URL also 

![](https://media.licdn.com/dms/image/v2/D4D12AQH1yn4iPtM9dA/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1723809407281?e=1729123200&v=beta&t=5nZ47idFOgH1DlTE9_QQhT6KS1ArfGGt_OsZB56dFto align="left")

Click on Start using Jenkins 

![](https://media.licdn.com/dms/image/v2/D4D12AQEUwsojb-ov2g/article-inline_image-shrink_400_744/article-inline_image-shrink_400_744/0/1723809407361?e=1729123200&v=beta&t=2ktNNOD0eFc8TVXyKTRcGRdW5Ggp6aJtQ6ueoubbuco align="left")

Congratulations You are using jenkins using ec2 machine 

![](https://media.licdn.com/dms/image/D4D12AQEHWg24GCbHaA/article-inline_image-shrink_400_744/0/1723809406960?e=1729123200&v=beta&t=aTlvT27AI0s2jqUtyJbbdvp5uFfX6W_pFfxlMrojEsw align="left")

Thankyou for reading !!!!!
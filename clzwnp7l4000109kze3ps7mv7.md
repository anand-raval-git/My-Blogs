---
title: "Day-22 [part-1]:  Mastering Jenkins: A Step-by-Step Guide to CI/CD Automation 🛠️"
datePublished: Fri Aug 16 2024 11:59:12 GMT+0000 (Coordinated Universal Time)
cuid: clzwnp7l4000109kze3ps7mv7
slug: day-22-part-1-mastering-jenkins-a-step-by-step-guide-to-cicd-automation

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
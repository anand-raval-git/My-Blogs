---
title: "Day-22 [part-2]:🔧 Jenkins Unleashed: Streamline Your DevOps Workflow with Automation 🚀"
seoTitle: "Jenkins Automation for DevOps Workflows"
seoDescription: "Understand Jenkins automation: streamline your DevOps workflow with CI/CD, improve efficiency, build a Freestyle pipeline, and explore its benefits"
datePublished: Sun Aug 18 2024 16:04:03 GMT+0000 (Coordinated Universal Time)
cuid: clzzrbsi4000508l3ge1c5eid
slug: day-22-part-2-jenkins-unleashed-streamline-your-devops-workflow-with-automation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1723996974352/183771b8-749c-43e6-8b85-16420acf0edc.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1723997017278/294115bb-8542-4fef-a8bc-1c8d22851a78.png
tags: devops, jenkins, cicd, 90daysofdevops, trainwithshubham

---

### what Jenkins is and why it is used ?

Jenkins is an open-source automation server that is widely used for continuous integration and continuous delivery (CI/CD). It helps automate the parts of software development related to building, testing, and deploying, facilitating continuous integration and continuous delivery. Jenkins supports a wide range of plugins to integrate with various tools and technologies, making it highly extensible and customizable. It is used to improve the efficiency and reliability of the software development process by automating repetitive tasks, ensuring code quality, and enabling faster delivery of software updates.

### Reflect on how Jenkins integrates into the DevOps lifecycle and its benefits.

Jenkins integrates into the DevOps lifecycle by automating various stages of the software development process, including building, testing, and deploying applications. It acts as a central hub for continuous integration and continuous delivery (CI/CD) pipelines, enabling teams to implement DevOps practices effectively.

Benefits of using Jenkins in the DevOps lifecycle include:

1. **Automation**: Jenkins automates repetitive tasks, reducing manual intervention and the risk of human error.
    
2. **Continuous Integration**: It allows developers to frequently integrate code changes into a shared repository, ensuring that the codebase is always in a deployable state.
    
3. **Continuous Delivery**: Jenkins facilitates the automated deployment of applications to various environments, enabling faster and more reliable releases.
    
4. **Extensibility**: With a vast library of plugins, Jenkins can integrate with numerous tools and technologies, making it highly customizable to fit different workflows.
    
5. **Scalability**: Jenkins can be scaled to handle large projects and distributed builds across multiple machines.
    
6. **Improved Collaboration**: By providing a unified platform for CI/CD, Jenkins enhances collaboration among development, testing, and operations teams.
    
7. **Feedback and Monitoring**: Jenkins provides real-time feedback on build and test results, helping teams quickly identify and address issues.
    

Overall, Jenkins streamlines the DevOps lifecycle, improving efficiency, reliability, and speed of software delivery.

### What is the role of Jenkins in automating the build, test, and deployment processes.

1. **Build Automation**:
    
    * Jenkins automatically compiles the source code into executable files. This process, known as building, is triggered whenever there are changes in the code repository.
        
    * It ensures that the code is always in a buildable state, catching errors early in the development cycle.
        
2. **Test Automation**:
    
    * Jenkins runs automated tests on the newly built code to verify its functionality and quality. This includes unit tests, integration tests, and other types of automated tests.
        
    * By running tests automatically, Jenkins helps identify bugs and issues early, reducing the time and effort required for manual testing.
        
3. **Deployment Automation**:
    
    * Jenkins automates the deployment of applications to various environments, such as development, staging, and production.
        
    * It ensures that the deployment process is consistent and repeatable, reducing the risk of human error and making it easier to roll out updates and new features.
        
    
    Overall, Jenkins streamlines the entire software development lifecycle by automating repetitive tasks, improving code quality, and enabling faster and more reliable software delivery.
    

### Task 2: Create a Freestyle Pipeline to Print "Hello World"

Create a freestyle pipeline in Jenkins that:

* Prints "Hello World"
    
* Prints the current date and time
    
* Clones a GitHub repository and lists its contents
    
* Configure the pipeline to run periodically (e.g., every hour).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723918326566/9ebde8b6-5700-46dd-a55f-ed1e4893f3f4.png align="center")

Click on the new item

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723918565921/4c37ded1-c3ce-4ff2-9a02-5fdd1627feab.png align="center")

Give a item nam and select itme type as freestyle project

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723918520299/babb3755-b297-430d-80cd-ef72ca87742a.png align="center")

Go into build steps and click on Execute shell

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723918610583/b08eb182-b751-4cbd-96c8-7d6b6cad00a6.png align="center")

```bash
echo "Hello world" #copy this command and paste in Execute shell and save it
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723918645625/754b6429-57d7-47e5-86a9-347efe9392c5.png align="center")

Now it's time to build so click on Build now

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723918691419/6c5d49f7-6635-4a4e-b4c5-73fb041fdfbe.png align="center")

You can see output in console output and congratulations you have successfully print Hello world

* Prints the current date and time
    

```bash
echo "Current date and time is $(date):
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723994447931/99c8233f-c933-4359-a68f-bb2fad4defbd.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723994270103/c6df34fc-6c1e-421a-97b3-311ac160db0a.png align="left")

* Clones a GitHub repository and lists its contents
    

```bash
git clone #repo name
cd #repo name
ls -a
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723994796420/587b4d03-07f7-4b46-986a-f6041c9a53c2.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723994727227/a915b7d8-c426-4737-8c95-ed3d49aa0750.png align="center")

* Configure the pipeline to run periodically (e.g., every hour).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723995389840/7ef30bac-1a8f-41f8-81fa-fc8444698d29.png align="center")

```bash
pipeline {
    agent any
    triggers {
        cron('* * * * *') // This sets the pipeline to run every minute
    }
    stages {
        stage('Example') {
            steps {
                echo 'This pipeline runs every minute'
            }
        }
    }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723996671267/63336138-31e8-45b2-9c26-24ee2ce8210d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723996611111/e68a5da5-21e4-44e2-828d-75a07d3c4319.png align="center")

Thankyou for reading !!!!!!
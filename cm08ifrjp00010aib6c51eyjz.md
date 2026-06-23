---
title: "Day 27 Task: Jenkins Declarative Pipeline with Docker 🚀"
seoTitle: "Jenkins Pipeline with Docker Guide"
seoDescription: "Create a Docker-integrated Jenkins Declarative Pipeline with ease. Follow these steps to elevate your CI/CD skills! 🚀"
datePublished: 2024-08-24T19:05:08.150Z
cuid: cm08ifrjp00010aib6c51eyjz
slug: day-27-task-jenkins-declarative-pipeline-with-docker
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1724526235426/b17a0944-87bf-4227-a1a8-961d0588eedd.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1724526284570/ae20b0e9-511f-4118-80f6-94ed358e333d.png
tags: devops, jenkins, declarative, 90daysofdevops, trainwithshubham

---

Day 26 was all about a Declarative pipeline, now its time to level up things, let's integrate Docker and your Jenkins declarative pipeline

## Use your Docker Build and Run Knowledge

**docker build -** you can use `sh 'docker build . -t <tag>'` in your pipeline stage block to run the docker build command. (Make sure you have docker installed with correct permissions.

**docker run:** you can use `sh 'docker run -d <image>'` in your pipeline stage block to build the container.

**How will the stages look**

# **How the Stages Look**

Here's an example of how the stages might look in your Jenkins Declarative Pipeline:

```bash
pipeline
{
agent any
stages {
    stage('Build') {
        steps {
            sh 'docker build -t your-image-tag .'
        }
    }

    stage('Run') {
        steps {
            sh 'docker run -d your-image-tag'
        }
    }
    stage('Deploy') {
        steps {
            sh 'Deploy throught out cicd'
        }
    }
 }
}
```

### Task 01: Create a Docker-Integrated Jenkins Declarative Pipeline

To create a Docker-integrated Jenkins Declarative Pipeline, follow these steps:

1. **Log In:** Log in to your Jenkins server and navigate to the Jenkins home page.
    
2. **Create New Item:** Click on the "New Item" button on the left-hand side of the screen to create a new Jenkins pipeline.
    
3. **Enter Item Name:** In the "Enter an item name" field, type in a name for your new pipeline and select "Pipeline" as the project type.
    
4. **Continue:** Click on the "OK" button to proceed.
    
5. **Configure Pipeline:** On the next page, scroll down to the "Pipeline" section and select "Pipeline script" as the Definition.
    
6. **Define Pipeline Script:** In the Script text area, use the following code and save it
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724523734615/4296a4d8-7deb-4e79-b278-f3db1b025d1d.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724523794345/6b3c27d4-65c1-44a4-b047-ceb715dc56ce.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724523943037/dd67e878-5a4f-464f-8b17-4c7849e318ea.png align="center")
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724525775981/961f154d-2ec0-4b83-ba63-9158f52ae724.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724525791895/4c26b4f8-0ec4-46af-82f6-f4957d9198a8.png align="center")

```bash
pipeline
{
    agent any
    stages{
    stage("Code")
    {
        steps
        {
            git url : 'https://github.com/anand-raval-git/react_django_demo_app.git' , branch: 'main'
        }
    }
    stage("Build")
    {
        steps
        {
            sh 'docker build . -t anand-raval-git/react_django_demo_app'
        }
    }
        
    }
}
```

**Step 2: Run the Jenkins Pipeline:**

1. To run the pipeline, click on the pipeline name on the Jenkins home page.
    
2. Click on the "Build Now" button to start the pipeline.
    
    Check the output of the build:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724525578937/8f970255-5da9-44d5-b398-1a0387a13f8e.png align="center")
    

Thankyou for reading !!!!!
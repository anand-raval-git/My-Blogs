---
title: "Day 23 Task: Jenkins Freestyle Project for DevOps Engineers"
seoTitle: "Jenkins Freestyle Project DevOps Guide"
seoDescription: "Guide for DevOps Engineers to set up Jenkins Freestyle Projects including build jobs, Docker commands, and automated deployment steps"
datePublished: 2024-08-20T20:34:00.837Z
cuid: cm02vunlx000309leh2gdeya2
slug: day-23-task-jenkins-freestyle-project-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1724185988565/e2c097d6-30ac-46e5-a6c0-c8f3edb0ec49.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1724186029240/252192a4-596d-4f45-a73c-9af7063c2b66.png
tags: devops, jenkins, jenkins-devops, 90daysofdevops, trainwithshubham

---

## What is CI/CD?

* **CI (Continuous Integration)** is the practice of automating the integration of code changes from multiple developers into a single codebase. It involves developers frequently committing their work into a central code repository (such as GitHub or Stash). Automated tools then build the newly committed code and perform tasks like code review, ensuring that the code is integrated smoothly. The key goals of Continuous Integration are to find and address bugs quickly, make the integration process easier across a team of developers, improve software quality, and reduce the time it takes to release new features.
    
* **CD (Continuous Delivery)** follows Continuous Integration and ensures that new changes can be released to customers quickly and without errors. This includes running integration and regression tests in a staging environment (similar to production) to ensure the final release is stable. Continuous Delivery automates the release process, ensuring a release-ready product at all times and allowing deployment at any moment.
    

## What Is a Build Job?

A Jenkins build job contains the configuration for automating specific tasks or steps in the application building process. These tasks include gathering dependencies, compiling, archiving, transforming code, testing, and deploying code in different environments.

Jenkins supports several types of build jobs, such as freestyle projects, pipelines, multi-configuration projects, folders, multibranch pipelines, and organization folders.

## What is a Freestyle Project? 🤔

A freestyle project in Jenkins is a type of project that allows you to build, test, and deploy software using various options and configurations. Here are a few tasks you could complete with a freestyle project in Jenkins:

### Task 1

1. **Create an Agent for Your App**
    
    Ensure you have a Jenkins agent set up for your app if you deployed it using Docker in an earlier task.
    
2. **Create a New Jenkins Freestyle Project for Your App**
    
    * Open Jenkins and click on "New Item."
        
    * Enter a name for the project, select "Freestyle project," and click "OK."
        
3. **Add a Build Step to Run the** `docker build` Command
    
    * In the "Build" section of the project configuration, click "Add build step" and select "Execute shell."
        
    * Enter the following command to build the Docker image:
        
        ```bash
         build -t your-app-image .
        ```
        
4. **Add a Build Step to Run the** `docker run` Command
    
    * Click "Add build step" again and select "Execute shell."
        
    * Enter the following command to start a container using the image created in the previous step:
        
        **Copy**
        
        **Copy**
        
        ```bash
          docker run -d --name your-app-container your-app-image
        ```
        

### Detailed Steps with Screenshots

1. **Create a New Jenkins Freestyle Project**
    
    Login to Jenkins, then create a "new item" freestyle project as shown below:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724180902624/72d2f899-873f-46f9-9542-cdf1fba417a4.png align="center")
    
2. **Project Configuration**
    
    In the "General" section, you can specify descriptions of your job or project. You can also specify a GitHub project with the "Project URL" copied from your GitHub repo URL.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724181035957/45ef137a-c119-4286-a855-0d803bd156be.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724185442461/53e61293-cf11-468c-b2d1-6419f5bbac09.png align="center")
    
3. **Source Code Management**
    
    Specify the repository URL and branch name under the "Source Code Management" section.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724181155449/84188b9e-3176-4029-a703-190cd4c4e694.png align="center")
    
4. **Build Steps**
    
    Add build steps to run the `docker build` command to create an image for the container, and then the `docker run` command to run the container from the created image.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724181336203/0c123376-678a-4da5-925e-c61830c0248e.png align="center")
    
5. **Ensure Docker is Installed**
    
    Ensure Docker is installed and given access to Jenkins:
    
    ```bash
     sudo apt-get install docker.io -y
     sudo apt-get install docker-compose
     sudo usermod -aG docker $USER
     sudo usermod -aG docker jenkins
     sudo reboot
    ```
    
6. **Build and View Console Output**
    
    Click on "Apply" and "Save," then click "Build Now" to manually start the process and execute the configured steps. You can view the console output to check the build progress.
    
7. **Verify Deployment**
    
    You can see the projects deployed from GitHub at the location `/var/lib/jenkins/workspace`. Additionally, you can verify that your application is running.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724182064740/a8b83c58-f02f-40f4-955b-addd3361ba79.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724182161343/3d469dee-59d5-475d-80c9-6df261a93aff.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724182238061/d0fbe39a-5ce2-4df6-ac87-4969b745b3bf.png align="center")
    
    ### **Task-02: Create a Jenkins Project to Run** `docker-compose up -d`
    
    **Step -1) Create a Jenkins project to run the "docker-compose up -d" command to start the multiple containers defined in the compose file.**
    
    **Step 2) Set up a cleanup step in the Jenkins project to run the "docker-compose down" command to stop and remove the containers defined in the compose file.**
    
    1. In continuing to the first task, we create `docker-compose.yml` the file inside our project.
        
    2. In `Build step` section, `add build steps` like this. Here `docker compose down` is taken first to remove and stop the containers defined in the compose file then afterward we use `docker-compose up -d` command.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724182752015/e23b64c8-bc16-4f0d-a336-8b42098d6ef7.png align="center")
        
    3. Thus, we `save` and `build now` the project. We can view the `console output` below.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724185235517/127b1e50-ba56-405a-8f04-c7f3f33bb3ad.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724185277332/2d69d3cb-3164-4f83-9824-04aab708f457.png align="center")
        

Thankyou for reading !!!!!!
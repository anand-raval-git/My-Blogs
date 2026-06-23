---
title: "Day 26 Task: Jenkins Declarative Pipeline 🚀"
seoDescription: "Learn Jenkins Declarative Pipeline, Jenkinsfile, pipeline structure, and creating Jenkins jobs with Declarative Pipeline syntax. 🚀"
datePublished: 2024-08-23T13:50:40.234Z
cuid: cm06rriax000009jx8rqi21dv
slug: day-26-task-jenkins-declarative-pipeline
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1724420388347/ff67d977-8e58-4ab0-9f65-77942fe0683f.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1724420415697/4d37e72e-29fe-430f-a5c2-e699b0d2a24b.png
tags: devops, jenkins, declarative, 90daysofdevops, trainwithshubham

---

## Some terms for your Knowledge

**What is Pipeline -** A pipeline is a collection of steps or jobs interlinked in a sequence.

**Declarative:** Declarative is a more recent and advanced implementation of a pipeline as a code.

**Scripted:** Scripted was the first and most traditional implementation of the pipeline as a code in Jenkins. It was designed as a general-purpose DSL (Domain Specific Language) built with Groovy.

# **What is Jenkinsfile ?**

The definition of a Jenkins Pipeline is written into a text file (called a [`Jenkinsfile`](https://www.jenkins.io/doc/book/pipeline/jenkinsfile)) [which in t](https://www.jenkins.io/doc/book/pipeline/jenkinsfile)urn can be committed to a project’s source control repository.  
This is the foundation of "Pipeline-as-code"; treating the CD pipeline as a part of the application to be versioned and reviewed like any other code.

**Creating a** `Jenkinsfile` and committing it to source control provides a number of immedia[te benefits](https://www.jenkins.io/doc/book/pipeline/jenkinsfile):

* Automatically creates a Pipeline build process for all branches and pull requests.
    
* C[ode review/](https://www.jenkins.io/doc/book/pipeline/jenkinsfile)iteration on the Pipeline (along with the remaining source code).
    

A Jenk[insfile is](https://www.jenkins.io/doc/book/pipeline/jenkinsfile) a text file that contains the definition of a Jenkins pipeline. It is used to automate the process of building, testing, and deploying software projects. The Jenkinsfile is written using a domain-specific language (DSL) that Jenkins understands, and it allows you to define the steps your pipeline should take in a clear and structured way. By using a Jenkinsfile, you can version control your pipeline code along with your application code, making it easier to manage and maintain.

## **Jenkins Pipeline Structure**

| **Term** | **Description** |
| --- | --- |
| Pipeline | The pipeline is a set of instructions given in the form of code for continuous delivery and consists of instructions needed for the entire build process. With a pipeline, you can build, test, and deliver the application. |
| Node | The machine on which Jenkins runs is called a node. A node block is mainly used in scripted pipeline syntax. |
| Stage | A stage block contains a series of steps in a pipeline. That is, the build, test, and deploy processes all come together in a stage. Generally, a stage block is used to visualize the Jenkins pipeline process. |
| Step | A step is nothing but a single task that executes a specific process at a defined time. A pipeline involves a series of steps. |
| Agent | An agent specifies where the pipeline, or a specific stage of the pipeline, will run. It can be a specific Jenkins node, a Docker container, or any other environment that Jenkins can use to execute the pipeline steps. The agent block is used in declarative pipeline syntax. |
| Post | The post block contains steps that are run at the end of the pipeline or stage. It is used to define actions that should be taken after the pipeline or stage completes, such as sending notifications or cleaning up resources. |
| Environment | The environment block is used to define environment variables that will be available to all steps within the pipeline or a specific stage. These variables can be used to configure the pipeline's behavior or pass information between steps. |
| Parameters | The parameters block is used to define parameters that can be passed to the pipeline when it is triggered. These parameters can be used to customize the pipeline's behavior based on user input. |

## **Why Use Declarative Pipeline Syntax?**

Using Declarative Pipeline Syntax in Jenkins is beneficial because it makes creating and managing pipelines easier and more straightforward. Here are some reasons why:

1. **Simplicity**: Declarative syntax is easier to read and write, especially for beginners. It uses a clear and structured format, which makes it simpler to understand what each part of the pipeline does.
    
2. **Error Checking**: Jenkins can catch errors in your pipeline code before it runs, helping you avoid mistakes and save time.
    
3. **Consistency**: Declarative pipelines enforce a consistent structure, which makes it easier to maintain and share your pipeline code with others.
    
4. **Built-in Features**: Declarative syntax includes many built-in features like stages, steps, and post actions, which help you define your pipeline more efficiently.
    
5. **Version Control**: By writing your pipeline as code, you can store it in your version control system (like Git), making it easier to track changes and collaborate with your team.
    

Overall, Declarative Pipeline Syntax helps you create reliable, maintainable, and easy-to-understand pipelines in Jenkins.

# **Types of Jenkins Pipeline**

## Types of Jenkins Pipeline

1. **Declarative Pipeline**: This is a more recent and advanced implementation of pipeline as code. It uses a simpler and more structured syntax, making it easier to read and write. Declarative pipelines are designed to be user-friendly and include built-in error checking and validation.
    
2. **Scripted Pipeline**: This was the first and most traditional implementation of pipeline as code in Jenkins. It uses a general-purpose DSL (Domain Specific Language) built with Groovy. Scripted pipelines offer more flexibility and control but can be more complex and harder to maintain compared to declarative pipelines.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724418574377/fac77b7e-9789-4274-b9eb-8726684b743c.jpeg align="center")

## **Scripted Pipeline**

Jenkins only allowed the user to write the pipeline as a code, hence a scripted pipeline. Such a pipeline is written in a Jenkinsfile on the web UI of the Jenkins tool. You can write a scripted pipeline with `DSL (domain specific language)` and use `Groovy based syntax`.

The Job `DSL plugin` provides a solution, and allows you to configure Jenkins jobs as code.

***What exactly is*** `Groovy`***?*** It is a programming language that uses the Java virtual machine(JVM).

A `Java virtual machine (JVM)` is a virtual machine that enables a computer to run Java programs as well as programs written in other languages that are also compiled to Java bytecode.

### **Advantages of Scripted Pipeline**

* Scripted pipelines offer a full-fledged programming ecosystem to developers
    
* Developers can inject Groovy scripts and reference Java APIs inside a scripted pipeline definition
    
* Blocks of scripted pipelines can be injected inside the script step of a declarative pipeline definition. This enhances cross-pipeline support.
    

### **Disadvantage of Scripted Pipeline**

* Scripted syntax can be harder to learn for beginners as compared to declarative syntax
    
* Scripted pipelines don’t offer runtime syntax checking
    
* Scripted pipelines don’t have the When directive, which can be used to skip a stage if a condition isn’t met
    
* It isn’t possible to restart a scripted pipeline from a previous stage
    

### **Syntax**

```bash
node {  
    stage('Build') { 
        // Execute Some steps here
    }
    stage('Test') { 
        // Execute Some steps here
    }
    stage('Pre deploy') { 
        // Execute Some steps here
    }
    stage('Deploy') { 
        // Execute Some steps here
    }
}
```

## **Creating a Jenkins Job Using Declarative Pipeline Syntax**

Follow these steps to create a new Jenkins job using the Declarative Pipeline Syntax:

### **Step 1 - Create a New Jenkins Job**

1. Log in to your Jenkins instance
    
2. Go into New Item -&gt; Enter an item name -&gt; select pipeline
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724419374942/777a8e53-7c5c-46c1-8e87-a3c6928749af.png align="center")

### **2 - Define Your Pipeline**

Once you have created your new job, you will be taken to the job configuration page. On this page, you can define the description as follow:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724419469613/27393fa7-2a1a-4ea5-bf47-966c5f2d0852.png align="center")

Now write script

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724419676860/42c83e2f-71e4-4ad7-93cd-c49ac9112b29.png align="center")

```bash
pipeline
{
    agent any
    stages
    {
        stage("Clone"){
            steps{
                echo "Clone code from github"
            }
        }
        stage("Test"){
            steps{
                echo "Test the code"
            }
        }
        stage("Deploy"){
            steps{
                echo "Deploy the code"
            }
        }
    }
}
```

In this Pipeline, we have defined four stages - Clone, Test, and Deploy. Each stage has a single step that prints a message to the console. The `agent` directive specifies that the Pipeline can run on any available agent.

### **Step 3 - Save and Run Your Pipeline**

Once you have defined your Pipeline, save the changes to your job configuration. Jenkins will automatically validate your Pipeline syntax and display any errors or warnings.

To run your Pipeline, click the "Build Now" button on the job page. Jenkins will start the build process and display the console output in real-time.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724419877659/205e4f55-5b3c-410d-bdaf-dc6ecfb033b0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724419828933/29f03a25-f71a-4f38-a998-8bed49b7d8de.png align="center")

Thankyou for reading !!!!!
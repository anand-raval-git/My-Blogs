---
title: "Day 25 Task: 🚀Complete Jenkins CI/CD Project - Continued with Documentation 📄"
seoDescription: "Comprehensive guide on Jenkins CI/CD project setup, including GitHub, Docker, and Webhook integration, with step-by-step documentation"
datePublished: Thu Aug 22 2024 19:06:40 GMT+0000 (Coordinated Universal Time)
cuid: cm05nm13s000209l3hgh3akfj
slug: day-25-task-complete-jenkins-cicd-project-continued-with-documentation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1724353551706/70a13def-ed80-4576-8280-c1755e94e5bd.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1724353588581/b1bf47d9-5432-4545-9031-2e334d877f12.png
tags: devops, jenkins, ci-cd, 90daysofdevops, trainwithshubham

---

## Introduction

We completed till day 24 , we deployed project through cicd pipeline and learn aboout github hooks and many things so in this blog i made documentation about what we learned in jenkins

## Steps for Jenkins CI/CD Project

Let's dive into the detailed documentation.

### GitHub Setup

1. **Create a GitHub Account**: If you don't already have a GitHub account, you can create one by following the steps in [Creating an account on GitHub](https://github.com/).
    
2. **Create a GitHub Repository**: Once your account is set up, create a new repository by following the instructions in [Create a GitHub Repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository).
    
3. **Set Up Git Configuration**:
    
    * Open your terminal or command prompt.
        
    * Configure your Git username and email:
        
        ```bash
        git config --global user.name "Your Name"
        git config --global user.email "your-email@example.com"
        ```
        
4. **Clone the Repository**:
    
    * Copy the repository URL from GitHub.
        
    * Clone the repository to your local machine:
        
        ```bash
        git clone https://github.com/your-username/your-repository.git
        ```
        
5. **Initialize Git Repository**:
    
    * Navigate to your project directory:
        
        ```bash
        cd your-repository
        ```
        
    * Initialize the Git repository:
        
        ```bash
        git init
        ```
        
6. **Add Files**:
    
    * Add your project files to the repository:
        
        ```bash
        git add .
        ```
        
7. **Commit Changes**:
    
    * Commit your changes with a message:
        
        ```bash
        git commit -m "Initial commit"
        ```
        
8. **Push Changes**:
    
    * Push your changes to the remote repository:
        
        ```bash
        git push origin main
        ```
        

### Docker and jenkins installation in ubuntu

1. **Install Docker**:
    
    * Update your package list:
        
        ```bash
        sudo apt-get update
        ```
        
    * Install Docker:
        
        ```bash
        sudo apt-get install -y docker.io
        ```
        
2. **Install Docker Compose**:
    
    * Download the Docker Compose binary:
        
        ```bash
        sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
        ```
        
    * Apply executable permissions:
        
        ```bash
        sudo chmod +x /usr/local/bin/docker-compose
        ```
        
3. **Install Java**:
    
    * Install Java Development Kit (JDK):
        
        ```bash
        sudo apt-get install -y openjdk-11-jdk
        ```
        
4. **Add Jenkins Repository Key**:
    
    * Add the Jenkins repository key:
        
        ```bash
        wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
        ```
        
5. **Add Jenkins Repository**:
    
    * Add the Jenkins repository to your sources list:
        
        ```bash
        sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
        ```
        
6. **Install Jenkins**:
    
    * Update your package list and install Jenkins:
        
        ```bash
        sudo apt-get update
        sudo apt-get install -y jenkins
        ```
        
7. If you phase any problem then follow this link [jenkins installation](https://anandraval.hashnode.dev/day-22-part-1-mastering-jenkins-a-step-by-step-guide-to-cicd-automation)
    
8. **Jenkins Service**:
    
    * Start the Jenkins service:
        
        ```bash
        sudo systemctl start jenkins
        ```
        

### Docker Setup

1. **Add User to Docker Group**:
    
    * Add your user to the Docker group:
        
        ```bash
        sudo usermod -aG docker $USER
        ```
        
2. **Verify User Group Addition**:
    
    * Verify that your user has been added to the Docker group:
        
        ```bash
        groups $USER
        ```
        
3. **Fix Docker Permission Errors**:
    
    * If you encounter permission errors, restart your machine or log out and log back in.
        
4. **Create a Dockerfile**:
    
    * Create a `Dockerfile` in your project directory. Example:
        
        ```Dockerfile
        FROM openjdk:11
        COPY . /app
        WORKDIR /app
        RUN ./mvnw package
        CMD ["java", "-jar", "target/your-app.jar"]
        ```
        
5. **Build Docker Image**:
    
    * Build your Docker image:
        
        ```bash
        docker build -t your-app .
        ```
        
6. **List Docker Images**:
    
    * List your Docker images to verify the build:
        
        ```bash
        docker images
        ```
        
7. **Run Docker Container**:
    
    * Run your Docker container:
        
        ```bash
        docker run -p 8080:8080 your-app
        ```
        
8. **List Running Containers**:
    
    * List running containers to verify your application is running:
        
        ```bash
        docker ps
        ```
        
9. **Set Up Inbound Rules**: Add specific ports to your instance for accessing your application via browser (refer to [Setting up inbound rules](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html)).
    

### Jenkins Setup

1. **Access Jenkins**: Visit `<Your_Public_IP:8080>` in your browser.
    
2. **Unlock Jenkins**: Use the admin password found in the location specified in the Jenkins setup page.
    
3. **Set Up Jenkins**: Follow the instructions in the Jenkins setup wizard to complete the setup.
    
4. **Create a Freestyle Job**: Create your first Jenkins job by referring to the Jenkins documentation on [First Freestyle Job](https://www.jenkins.io/doc/book/pipeline/getting-started/).
    

### GitHub Webhook Integration

1. **Create a Webhook in GitHub**: Set up a webhook in your GitHub repository by following the instructions in [How to create a Webhook](https://docs.github.com/en/developers/webhooks-and-events/webhooks/creating-webhooks).
    
2. **Configure Webhook**:
    
    * **Payload URL**: `<Jenkins_URL:port/github-webhook/>`
        
    * **Select Events**: Choose the events that should trigger the webhook.
        
3. **Add Webhook**: Click on the “Add webhook” button and refresh the page to confirm activation.
    
4. **Integrate Webhook with Jenkins Job**: Follow the steps in the Jenkins [documentation](https://anandraval.hashnode.dev/day-24-mastering-webhooks-for-jenkins-and-github-integration) to integrate the webhook with your Jenkins job.
    
5. **Test Integration**: Make changes to any file in your GitHub repo, commit the changes, and verify that Jenkins triggers the job automatically.
    
6. **Access Application**: Use `<Your_Public_IP>:Port` specified in your application to verify deployment.
    

Thankyou for reading !!!!!
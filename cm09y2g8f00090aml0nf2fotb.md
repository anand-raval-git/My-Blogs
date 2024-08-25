---
title: "Day 28 : 🚀 Setting Up Jenkins Agents: A Step-by-Step Guide 🖥️"
seoTitle: "Setting Up Jenkins Agents: Step-by-Step Guide"
seoDescription: "Step-by-step guide to setting up Jenkins Agents, enhancing your CI/CD pipeline for scalable, distributed job execution"
datePublished: Sun Aug 25 2024 19:10:26 GMT+0000 (Coordinated Universal Time)
cuid: cm09y2g8f00090aml0nf2fotb
slug: day-28-setting-up-jenkins-agents-a-step-by-step-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1724612890956/6f295bec-bc25-4c73-8b9d-991170f5b0f5.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1724613008185/5fce2eb1-d793-4814-9127-ad648cd74316.png
tags: devops, jenkins, jenkins-devops, 90daysofdevops, trainwithshubham

---

## Jenkins Master (Server)

The Jenkins master server is the central control unit that manages the overall orchestration of workflows defined in pipelines. It handles tasks such as scheduling jobs, monitoring job status, and managing configurations. The master serves the Jenkins UI and acts as the control node, delegating job execution to agents.

## Jenkins Agent

A Jenkins agent is a separate machine or container that executes the tasks defined in Jenkins jobs. When a job is triggered on the master, the actual execution occurs on the assigned agent. Each agent is identified by a unique label, allowing the master to delegate jobs to the appropriate agent.

For small teams or projects, a single Jenkins installation may suffice. However, as the number of projects grows, it becomes necessary to scale. Jenkins supports this by allowing a master to connect with multiple agents, enabling distributed job execution.

[![](https://user-images.githubusercontent.com/115981550/215276859-fa140ab7-e905-41c9-8ae2-1eef577c5e72.png align="center")](https://user-images.githubusercontent.com/115981550/215276859-fa140ab7-e905-41c9-8ae2-1eef577c5e72.png)

## Pre-requisites

To set up an agent, you'll need a fresh Ubuntu 22.04 Linux installation. Ensure Java (the same version as on the Jenkins master server) and Docker are installed on the agent machine.

*Note: While creating an agent, ensure that permissions, rights, and ownership are appropriately set for Jenkins users.*

### **Let's start With Jenkins Master and Agent Instances**

1. Launch an EC2 instance, named "Jenkins-master".
    
2. Connect it with terminal.
    
3. Install Java and Jenkins on the master instance. Refer this **Installation Of Java and Jenkins**.
    
4. Now login to Jenkins using &lt;Your\_Public\_IP:8080&gt; via browser. Add 8080 to security group under inbound rules in your instance using the AWS console.  
    You will see the below page.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724606781687/d5cc4c66-b0c7-4e71-b559-2b898224ef46.png align="center")
    
    ```bash
    #You can find the Admin password on the location given in the above snapshot
    sudo cat /var/lib/jenkins/secrets/initialAdminPassword
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724606899746/81fb5b5a-9104-4db7-83df-ed8a02febda5.png align="center")
    
5. You need to setup Jenkins here, Refer to **Setting up Jenkins**.
    
6. Launch another instance, named "Jenkins-agent".
    
7. Connect it with terminal and install Java on this terminal.
    
8. Now Go to Your Jenkins and click on "Manage Jenkins".
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724607027361/a0636d71-611e-46d0-b5a3-4c8b1089dee7.png align="center")
    
9. Click on "Security"
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724607067699/54455f80-6c97-426f-9231-3bfd8037c18c.png align="center")
    
10. Under Security, Go to "Agents" and in TCP port, Select "Random" and save the configuration.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724607149427/943e751c-4cfb-4e46-a9e9-381d8e4f25a2.png align="center")
    
11. Now, In "Manage Jenkins", Go to "Nodes".
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724607203730/890d11e9-23a7-484b-a93a-2042c1e51d84.png align="center")
    
12. Click on "New Node".
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724607255245/ec8a7599-41bb-4902-9831-bc1899409269.png align="center")
    
13. Now give the name of your node and select "Permanent Agent".
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724607322582/a037dd90-ba55-4f48-9cda-096c6106fcec.png align="center")
    
14. Now, configure your node. Give the Remote root directory where your node will get launch and will do the tasks and leave all the settings as default and click on "Save".
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724607427348/537ad715-5f66-48d0-84c7-962e08331c8d.png align="center")
    
15. You can see, we have our node and it is offline as of now.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724607473451/7f04640b-c6ac-4927-a97f-3590054600f8.png align="center")
    
16. Click on your agent, you will see the below page.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724607586799/f1907fcf-3c35-4749-8a30-9a67fee4f15b.png align="center")
    
17. On Jenkins-agent instance just paste the commands given in the above screenshot a per you choice. You can choose any of the above according to your OS.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724609571063/6248cdbf-cb98-483a-a710-7e5ceb36b19f.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704206230199/bdd31012-b4ba-4390-8dab-d1b6d0c2f394.png?auto=compress,format&format=webp&auto=compress,format&format=webp align="left")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724609883896/4f532b2f-6a72-4601-b0da-3bdc80dfc891.png align="center")
    
18. I have got the above error, while connecting as the port was not specified on the master instance. So, I have added the port in the security group.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724609978409/e10be582-2c0a-4164-b5b8-2965897ff0e3.png align="center")
    
19. Then run the command again, it worked.\]
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724610187358/93c17625-0f0a-49b4-92a3-210a63fe93c6.png align="center")
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724610235785/fea6cdd1-5791-4e0e-88c2-bcb2766dc17d.png align="center")

### Creating Jobs on Jenkins with Node Configuration

#### Example: Deploy a Django Application

1. 1. Create a new Jenkins freestyle project named "Django-todo"
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724612198729/147f5e45-123a-4144-9d1c-6d87701168ac.png align="center")
        
2. **Configure Source Code Management:**
    
    * The GitHub URL to pull the code for your Django application.
        
        [Github](https://github.com/anand-raval-git/django-todo.git)
        
3. Configure the project. Under "General Settings" &gt; Select "Restrict where this project can be run" &gt; Select the "Node".
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724610408315/7ff0f0c9-6b5a-4caf-97b2-c1486f92ac9b.png align="center")
    
4. In the Source Code Management section &gt; Select Git &gt; Enter the GitHub Repository Link and the branch name.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724610686110/5503056e-2959-4835-86b2-36c668fe133c.png align="center")
    
5. In the Build Steps section &gt; Select Add Build Steps &gt; Select Execute Shell &gt; And type the commands required for your activity. Click on Save.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724611360859/eb018bbd-c750-4b0d-9674-1513ef233e6b.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724611514202/0eba9347-3da3-45a6-bdd4-63330a131e58.png align="center")
    
    ```bash
    docker build -t app .
    docker run -d --name todoapp -p 8000:8000 app:latest
    ```
    
6. Before building the project, see if Docker is installed on your Jenkins-agent or not. If not then install it and gave permission to it using below command.
    
    ```bash
    sudo apt install docker
    sudo usermod -aG docker $user
    sudo reboot
    ```
    
7. You can also give direct permission to docker demon using below command
    
    ```bash
    sudo chmod 666 /var/run/docker.sock
    ```
    
8. **Build and Verify:**
    
    * Click on “Build Now” and monitor the output.
        
    * Verify that the application is running correctly on the agent server.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724611626249/9c5797d1-104d-448b-ba46-e736a9629922.png align="center")
        
    
    Thankyou for reading !!!!!
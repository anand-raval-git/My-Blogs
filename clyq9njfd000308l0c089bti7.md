---
title: "Day 7 Task :- Mastering Linux Package Management: A Beginner's Guide to Docker and Jenkins Installation 🐧📦"
seoTitle: "Linux Package Management: Docker & Jenkins Guide"
seoDescription: "Master Linux package management, install Docker/Jenkins on Ubuntu, and grasp essential concepts/commands"
datePublished: Wed Jul 17 2024 19:59:40 GMT+0000 (Coordinated Universal Time)
cuid: clyq9njfd000308l0c089bti7
slug: day-7-task-mastering-linux-package-management-a-beginners-guide-to-docker-and-jenkins-installation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1721246168465/03ecbf2b-e87e-43b7-88b8-80649ad8e4fd.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1721246366256/ea7b19ab-644b-4541-9220-d68825866b29.png
tags: docker, devops, jenkins, 90daysofdevops, trainwithshubham

---

## Day 7 :- TASK

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721158034706/82acb8da-832b-4c7f-a5b3-4aeb9608fe48.png align="center")

## • What is a Package Manager in Linux ?

A package manager in Linux is a tool that helps you install, update, and remove software on your computer. Think of it like an app store on your smartphone, but for your Linux system.

Here's a simple breakdown:

1. **Installation**: If you want to add new software to your computer, the package manager can find and install it for you. You don't need to search the internet for the software or worry about downloading the wrong version.
    
2. **Updates**: Software often gets updates to fix bugs or add new features. The package manager can automatically check for updates and install them, keeping your software up-to-date.
    
3. **Removal**: If you no longer need a piece of software, the package manager can remove it cleanly from your system, ensuring that all related files are also deleted.
    
4. **Dependencies**: Some software needs other software to work properly. The package manager handles these dependencies for you, making sure everything needed is installed.
    

In summary, a package manager makes managing software on your Linux system easy and efficient, much like how an app store simplifies managing apps on your phone.

## • What is a Package ?

A package in the context of computers and software is like a bundle that contains everything needed to install and run a specific program or application. Think of it as a neatly packed box that includes the software itself, along with all the instructions and additional files it needs to work properly.

Here's a simple breakdown:

1. **Software**: The main program or application you want to use.
    
2. **Dependencies**: Other small programs or libraries that the main software needs to function correctly. These are included in the package to ensure everything works smoothly.
    
3. **Instructions**: Information on how to install and set up the software on your computer.
    

In summary, a package is a convenient way to distribute software, ensuring that you get everything you need in one go, without having to hunt down additional files or worry about compatibility issues.

## • Different Kinds of Package Managers

There are several different kinds of package managers in Linux, each designed to work with specific types of Linux distributions. Here are some of the most common ones, explained in a beginner-friendly way:

1. **APT (Advanced Package Tool)**:
    
    * **Used by**: Debian-based distributions like Ubuntu.
        
    * **How it works**: APT helps you install, update, and remove software using simple commands. It automatically handles dependencies, so you don't have to worry about missing files.
        
2. **YUM (Yellowdog Updater, Modified)**:
    
    * **Used by**: Red Hat-based distributions like Fedora and CentOS.
        
    * **How it works**: YUM allows you to manage software packages from the command line. It can automatically download and install software from repositories, making it easy to keep your system up-to-date.
        
3. **DNF (Dandified YUM)**:
    
    * **Used by**: Newer versions of Fedora and CentOS.
        
    * **How it works**: DNF is the next-generation version of YUM. It offers better performance and more features, but works in a similar way to help you manage software packages.
        
4. **Pacman**:
    
    * **Used by**: Arch Linux and its derivatives.
        
    * **How it works**: Pacman is known for its simplicity and speed. It uses straightforward commands to install, update, and remove software, and it handles dependencies automatically.
        
5. **Zypper**:
    
    * **Used by**: openSUSE and SUSE Linux Enterprise.
        
    * **How it works**: Zypper is a command-line tool that makes it easy to manage software packages. It can install, update, and remove software, and it also handles dependencies for you.
        
6. **Snap**:
    
    * **Used by**: Various Linux distributions.
        
    * **How it works**: Snap packages are self-contained and include all the dependencies needed to run the software. This makes it easy to install and run software on different Linux distributions without compatibility issues.
        
7. **Flatpak**:
    
    * **Used by**: Various Linux distributions.
        
    * **How it works**: Flatpak is similar to Snap in that it provides self-contained packages. It aims to make it easy to install and run software across different Linux distributions.
        

In summary, package managers are tools that help you install, update, and remove software on your Linux system. Different Linux distributions use different package managers, but they all aim to make managing software easy and efficient.

## • **How to Install Docker and Jenkins on Ubuntu Using Package Managers**

Installing software on Ubuntu can be a breeze if you use the right package managers. In this guide, we'll walk you through the steps to install Docker and Jenkins on your Ubuntu system using the APT package manager.

### Installing Docker

Docker is a platform that allows you to automate the deployment of applications inside lightweight, portable containers. Here’s how to install Docker on Ubuntu:

1. **Update the package list and install required packages:** Open your terminal and run the following commands to update your package list and install necessary packages:
    
    ```bash
    sudo apt update
    sudo apt install apt-transport-https ca-certificates curl software-properties-common
    ```
    
2. **Add Docker’s official GPG key:**
    
    ```bash
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
    ```
    
3. **Add the Docker APT repository:**
    
    ```bash
    echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    ```
    
4. **Update the package list again:**
    
    ```bash
    sudo apt update
    ```
    
5. **Install Docker:**
    
    ```bash
    sudo apt install docker-ce
    ```
    
6. **Check Docker installation:** Verify that Docker is installed correctly by running:
    
    ```bash
    sudo systemctl status docker
    ```
    

### Installing Jenkins

Jenkins is an open-source automation server that helps automate parts of software development related to building, testing, and deploying. Here’s how to install Jenkins on Ubuntu:

1. **Add the Jenkins repository key to the system:**
    
    ```bash
    curl -fsSL https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
    ```
    
2. **Add the Jenkins repository:**
    
    ```bash
    echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
    ```
    
3. **Update the package list:**
    
    ```bash
    sudo apt update
    ```
    
4. **Install Jenkins:**
    
    ```bash
    sudo apt install jenkins
    ```
    
5. **Start Jenkins:**
    
    ```bash
    sudo systemctl start jenkins
    ```
    

### Note:

Before installing Jenkins, ensure that Java is installed on your system. You can check if Java is installed by running:

```bash
java -version
```

If Java is not installed, you can install it using:

```bash
sudo apt install openjdk-11-jdk
```

By following these steps, you can easily install Docker and Jenkins on your Ubuntu system using the APT package manager. This will set you up to start using these powerful tools for containerization and automation.

## Another method for jenkins installation

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721243497580/9b3803a8-8704-4dd1-ad13-d1e32eb5d9c4.png align="center")

```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```

[Jenkins Documation](https://www.jenkins.io/doc/book/installing/linux/)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721244106118/e64fe5fc-cb47-46ce-9beb-1bca01870413.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721244146946/f741415e-40b3-4146-8e2f-0e924b4ac222.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721244301670/aa9ddf70-1477-4450-b513-240e70556ba5.png align="left")

## • what is Systemctl and Systemd

**Systemctl** and **Systemd** are tools used in Linux to manage and control system services and processes.

**Systemd** is a system and service manager for Linux operating systems. It is responsible for starting, stopping, and managing various services and processes on your computer. Think of it as the conductor of an orchestra, ensuring that all the different parts of your system work together harmoniously.

* **Boot Process**: Systemd is responsible for booting up your system. It starts all the necessary services and processes when you turn on your computer.
    
* **Service Management**: It manages services (like web servers, databases, etc.) and ensures they run smoothly. If a service crashes, Systemd can automatically restart it.
    
* **Logging**: Systemd keeps logs of system events, which can be useful for troubleshooting issues.
    

### • Systemctl

**Systemctl** is a command-line tool used to interact with Systemd. It allows you to control and manage services and processes on your system. Think of it as a remote control for Systemd.

Here are some common tasks you can perform with Systemctl:

* **Start a Service**: You can start a service using the command:
    
    ```bash
    sudo systemctl start <service-name>
    ```
    
    For example, to start the Apache web server, you would use:
    
    ```bash
    sudo systemctl start apache2
    ```
    
* **Stop a Service**: You can stop a service using the command:
    
    ```bash
    sudo systemctl stop <service-name>
    ```
    
* **Restart a Service**: You can restart a service using the command:
    
    ```bash
    sudo systemctl restart <service-name>
    ```
    
* **Enable a Service**: You can enable a service to start automatically at boot using the command:
    
    ```bash
    sudo systemctl enable <service-name>
    ```
    
* **Disable a Service**: You can disable a service from starting automatically at boot using the command:
    
    ```bash
    sudo systemctl disable <service-name>
    ```
    
* **Check Service Status**: You can check the status of a service using the command:
    
    ```bash
    sudo systemctl status <service-name>
    ```
    

**Systemd** is the system and service manager that ensures your Linux system runs smoothly, while **Systemctl** is the tool you use to control and manage those services and processes.

* Examples:
    
    * Check the status of the Docker service:
        
        ```bash
           sudo service docker status
        ```
        
    * Start the Jenkins service:
        
        ```bash
           sudo service jenkins start
        ```
        
    * Stop the Docker service:
        
        ```bash
           sudo service docker stop
        ```
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721244146946/f741415e-40b3-4146-8e2f-0e924b4ac222.png align="center")

* `service` Command
    
    * 'service' is a command that works with the older 'init' systems (like SysVinit). It provides a way to start, stop, and check the status of services. While it is still available on systems using 'systemd' for backward compatibility, its usage is generally discouraged in favor of 'systemctl'.
        
    * **Key Differences**
        
        * 1 System Architecture:
            
            * `systemctl` works with `systemd`.
                
            * `service` works with SysVinit and is compatible with `systemd` for backward compatibility.
                
        * 2 Functionality:
            
            * `systemctl` offers more functionality and control over services, including management of the service's state (start, stop, restart, reload), enabling/disabling services at boot, and querying detailed service status.
                
            * `service` provides basic functionality for managing services, such as starting, stopping, and checking the status of services.
                
        * 3 Syntax and Usage:
            
            * `systemctl` uses a more unified syntax for managing services.
                
            * `service` has a simpler and more traditional syntax.
                
        
        ## • **Automate Service Management:**
        
    * Write a script to automate the starting and stopping of Docker and Jenkins services.
        
    
    ```bash
    #!/bin/bash
    
    read -p "Enter the service you want to manage (docker/jenkins):" service
    read -p "Enter action (start/stop):" action
    
    sudo systemctl $action $service
    
    echo "$service service $action completed"
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721244966192/31242796-1a11-4fa2-b96a-c5fb3665ff94.png align="left")
    
    ## • **Enable and Disable Services:**
    
* Use systemctl to enable Docker to start on boot and disable Jenkins from starting on boot.
    

Enable Docker to start on boot:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721245338759/58aa21b3-c3cb-4451-90a2-2b0fcb84bd03.png align="center")

Disable Jenkins from starting on boot:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721245399007/29b1a497-7489-4c95-8b86-22937720c1b6.png align="center")

* ## • **Analyze Logs:**
    
* Use journalctl to analyze the logs of the Docker and Jenkins services. Post your findings.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721245551281/b056bdf1-0557-4af9-b12d-994fdf9ebc8f.png align="center")

Jenkins Logs:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721245590901/2cc0b6b9-d5bf-424b-b6e6-37158afac03d.png align="center")

Thank you for reading!

<mark>© 2024 Anand Raval. All rights reserved.</mark>
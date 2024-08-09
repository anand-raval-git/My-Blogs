---
title: "Day 18 : Mastering Docker Compose: A Comprehensive Guide for DevOps Engineers 🚀"
seoDescription: "Master Docker Compose with this comprehensive guide for DevOps engineers, covering YAML, container management, and essential commands. 🚀😃"
datePublished: Fri Aug 09 2024 14:35:30 GMT+0000 (Coordinated Universal Time)
cuid: clzmt78h3000808jl0o6tcj0j
slug: day-18-mastering-docker-compose-a-comprehensive-guide-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1723214093180/75771f38-8341-4ac7-80bd-c829a109d93a.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1723214113485/e04d2caa-9c3e-4acf-9db8-047bdd5fe341.png
tags: docker, devops, containers, 90daysofdevops, trainwithshubham

---

Till now you have created a Dockerfile and pushed it to the repository. Let's move forward and dig deeper into other Docker concepts. Today, let's study Docker Compose! 😃

## Docker Compose

* Docker Compose is a tool that was developed to help define and share multi-container applications.
    
* With Compose, we can create a YAML file to define the services and, with a single command, spin everything up or tear it all down.
    
* Learn more about Docker Compose [here](https://tecadmin.net/tutorial/docker/docker-compose/).
    

## What is YAML?

* YAML is a data serialization language that is often used for writing configuration files. Depending on whom you ask, YAML stands for "Yet Another Markup Language" or "YAML Ain’t Markup Language" (a recursive acronym), which emphasizes that YAML is for data, not documents.
    
* YAML is a popular programming language because it is human-readable and easy to understand.
    
* YAML files use a .yml or .yaml extension.
    
* Read more about it [here](https://www.redhat.com/en/topics/automation/what-is-yaml).
    

## Task 1

Learn how to use the docker-compose.yml file to set up the environment, configure the services and links between different containers, and also to use environment variables in the docker-compose.yml file.

[Sample docker-compose.yml file](https://github.com/LondheShubham153/90DaysOfDevOps/blob/master/2023/day18/docker-compose.yaml)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723212600604/de9d4475-6143-4b76-9546-2f2fcea4919a.png align="center")

## Task 2

* Pull a pre-existing Docker image from a public repository (e.g. Docker Hub) and run it on your local machine. Run the container as a non-root user (Hint: Use the `usermod` command to give the user permission to Docker). Make sure you reboot the instance after giving permission to the user.
    
* Inspect the container's running processes and exposed ports using the `docker inspect` command.
    
* Use the `docker logs` command to view the container's log output.
    
* Use the `docker stop` and `docker start` commands to stop and start the container.
    
* Use the `docker rm` command to remove the container when you're done.
    

1. Pulling a pre-existing Docker image from a public repository.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723212868248/7122f89a-555d-415c-a6e1-eef1c1c9f23e.png align="center")

2. Running it on your local machine.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723212934450/65498420-7bcb-4c1e-b172-067791f3b180.png align="center")

3. Inspect the container's running processes and exposed ports using the `docker inspect` command.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723213076900/4c613310-e7ef-422f-93ac-eee2b7a9e844.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723213177984/05add98e-c6a5-4555-81de-490c72ceb4c1.png align="center")

4. Use the `docker logs` command to view the container's log output.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723213293893/40632576-59a4-4ff6-8ad1-8470e4d8adb8.png align="center")

5. Use the `docker stop` and `docker start` commands to stop and start the container.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723213345535/816f2497-49d7-46d7-8f7c-e20bf28903ae.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723213373925/ff72064a-436a-4bd5-90e0-597b1635278f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723213394547/cc6027bd-2959-40ab-872b-b46ef29b2ea1.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723213416205/a45a6e77-5d26-487e-8019-006320fa2a03.png align="center")

6. Use the `docker rm` command to remove the container when you're done.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723213493989/950909ef-19d6-456e-95c5-46cb132a9ab5.png align="center")

## How to Run Docker Commands Without Sudo?

* Make sure Docker is installed and the system is updated (This was already completed as part of previous tasks):
    
* `sudo usermod -a -G docker $USER`
    
* Reboot the machine.
    

Thank you for reading!

<mark>© 2024 Anand Raval. All rights reserved.</mark>
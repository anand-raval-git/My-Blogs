---
title: "Day 20 : 🚀 Docker Cheat Sheet: Essential Commands for Images, Containers, and Docker Hub 🌟"
seoTitle: "Docker Cheat Sheet: Key Commands"
seoDescription: "Essential Docker commands for images, containers, and Docker Hub. Get your quick reference guide for managing and optimizing your Docker workflow"
datePublished: 2024-08-14T17:23:09.182Z
cuid: clzu4e3ge000409l37xpw1jty
slug: day-20-docker-cheat-sheet-essential-commands-for-images-containers-and-docker-hub
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1723656218555/41d95a53-f85b-41c2-9f09-ad97207f24ab.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1723656168045/d0829b67-d0a5-421c-866b-df482403b24e.png
tags: docker, devops, containers, 90daysofdevops, trainwithshubham

---

## Docker Cheat Sheet

Docker is a powerful platform for developing, shipping, and running applications inside containers. This cheat sheet covers essential Docker commands for managing images, containers, general operations, and Docker Hub interactions.

### Images Commands

* **List Images**
    
    ```sh
    docker images
    ```
    
    Lists all images on your local machine.
    
* **Pull an Image**
    
    ```sh
    docker pull <image_name>
    ```
    
    Downloads an image from Docker Hub.
    
* **Remove an Image**
    
    ```sh
    docker rmi <image_name>
    ```
    
    Deletes an image from your local machine.
    
* **Build an Image**
    
    ```sh
    docker build -t <image_name> <path_to_dockerfile> or .
    ```
    
    Builds an image from a Dockerfile.
    
* **Tag an Image**
    
    ```sh
    docker tag <image_id> <new_image_name>
    ```
    
    Tags an image with a new name.
    

### Containers Commands

* **List Containers**
    
    ```sh
    docker ps
    ```
    
    Lists all running containers.
    
* **List All Containers**
    
    ```sh
    docker ps -a
    ```
    
    Lists all containers, including stopped ones.
    
* **Run a Container**
    
    ```sh
    docker run -d --name <container_name> <image_name>
    ```
    
    Runs a container in detached mode.
    
* **Stop a Container**
    
    ```sh
    docker stop <container_name>
    ```
    
    Stops a running container.
    
* **Remove a Container**
    
    ```sh
    docker rm <container_name>
    ```
    
    Deletes a stopped container.
    
* **Start a Container**
    
    ```sh
    docker start <container_name>
    ```
    
    Starts a stopped container.
    
* **Restart a Container**
    
    ```sh
    docker restart <container_name>
    ```
    
    Restarts a running container.
    
* **Attach to a Running Container**
    
    ```sh
    docker attach <container_name>
    ```
    
    Attaches your terminal to a running container.
    

### General Commands

* **Docker Version**
    
    ```sh
    docker --version
    ```
    
    Displays the Docker version installed on your machine.
    
* **Docker Info**
    
    ```sh
    docker info
    ```
    
    Displays system-wide information about Docker.
    
* **Login to Docker Hub**
    
    ```sh
    docker login
    ```
    
    Logs you into Docker Hub.
    
* **Logout from Docker Hub**
    
    ```sh
    docker logout
    ```
    
    Logs you out of Docker Hub.
    
* **Docker Help**
    
    ```sh
    docker --help
    ```
    
    Displays help information for Docker commands.
    

### Docker Hub Commands

* **Push an Image to Docker Hub**
    
    ```sh
    docker push <image_name>
    ```
    
    Uploads an image to Docker Hub.
    
* **Pull an Image from Docker Hub**
    
    ```sh
    docker pull <image_name>
    ```
    
    Downloads an image from Docker Hub.
    
* **Search for an Image on Docker Hub**
    
    ```sh
    docker search <image_name>
    ```
    
    Searches for an image on Docker Hub.
    

### Conclusion

This cheat sheet provides a quick reference to the most commonly used Docker commands. Whether you're managing images, containers, or interacting with Docker Hub, these commands will help streamline your workflow. Happy Dockering!
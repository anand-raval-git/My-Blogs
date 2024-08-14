---
title: "Day 19: Docker for DevOps Engineers 🚀"
seoTitle: "Docker Essentials for DevOps Engineers"
seoDescription: "Learn Docker Volume and Network for data storage and container communication. Master multi-container apps with advanced Docker Compose"
datePublished: Wed Aug 14 2024 17:21:58 GMT+0000 (Coordinated Universal Time)
cuid: clzu4ckwd000209mf6k7p1ims
slug: day-19-docker-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1723656106626/4938a7e7-86a2-4302-bbeb-fa41ebab8913.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1723574041900/2731fa0e-125e-4223-87bb-3082ca3daac9.png
tags: docker, devops, docker-images, 90daysofdevops, trainwithshubham

---

So far, you've learned how to create a docker-compose.yml file and push it to the repository. Let's move forward and explore more Docker Compose concepts. Today, let's study Docker Volume and Docker Network! 😃

## Docker Volume

Docker allows you to create volumes, which are like separate storage areas that can be accessed by containers. They enable you to store data, like a database, outside the container, so it doesn't get deleted when the container is removed. You can also mount the same volume to multiple containers, allowing them to share data. For more details, check out this [reference](https://docs.docker.com/storage/volumes/).

## Docker Network

Docker allows you to create virtual networks, where you can connect multiple containers together. This way, the containers can communicate with each other and with the host machine. Each container has its own storage space, but if we want to share storage between containers, we need to use volumes. For more details, check out this [reference](https://docs.docker.com/network/).

## Task 1

Create a multi-container docker-compose file that will bring up and bring down containers in a single shot (e.g., create application and database containers).

### Hints:

* Use the `docker-compose up` command with the `-d` flag to start a multi-container application in detached mode.
    
* Use the `docker-compose scale` command to increase or decrease the number of replicas for a specific service. You can also add [`replicas`](https://stackoverflow.com/questions/63408708/how-to-scale-from-within-docker-compose-file) in the deployment file for auto-scaling.
    
* Use the `docker-compose ps` command to view the status of all containers, and `docker-compose logs` to view the logs of a specific service.
    
* Use the `docker-compose down` command to stop and remove all containers, networks, and volumes associated with the application.
    

## Task 2

* Learn how to use Docker Volumes and Named Volumes to share files and directories between multiple containers.
    
* Create two or more containers that read and write data to the same volume using the `docker run --mount` command.
    
* Verify that the data is the same in all containers by using the `docker exec` command to run commands inside each container.
    
* Use the `docker volume ls` command to list all volumes and the `docker volume rm` command to remove the volume when you're done.
    

## Answer to Task 1

To create a multi-container docker-compose file, follow these steps:

1. Create a `docker-compose.yml` file with the following content:
    

```yaml
version: '3.8'

services:
  app:
    image: your-application-image
    ports:
      - "8080:8080"
    networks:
      - app-network
    depends_on:
      - db

  db:
    image: your-database-image
    volumes:
      - db-data:/var/lib/mysql
    networks:
      - app-network

networks:
  app-network:

volumes:
  db-data:
```

2. Use the following commands to manage your multi-container application:
    

* Start the application in detached mode:
    
    ```sh
    docker-compose up -d
    ```
    
* Scale the application service:
    
    ```sh
    docker-compose scale app=3
    ```
    
* View the status of all containers:
    
    ```sh
    docker-compose ps
    ```
    
* View the logs of a specific service:
    
    ```sh
    docker-compose logs app
    ```
    
* Stop and remove all containers, networks, and volumes:
    
    ```sh
    docker-compose down
    ```
    

## Answer to Task 2

To use Docker Volumes and Named Volumes to share files and directories between multiple containers, follow these steps:

1. Create and start containers with a shared volume:
    

```sh
docker run -d --name container1 --mount source=shared-data,target=/data your-image
docker run -d --name container2 --mount source=shared-data,target=/data your-image
```

2. Verify that the data is the same in all containers:
    

* Write data in `container1`:
    
    ```sh
    docker exec container1 sh -c 'echo "Hello from container1" > /data/hello.txt'
    ```
    
* Read data in `container2`:
    
    ```sh
    docker exec container2 cat /data/hello.txt
    ```
    

3. List all volumes:
    

```sh
docker volume ls
```

4. Remove the volume when done:
    

```sh
docker volume rm shared-data
```

Thank you for reading!

<mark>© 2024 Anand Raval. All rights reserved.</mark>
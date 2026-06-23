---
title: "Day 16 : Docker for DevOps Engineers 🐳"
seoTitle: "Docker Essentials for DevOps Engineers"
seoDescription: "Learn Docker commands to manage containers efficiently for DevOps tasks: run, inspect, port, stats, top, save, and load"
datePublished: 2024-07-30T17:41:57.819Z
cuid: clz8pgibf000408l6ghh58t0p
slug: day-16-docker-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1722361256443/c00e9942-1dc3-4345-ac40-e61c3f678b72.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1722361294919/2f38f141-2e1c-4fa4-b1e5-83add04dc87c.png
tags: docker, devops, containers, 90daysofdevops, trainwithshubham

---

### Docker

Docker is a software platform that allows you to build, test, and deploy applications quickly. Docker packages software into standardized units called containers that have everything the software needs to run, including libraries, system tools, code, and runtime. Using Docker, you can quickly deploy and scale applications into any environment and know your code will run.

## Tasks

As you have already installed Docker in previous tasks, now is the time to run Docker commands.

* Use the `docker run` command to start a new container and interact with it through the command line. \[Hint: `docker run hello-world`\]
    
* Use the `docker inspect` command to view detailed information about a container or image.
    
* Use the `docker port` command to list the port mappings for a container.
    
* Use the `docker stats` command to view resource usage statistics for one or more containers.
    
* Use the `docker top` command to view the processes running inside a container.
    
* Use the `docker save` command to save an image to a tar archive.
    
* Use the `docker load` command to load an image from a tar archive.
    

These tasks involve simple operations that can be used to manage images and containers.

## What is docker ?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721983880753/8a51d1fe-4b49-4faa-a9b1-dd353b849732.png align="center")

Docker is a tool that helps developers create, deploy, and run applications inside containers. Think of a container as a lightweight, portable box that holds everything an application needs to run, such as code, libraries, and system tools. This ensures that the application works the same way, regardless of where it is run.

### Example

Imagine you have a recipe for baking a cake. Normally, you would need to gather all the ingredients and tools (like flour, sugar, eggs, oven, etc.) every time you want to bake. This can be time-consuming and sometimes things might not work out if you miss an ingredient or use a different oven.

Now, think of Docker as a special kitchen box that contains all the ingredients and tools you need to bake the cake. No matter where you take this box, you can always bake the same cake because everything you need is already inside.

In technical terms, here's a simple example:

1. **Dockerfile**: This is like your recipe. It contains instructions on how to build your container.
    
    ```dockerfile
    FROM python:3.8-slim
    COPY . /app
    WORKDIR /app
    RUN pip install -r requirements.txt
    CMD ["python", "app.py"]
    ```
    
2. **Building the Container**: You use the Dockerfile to create a container image.
    
    ```sh
    docker build -t my-python-app .
    ```
    
3. **Running the Container**: You can then run the container anywhere.
    
    ```sh
    docker run -d -p 5000:5000 my-python-app
    ```
    

In this example, the container will run a Python application, and it will work the same way on any computer because everything it needs is inside the container.

## How does docker work ?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721984361553/ed1d625a-f069-420a-a2c4-88090e195c4b.png align="center")

Docker works by leveraging several layers to create and manage containers. Here's an explanation of how Docker operates across different layers:

### Resource Layer

This is the physical or virtual hardware that provides the computing resources such as CPU, memory, storage, and network interfaces. These resources are essential for running the operating system and Docker containers.

### Operating System Layer

Docker runs on the host operating system, which can be Linux or Windows. The host OS manages the hardware resources and provides the necessary system calls and services that Docker relies on. Docker uses the OS kernel features like namespaces and control groups (cgroups) to isolate and manage resources for containers.

### Hypervisor Layer (Optional)

In some setups, Docker can run on virtual machines managed by a hypervisor like VMware, Hyper-V, or KVM. The hypervisor layer abstracts the physical hardware and allows multiple virtual machines to run on a single physical machine. Each VM can run its own instance of Docker.

### Docker Engine Layer

The Docker Engine is the core component of Docker. It consists of three main parts:

1. **Docker Daemon (dockerd)**: This is the background service running on the host OS. It manages Docker objects like images, containers, networks, and volumes.
    
2. **REST API**: This allows programs to interact with the Docker Daemon and instruct it to perform actions.
    
3. **Docker CLI (Command Line Interface)**: This is the command-line tool that users interact with to issue commands to the Docker Daemon.
    

### Docker Container Layer

Containers are lightweight, standalone, and executable packages that include everything needed to run a piece of software, including the code, runtime, libraries, and system tools. Each container runs as an isolated process in user space on the host OS, sharing the kernel with other containers. Containers are created from Docker images, which are read-only templates with instructions for creating a Docker container.

### How It All Works Together

1. **Resource Layer**: Provides the necessary hardware resources.
    
2. **Operating System Layer**: Manages hardware resources and provides the environment for Docker to run.
    
3. **Hypervisor Layer** (if used): Allows Docker to run on virtual machines.
    
4. **Docker Engine Layer**: Manages Docker containers and images.
    
5. **Docker Container Layer**: Runs applications in isolated environments.
    

By using these layers, Docker ensures that applications are portable, consistent, and can run anywhere, whether on a developer's laptop, on-premises data center, or in the cloud.

## **Difference Between Using VirtualBox and Docker**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721984375181/0df55873-eb9f-4697-a4ff-44c5b29bf2db.png align="center")

## **VirtualBox (Virtual Machines)**

1. **Resource Usage**: Each virtual machine (VM) runs a full operating system, which consumes more CPU, memory, and storage.
    
2. **Boot Time**: VMs take longer to start because they need to boot an entire OS.
    
3. **Isolation**: VMs provide strong isolation as each VM runs a separate OS.
    
4. **Portability**: VMs are less portable because they are tied to the hypervisor and the underlying hardware.
    

### **Bungalow (Virtual Machines)**

1. **Resource Usage**: Each bungalow is like a virtual machine (VM). It has its own kitchen, bathroom, and living spaces, consuming more resources (CPU, memory, storage).
    
2. **Boot Time**: Just like it takes time to build and set up a bungalow, VMs take longer to start because they need to boot an entire operating system.
    
3. **Isolation**: Each bungalow is completely isolated from the others, providing strong isolation.
    
4. **Portability**: Moving a bungalow to a different location is difficult, similar to how VMs are less portable because they are tied to the hypervisor and underlying hardware.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721984673329/36cb89b7-d9aa-4d98-a5bc-b1aae6a892dc.png align="center")

#### **Docker (Containers)**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721984411821/88a6140e-5502-4364-84da-84edf8ffbad9.png align="center")

1. **Resource Usage**: Containers share the host OS kernel, making them more lightweight and efficient in terms of resource usage.
    
2. **Boot Time**: Containers start almost instantly because they do not need to boot an entire OS.
    
3. **Isolation**: Containers provide process-level isolation, which is sufficient for most applications but not as strong as VMs.
    
4. **Portability**: Containers are highly portable and can run on any system that supports Docker, regardless of the underlying hardware.
    

In summary, Docker is more efficient and portable compared to using virtual machines with VirtualBox. While VMs provide stronger isolation, Docker's lightweight nature and faster startup times make it a better choice for many development and deployment scenarios.

Imagine a society with a large bungalow and several apartments to understand how Docker works with the operating system and resources.

### **Apartments (Docker Containers)**

1. **Resource Usage**: Apartments share common resources like the building's foundation, walls, and roof, similar to how Docker containers share the host OS kernel. This makes them more lightweight and efficient.
    
2. **Boot Time**: Just as you can quickly move into an apartment because the building is already there, containers start almost instantly because they do not need to boot an entire OS.
    
3. **Isolation**: Each apartment is isolated from the others, providing sufficient privacy and separation, similar to how containers provide process-level isolation.
    

**Portability**: Apartments can be easily rented out or moved into different buildings, just like containers are highly portable and can run on any system that supports Docker.

## What is docker engine ?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721984847125/65df9524-8f73-439d-a839-db5083ab195d.png align="center")

The Docker Engine is the core component of Docker, responsible for managing containers. It consists of three main parts:

1. **Docker Daemon (dockerd)**: This is the background service that manages Docker objects like images, containers, networks, and volumes. It listens for Docker API requests and performs the necessary actions.
    
2. **Docker CLI (Command Line Interface)**: This is the tool users interact with to issue commands to the Docker Daemon. It simplifies container management by allowing users to run commands like `docker run`, `docker build`, and `docker pull`.
    
3. **containerd**: This is a container runtime that the Docker Daemon uses to manage the lifecycle of containers. It handles tasks such as starting, stopping, and managing containers.
    

Together, these components ensure efficient and consistent container management.

### Use the `docker run` command to start a new container and interact with it through the command line. \[Hint: `docker run hello-world`\]

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721985481473/eed30b34-5e47-4745-b0cc-8ec19840cab2.png align="center")

### Use the `docker inspect` command to view detailed information about a container or image.

```bash
# Inspecting a container
docker inspect <container_id_or_name>

# Inspecting an image
docker inspect <image_id_or_name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722001048900/ce160c3f-10fa-44bc-984f-72de87fa4c6f.png align="center")

### Use the `docker port` command to list the port mappings for a container.

```bash
# List port mappings for a container
docker port <container_id_or_name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722001180121/56000039-afff-4c49-8d0e-a8ff85d45c80.png align="center")

### Use the `docker stats` command to view resource usage statistics for one or more containers.

```bash
# View resource usage statistics for all running containers
docker stats

# View resource usage statistics for a specific container
docker stats <container_id_or_name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722001264903/1482be6d-b7aa-427d-945a-dec77489b765.png align="center")

### Use the `docker top` command to view the processes running inside a container.

```bash
# View processes running inside a container
docker top <container_id_or_name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722001316601/e6e60102-df87-40b7-ae69-d49ca16c59ce.png align="center")

### Use the `docker save` command to save an image to a tar archive.

```bash
# Save an image to a tar archive
docker save -o <path_to_tar_archive> <image_id_or_name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722001433611/42eab74b-27b6-4db0-848a-808cc94b2365.png align="center")

### Use the `docker load` command to load an image from a tar archive.

```bash
# Load an image from a tar archive
docker load -i <path_to_tar_archive>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722001500836/1efc57e9-c02b-46c9-a269-69409195d0c3.png align="center")

Thank you for reading!

<mark>© 2024 Anand Raval. All rights reserved.</mark>
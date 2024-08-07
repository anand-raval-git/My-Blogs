---
title: "Day 17  : Docker Project for DevOps Engineers"
seoTitle: "Docker Project for DevOps Engineers"
seoDescription: "Learn how to create a Dockerfile for a simple web application and manage Docker containers effectively. Perfect for DevOps Engineers!"
datePublished: Wed Aug 07 2024 13:41:44 GMT+0000 (Coordinated Universal Time)
cuid: clzjweeem000409lc5qv24vp4
slug: day-17-docker-project-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1723038066353/18f2ba4d-d55a-4279-8e42-4e6fdac74b94.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1723038091559/8fc8ff3f-bd44-48c4-9525-8255d3872dcf.png
tags: docker, devops, docker-images, 90daysofdevops, trainwithshubham

---

## Day 17 Task:

# Dockerfile

Docker is a tool that makes it easy to run applications in containers. Containers are like small packages that hold everything an application needs to run. To create these containers, developers use something called a Dockerfile.

A Dockerfile is like a set of instructions for making a container. It tells Docker what base image to use, what commands to run, and what files to include. For example, if you were making a container for a website, the Dockerfile might tell Docker to use an official web server image, copy the files for your website into the container, and start the web server when the container starts.

For more about Dockerfile, visit [here](https://rushikesh-mashidkar.hashnode.dev/dockerfile-docker-compose-swarm-and-volumes).

## Task

* Create a Dockerfile for a simple web application (e.g. a Node.js or Python app)
    
* Build the image using the Dockerfile and run the container
    
* Verify that the application is working as expected by accessing it in a web browser
    
* Push the image to a public or private repository (e.g. Docker Hub)
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722281426726/374826f5-b2a2-4ea2-aa3a-3aa58332b61c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722281433829/9aa56ba1-0fc7-4f80-8e3b-e512ab50f201.png align="center")

To write a Dockerfile, follow these steps:

1. **Choose a Base Image**: Start with a base image that suits your application. For example, if you're creating a Node.js application, you might use the official Node.js image.
    
2. **Set the Working Directory**: Define the working directory inside the container where your application code will reside.
    
3. **Copy Application Files**: Copy your application files from your local machine to the container.
    
4. **Install Dependencies**: Run commands to install any dependencies your application needs.
    
5. **Expose Ports**: Specify which ports the container should expose.
    
6. **Define the Command to Run the Application**: Specify the command that should be run when the container starts.
    

Here is an example Dockerfile for a simple Node.js application:

```Dockerfile
# Use the official Node.js image as the base image
FROM node:14

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install the dependencies
RUN npm install

# Copy the rest of the application files to the working directory
COPY . .

# Expose port 3000
EXPOSE 3000

# Define the command to run the application
CMD ["node", "app.js"]
```

Explanation of each line:

* `FROM node:14`: This line specifies the base image to use. In this case, it's the official Node.js image with version 14.
    
* `WORKDIR /app`: This sets the working directory inside the container to `/app`.
    
* `COPY package*.json ./`: This copies `package.json` and `package-lock.json` files to the working directory.
    
* `RUN npm install`: This runs the `npm install` command to install the dependencies listed in `package.json`.
    
* `COPY . .`: This copies the rest of the application files to the working directory.
    
* `EXPOSE 3000`: This exposes port 3000, which is the port the application will run on.
    
* `CMD ["node", "app.js"]`: This defines the command to run the application, which in this case is `node app.js`.
    

To build and run the Docker container:

1. **Build the Docker Image**:
    
    ```sh
    docker build -t my-node-app .
    ```
    
2. **Run the Docker Container**:
    
    ```sh
    docker run -p 3000:3000 my-node-app
    ```
    
3. **Verify the Application**: Open a web browser and go to [`http://localhost:3000`](http://localhost:3000) to verify that the application is running.
    
4. **Push the Image to a Repository**:
    
    ```sh
    docker tag my-node-app your-dockerhub-username/my-node-app
    docker push your-dockerhub-username/my-node-app
    ```
    

Replace `your-dockerhub-username` with your actual Docker Hub username.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723037490043/9daff972-23f8-465b-b0ea-1598226a2807.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723037449762/e0156369-77ff-4e75-a619-a2c5aed07455.png align="center")

```bash
plaintextCopy codeFlask==2.0.3
Werkzeug==2.0.3
```

### Rebuild Docker Image

After updating the `requirements.txt` file, rebuild your Docker image to install the correct versions of the dependencies.

```bash
bashCopy codedocker build -t tic-tac-toe .
```

### Verify Updated `requirements.txt`

Ensure your `requirements.txt` looks like this:

```bash
plaintextCopy codeFlask==2.0.3
Werkzeug==2.0.3
```

### Full Directory Structure and File Contents

Ensure your project directory structure and file contents are correct:

#### Directory Structure

```bash
plaintextCopy codetic_tac_toe/
├── app/
│   ├── __init__.py
│   ├── routes.py
│   └── static/
│       └── style.css
│   └── templates/
│       └── index.html
├── Dockerfile
├── requirements.txt
└── run.py
```

#### `app/__init__.py`

```bash
pythonCopy codefrom flask import Flask

app = Flask(__name__)

from app import routes
```

#### `app/`[`routes.py`](http://routes.py)

```bash
pythonCopy codefrom flask import render_template, request, jsonify
from app import app

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/make_move', methods=['POST'])
def make_move():
    data = request.get_json()
    board = data['board']
    player = data['player']
    
    # Here you should add the logic to check for a win or draw.
    result = {'status': 'ongoing'}  # This is just a placeholder.
    
    return jsonify(result)
```

#### `app/templates/index.html`

```bash
htmlCopy code<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic Tac Toe</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
</head>
<body>
    <h1>Tic Tac Toe</h1>
    <div id="board"></div>
    <script>
        const player = 'X'; // This should switch between 'X' and 'O' in actual game logic.
        let board = Array(9).fill(null);

        function createBoard() {
            const boardDiv = document.getElementById('board');
            boardDiv.innerHTML = '';
            board.forEach((cell, index) => {
                const cellDiv = document.createElement('div');
                cellDiv.classList.add('cell');
                cellDiv.dataset.index = index;
                cellDiv.addEventListener('click', () => makeMove(index));
                cellDiv.textContent = cell;
                boardDiv.appendChild(cellDiv);
            });
        }

        function makeMove(index) {
            if (board[index]) return;
            board[index] = player;
            createBoard();
            fetch('/make_move', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify({ board, player }),
            })
            .then(response => response.json())
            .then(data => {
                if (data.status === 'win') {
                    alert(`${player} wins!`);
                } else if (data.status === 'draw') {
                    alert('Draw!');
                } else {
                    // Switch player and continue
                }
            });
        }

        createBoard();
    </script>
</body>
</html>
```

#### `app/static/style.css`

```bash
cssCopy codebody {
    font-family: Arial, sans-serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    margin: 0;
}

h1 {
    margin-bottom: 20px;
}

#board {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    grid-gap: 10px;
}

.cell {
    width: 100px;
    height: 100px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2rem;
    background-color: #f0f0f0;
    cursor: pointer;
}
```

#### [`run.py`](http://run.py)

```bash
pythonCopy codefrom app import app

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=5000, debug=True)
```

#### `Dockerfile`

```bash
DockerfileCopy code# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set the working directory
WORKDIR /app

# Copy the current directory contents into the container
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Make port 5000 available to the world outside this container
EXPOSE 5000

# Run app.py when the container launches
CMD ["python", "run.py"]
```

#### `requirements.txt`

```bash
plaintextCopy codeFlask==2.0.3
Werkzeug==2.0.3
```

### Rebuild and Run the Docker Container

1. **Build the Docker Image:**
    
    ```bash
    bashCopy codedocker build -t tic-tac-toe .
    ```
    
2. **Run the Docker Container:**
    
    ```bash
    bashCopy codedocker run -d -p 5000:5000 tic-tac-toe
    ```
    
3. **Check Running Containers:**
    
    ```bash
    bashCopy codedocker ps
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723037773124/e37e8e95-fcfd-42d3-a816-6fc896eec45d.png align="center")
    
    Thank you for reading!
    
    <mark>© 2024 Anand Raval. All rights reserved.</mark>
---
title: "What is virtual environment and Introduction to FastAPI"
seoTitle: "Virtual Environments & FastAPI Intro Guide"
seoDescription: "Develop APIs with FastAPI, set up virtual environments, and deploy with CI/CD pipelines. Ideal for beginner Python developers"
datePublished: Mon May 12 2025 19:01:07 GMT+0000 (Coordinated Universal Time)
cuid: cmalg7y0e000509l83erd8tjp
slug: what-is-virtual-environment-and-introduction-to-fastapi
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1747076314626/9dd9061a-627e-4c61-8786-887b95159c16.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1747076419601/a0e9cbd7-2a98-4547-a66c-7a1166c7cbf3.png
tags: python, apis, python3, devops, 90daysofdevops

---

# **Python API Development with FastAPI**

Master Python API development with FastAPI, SQL integration, testing, and cloud deployment throughout blogs. Build robust APIs, automate testing, and deploy seamlessly with CI/CD pipelines. Everything you need to become a pro API developer.

Let’s start from beginner level.

* Install VS Code editor [link](https://code.visualstudio.com/download) For environment where we will write our code.
    
* Install Python [link](https://www.python.org/downloads/).
    
* Now open vs code and make one **folder** called **FASTAPI.**
    
* In that folder make one file called as main.py (.py is extension for code editor which can identify, this is file or code belongs to python).
    
* Open …&gt;terminal (Given below image you can see there is powershell change it to cmd).
    
* Now we have to make virtual environment for our project.
    

## What is virtual environment

Assume that we are working on 3 project in same machine and different project required different python version and dependency. so that means python virtual environments tool is just providing isolation for each project. it will create isolate space for project you can see image for more understanding.

![3 Ways to Set Up Virtual Environments | by Kay Jan Wong | Python in Plain  English](https://miro.medium.com/v2/resize:fit:1091/1*cAx4hY_TEGjbGN_ZcO9UKQ.png align="left")

Execute command given in image

* `py -3`: This tells the `py` (Python Launcher for Windows) to use the **Python 3** interpreter installed on your system.
    
* `venv`: This is the name of the Python module used for creating virtual environments.
    
* `venv` (the second one): This is the **name you are giving to your new virtual environment directory**. In this case, it will create a folder named `venv` in your current location.
    

```python
py -3 venv venv
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747029831785/4f2d72d9-bd67-4c41-baca-fbd25c8e4cab.png align="center")

After executing that command you will see in code editor new folder called venv is created for isolated environment for this project, you can see in below image.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747030862669/347213e9-426f-4800-b18b-ccf657236020.png align="center")

In venv folder you'll find a set of directories and files that constitute your isolated Python environment.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747030961433/9936a835-12d7-4876-aed6-a0c8534859d2.png align="center")

Now we will use venv environment for project so first of all we have to choose python interpreter for this project which is created earlier within venv.

* Click on serarch button in python code which is located on top of middle in your screen.
    
* Write &gt;python inter.
    
* Click on Python: Select Interpreter.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747031084167/346953af-f203-49d8-a934-eb325eb05276.png align="center")

Select Venv (Python 3.13.3) venv\\Scripts\\python.ext.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747031209258/cde44983-c2de-4e8f-bf43-20d3603bb406.png align="center")

Now to activate that virtual environment run activate file which is located in venv&gt;Scripts just execute below command in terminal (use cmd).

In below image you can see (venv) that means you are into virtual environment which we created earlier. Remember this very carefully whenever we use project this project we will work in this virtual environment, every time you have to execute this command when you are not in virtaul environment

```powershell
venv\Scripts\activate.bat
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747031554458/bdaa9e0f-a1a3-438b-a19c-75c17c896f66.png align="center")

Now i want to share a fast api documentation website. which will help you throught journey. for this project i am also using this fast api documentation [link](https://fastapi.tiangolo.com/tutorial/first-steps/)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747032002003/03689aaa-08c9-4830-9345-841e4dd49751.png align="center")

Now open your code editor and install fastapi all modules for this project. execute below command in terminal that will download all require packages or modules for this project.

```python
pip install Fastapi[all]
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747032212972/d1a03f61-2e5a-4f96-b1a0-1b5a116dae84.png align="center")

```python
pip freeze #you can see what packages or modules installed in virtual environment
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747032245700/aa916b37-8ac7-4bfc-baee-9821b881cea7.png align="center")

Now run below code in code editor

```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/")
async def root():
    return {"message": "Hello World"}
```

```python
unicorn main:app #run this command in terminal
```

`uvicorn main:app` **starts the Uvicorn ASGI server** to run a **modern, asynchronous Python web application**

It loads the application object named `app`

from the Python module `main` and makes it accessible over the network.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747032534959/08cb7992-3eef-406b-9baa-677d81863036.png align="center")

Open uvicorn running link on browser you will output like below image

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747032693627/af0deb2d-2f0c-4a83-8061-b511366a68b5.png align="center")

That’s it for today guys in next blog we will understand about that code, hope you got all points which i shared you throughout this blog if you have any question or doubts you can free feel to reach out me

Thankyou for reading this blog !!!!!!!!!!
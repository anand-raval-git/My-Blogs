---
title: "Day 12 :-🛠️ Easy Guide to Git and GitHub Basics"
seoTitle: "Beginner's Guide to Git and GitHub"
seoDescription: "Learn Git and GitHub basics including version control, branching, collaboration, repository creation, and more in this easy-to-follow guide"
datePublished: 2024-07-25T12:49:05.523Z
cuid: clz19sm42000109mfe1bv8npp
slug: day-12-easy-guide-to-git-and-github-basics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1721911702942/eb70bcac-60a7-49c9-8b4e-0db0a6e7e232.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1721911730673/575b52f5-bb8f-4d85-97bc-b9b8ee7c6295.png
tags: github, git, devops, 90daysofdevops, trainwithshubham

---

## Day 12 :- TASK

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721309232627/957d35db-e9ec-430e-9f5e-bcbb75878165.png align="center")

## • What is Git and why is it important?

Git is a version control system that helps people manage and track changes to their files and projects. Imagine you're working on a document, and you make several changes over time. Git allows you to save snapshots of your document at different stages, so you can go back to any previous version if needed.

Here’s why Git is important:

1. **Version Tracking**: Git keeps a history of all changes made to your files. This means you can see what changes were made, who made them, and when they were made. If you make a mistake, you can easily revert to an earlier version.
    
2. **Collaboration**: If you're working with others on the same project, Git makes it easy to collaborate. Multiple people can work on the same files simultaneously without overwriting each other's work. Git merges the changes, ensuring everyone has the latest version.
    
3. **Backup**: By saving your project in a Git repository, you have a backup of your work. If your computer crashes, you can retrieve your project from the repository.
    
4. **Branching and Merging**: Git allows you to create branches, which are separate lines of development. You can work on a new feature or experiment without affecting the main project. Once you're satisfied with the changes, you can merge the branch back into the main project.
    
5. **Open Source Projects**: Many open-source projects use Git. Learning Git allows you to contribute to these projects and collaborate with a global community of developers.
    

## • What is the difference between Main Branch and Master Branch?

The terms "Main Branch" and "Master Branch" in Git refer to different default branches in a repository. Historically, "master" was the default branch name created when you initialized a new Git repository. However, many projects and organizations have shifted to using "main" as the default branch name. Here are the key differences and reasons for the change:

1. **Naming Convention**:
    
    * **Master Branch**: This was the traditional default branch name in Git.
        
    * **Main Branch**: This is the newer default branch name that many projects have adopted.
        
2. **Purpose**: Both branches serve the same purpose, which is to act as the primary branch where the stable and production-ready code resides.
    
3. **Cultural Shift**: The change from "master" to "main" is part of a broader movement to use more inclusive and neutral terminology in software development. The term "master" can be associated with slavery, which has led to a push for more inclusive language in technology.
    
4. **Configuration**: When you create a new repository, you can configure Git to use "main" instead of "master" as the default branch name. This can be done using Git settings or through repository hosting services like GitHub, which now default to "main".
    

the difference is primarily in the naming convention, with "main" being the more modern and inclusive term replacing "master". Both branches function the same way in terms of Git operations. The change to "main" reflects a commitment to more inclusive language in the tech community.

> What is the default branch in Git? Answer:- Master
> 
> What is the default branch in GitHub? Answer:- Main

## • Can you explain the difference between Git and GitHub?

Git and GitHub are related but serve different purposes.

**Git**:

* **What It Is**: Git is a tool that helps you keep track of changes to your files. Think of it as a supercharged "undo" button for your projects.
    
* **How It Works**: When you make changes to a file, Git allows you to save snapshots of your work at different stages. If you make a mistake, you can go back to an earlier version.
    
* **Why It's Useful**: It helps you manage your work, collaborate with others without overwriting each other's changes, and keep a history of all modifications.
    

**GitHub**:

* **What It Is**: GitHub is a website where you can store your Git projects online. It's like a social network for code.
    
* **How It Works**: You upload your Git projects to GitHub, making them accessible from anywhere. You can also share your projects with others, collaborate on them, and even contribute to other people's projects.
    
* **Why It's Useful**: It provides a central place to store your work, collaborate with others, and showcase your projects to potential employers or collaborators.
    

> **Git** is the tool you use on your computer to track changes to your files.

> **GitHub** is a website where you can store those files and collaborate with others.

> Think of Git as the engine of a car and GitHub as the garage where you park and show off your car.

## • How do you create a new repository on GitHub?

1. Go to GitHub.
    
2. Click on the + icon in the top right corner.
    
3. Select New repository.
    
4. Enter a repository name (e.g., "DevOps").
    
5. Click Create repository.
    

## • What is the difference between a local & remote repository? How to connect local to remote?

A local repository is a version-controlled directory on your computer where you can manage and track changes to your files using Git. A remote repository, on the other hand, is a version-controlled directory hosted on a server (such as GitHub, GitLab, or Bitbucket) that allows you to share your project with others and collaborate.

### Differences:

1. **Location**:
    
    * **Local Repository**: Stored on your local machine.
        
    * **Remote Repository**: Stored on a remote server.
        
2. **Access**:
    
    * **Local Repository**: Accessible only from your local machine.
        
    * **Remote Repository**: Accessible from anywhere with an internet connection.
        
3. **Collaboration**:
    
    * **Local Repository**: Primarily for individual use.
        
    * **Remote Repository**: Facilitates collaboration among multiple users.
        

## 1st Method :- using ssh public key

1. go to github
    
2. go to settings
    
3. click on ssh and gpg key
    
4. click on new ssh key
    
5. paste public key of local system
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721414380171/56181d0b-2abf-4906-a53e-059781fd7942.png align="center")

## How to find local ssh key ?

```bash
ssh-keygen
cd .ssh
#go into .pub file and copy it
```

## How can we push file from local to remote

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721414552790/dd2385bc-bcfd-4891-b923-338eab804df4.png align="center")

1. Now clone remote to local using ssh
    
    ```bash
    git clone #ssh link
    ```
    
2. go into repo
    
    ```bash
    cd #reponame
    ```
    
3. use those command for push something from local to remote
    
    ```bash
    git init
    git status
    git add #filename
    git commit -m "message"
    git push origin main
    #if you want to pull something from remote to local
    git pull origin #filename
    ```
    

## 2nd Method :- using toekns

1. go to github setting
    
2. click on devloper setting
    
3. click on personal access token
    
4. click on Tokens (classic)
    
5. click on generate new token
    
6. copy that token
    
7. go into local
    

## Use these command in local machine

```bash
fit remote -v
git remote set-url origin
```

Thank you for reading!

<mark>© 2024 Anand Raval. All rights reserved.</mark>
---
title: "Day 8 :- 🖥️ Exploring Bash Scripting Fundamentals"
seoDescription: "Explore bash scripting basics: comments, echo, variables, and wildcards. Learn through hands-on tasks in this comprehensive guide"
datePublished: Fri Jul 19 2024 15:55:55 GMT+0000 (Coordinated Universal Time)
cuid: clysvtrrf000x08lhcjwnd39h
slug: day-8-exploring-bash-scripting-fundamentals
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1721404512655/3b68df62-e7dd-4ea0-b066-c01fa9ee48ce.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1721404544947/c19465c4-36e3-4aff-8d19-a758f0ff3473.png
tags: bash, devops, script, 90daysofdevops, trainwithshubham

---

## Day 8 :- TASK

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721218903174/38973c53-f7e7-45d4-a44d-1e666d7368d2.png align="center")

## • Task 1: Comments

In bash scripts, comments are used to add explanatory notes or disable certain lines of code. Your task is to create a bash script with comments explaining what the script does.

```bash
#!/bin/bash
<<readme
info: this script will give you date and time
readme

#this script will print date and time

#print the current time and date
echo "Date and time is $(date)"

#print welcome message
echo "Welcome to scripting challenge"

#end of script
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721219535849/97b0102e-b599-4600-9f72-a11c95b0095e.png align="center")

## • **Echo**

The echo command is used to display messages on the terminal. Your task is to create a bash script that uses echo to print a message of your choice.

```bash
#!/bin/bash
<<readme
info : this file will print use of echo
readme


echo "Hello everyone this is my day08 of devops jounrey stay tuned"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721219723002/449aaed3-be4c-4b0b-8d4d-c4a9bd190a83.png align="center")

## • **Variables**

Variables in bash are used to store data and can be referenced by their name. Your task is to create a bash script that declares variables and assigns values to them.

```bash
#!/bin/bash


name="Anand Raval"
challenge="90DaysOfDevops"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721219967024/60c5b67d-d711-4047-b757-d23eb3244c14.png align="center")

## • **Using Variables**

Now that you have declared variables, let's use them to perform a simple task. Create a bash script that takes two variables (numbers) as input and prints their sum using those variables.

```bash
#!/bin/bash


read -p "Enter value of A:" a
read -p "Enter value of B:" b

sum=$((a+b))

echo "$a+$b=$sum"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721220334431/53c68769-f719-4020-bef6-e05e85a206a5.png align="center")

## • **Using Built-in Variables**

Bash provides several built-in variables that hold useful information. Your task is to create a bash script that utilizes at least three different built-in variables to display relevant information.

```bash
#!/bin/bash

echo "Current loged in user:$USER"
echo "Home directory:$HOME"
echo "Current shell:$SHELL"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721242316024/45389691-7a2d-4427-89ff-113933bd5b40.png align="center")

## • **Wildcards**

Wildcards are special characters used to perform pattern matching when working with files. Your task is to create a bash script that utilizes wildcards to list all the files with a specific extension in a directory

```bash
#!/bin/bash


echo "printing all list of directories"

ls *.txt
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721242605663/4f5c7b6f-573b-474b-835e-b536e90615ee.png align="center")

Thank you for reading!

<mark>© 2024 Anand Raval. All rights reserved.</mark>
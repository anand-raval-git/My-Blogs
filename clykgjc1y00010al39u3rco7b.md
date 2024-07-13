---
title: "Day 5 Task :- Mastering Shell Scripts for Directory Creation and Automated Backups 🗂️💾"
seoTitle: "Mastering Shell Scripts for Directory Creation and Automated Backup"
seoDescription: "Learn to master shell scripting for directory creation, automated backups, and user management with cron and crontab in just one day"
datePublished: Sat Jul 13 2024 18:25:44 GMT+0000 (Coordinated Universal Time)
cuid: clykgjc1y00010al39u3rco7b
slug: day-5-task-mastering-shell-scripts-for-directory-creation-and-automated-backups
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720894932447/334acaa1-1b65-4002-8323-f6e7ac711dc1.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1720895111515/c4f29868-a84a-4af1-8d9e-8b5325c0f20e.png
tags: devops, shell-script, devops-journey, 90daysofdevops, trainwithshubham

---

## Day 5 :- TASK

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720878143147/0cb8ba77-ea43-4d12-b15b-d1ff6e706ecb.png align="center")

## 1.**Create Directories Using Shell Script:**

* Write a bash script [`createDirectories.sh`](http://createDirectories.sh) that, when executed with three arguments (directory name, start number of directories, and end number of directories), creates a specified number of directories with a dynamic directory name.
    
    ```bash
    <<readme
    info:This file will create directories as per given argument
    createDirectories.sh <directory name> <start number of directories> <end number of directories>
    readme
    
    directory_name=$1
    start_number=$2
    end_number=$3
    
    if [ $# -ne 3 ]; then
            echo "usage : $0 day 1 90"
            exit 1
    fi
    
    for ((i=start_number; i<=end_number; i++))
    do
            mkdir "${directory_name}${i}"
    done
    
    echo "Directories created from ${directory_name}${start_number} to ${directory_name}${end_number}"
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720879394219/ab564db5-ea62-4b8c-a01d-66824a9a3177.png align="center")
    

Example 1: When executed as `./`[`createDirectories.sh`](http://createDirectories.sh)`day 1 90`, it creates 90 directories as `day1 day2 day3 ... day90`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720880159263/c17f5ced-abfb-4861-9c34-58e86279bdea.png align="center")

* Example 2: When executed as `./`[`createDirectories.sh`](http://createDirectories.sh)`Movie 20 50`, it creates 31 directories as `Movie20 Movie21 Movie22 ... Movie50`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720880285140/e413b22c-7513-41ea-b6dd-8f1f53689b6c.png align="center")
    

## 2.**Create a Script to Backup All Your Work:**

```bash
#!/bin/bash
<<readme
info : This script will create backup
./createBackup.sh <source_dir> <target_dir>
readme

source_dir=$1
target_dir=$2
timestamp=$(date "+%Y-%m-%d-%H-%M-%S")

backup_dir="${target_dir}/backup_${timestamp}"

zip -r "${backup_dir}.zip" "${source_dir}" >  /dev/null

if [ $? -eq 0 ]; then
        echo "backup_${timestamp} created successfully"
else
        echo "Backup was not perfomed backup_${timestamp}"
fi
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720882115049/07481d1b-4763-4b0a-898f-67068a36e9cc.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720882151855/d869334a-c318-4395-8944-9c7e342b00dd.png align="center")

## 3.**Read About Cron and Crontab to Automate the Backup Script:**

* Cron is the system's main scheduler for running jobs or tasks unattended. A command called crontab allows the user to submit, edit, or delete entries to cron. A crontab file is a user file that holds the scheduling information
    
    ```bash
    * * * * * bash /home/ubuntu/backup.sh /home/ubuntu/backup /home/ubuntu/devo
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720893695002/dc2dd733-b1c4-40ea-aee8-1f2b2dd013ce.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720893665377/6041ad21-a6e6-4d23-8ac4-403522efbb3f.png align="center")
    
    ## 4.**Read About User Management:**
    
* A user is an entity in a Linux operating system that can manipulate files and perform several other operations. Each user is assigned an ID that is unique within the system. IDs 0 to 999 are assigned to system users, and local user IDs start from 1000 onwards.
    
* Create 2 users and display their usernames.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720894773363/c41a7f1f-78a4-43bf-86ae-973f8bcd519e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720894810082/7276750d-eb69-4f27-8b95-c1960ede316d.png align="center")

Thank you for reading!

<mark>© 2024 Anand Raval. All rights reserved.</mark>
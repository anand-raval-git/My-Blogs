---
title: "Day 9 :- Shell Scripting Challenge: 📂 Directory Backup with Rotation 🔄"
seoTitle: "Directory Backup & Rotation Shell Script"
seoDescription: "Learn to create automated directory backups with rotation using shell scripting in Day 9 of the challenge"
datePublished: 2024-07-23T15:35:38.123Z
cuid: clyykv34a00020ala85ds6ry3
slug: day-9-shell-scripting-challenge-directory-backup-with-rotation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1721748238282/fd99f339-c40b-44a1-a9aa-38448ad10367.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1721748267317/8f523dfe-e626-40e9-85ed-abe2a3d54a16.png
tags: bash, devops, shell-script, 90daysofdevops, trainwithshubham

---

## Day 9 :- TASK

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721465699913/21445a6b-db44-45e6-9cd4-a54e9d1c09c5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721465720583/7ae45b7c-2634-4424-ac9e-ad058b260455.png align="center")

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

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721499108535/4749a9e9-42fb-43cc-a231-6a7708d76040.png align="center")

Thank you for reading!

<mark>© 2024 Anand Raval. All rights reserved.</mark>
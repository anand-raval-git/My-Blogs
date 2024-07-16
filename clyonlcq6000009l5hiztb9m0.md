---
title: "Day 6 Task :- 🔐 Understanding and Managing File Permissions in Linux: A Comprehensive Guide 📁"
seoTitle: "Linux File Permissions: Comprehensive Guide"
seoDescription: "Learn Linux file permissions: ownership, groups, ACLs, Sticky Bit, SUID, and SGID. Complete tasks to manage permissions effectively"
datePublished: Tue Jul 16 2024 16:54:21 GMT+0000 (Coordinated Universal Time)
cuid: clyonlcq6000009l5hiztb9m0
slug: day-6-task-understanding-and-managing-file-permissions-in-linux-a-comprehensive-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1721148623192/ec7b82ef-13b9-41af-8368-a1abf0c216be.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1721148657881/5de36b23-3e40-4be2-b96e-36ab5c7b902f.png
tags: ubuntu, devops, file-permission, 90daysofdevops

---

## Day 6 :- TASK

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720900234765/8b608f9c-ebe3-4b3a-9642-4996d970dc6e.png align="center")

## • **Understanding File Permissions:**

1. * Create a simple file and run `ls -ltr` to see the details of the files. [Refer to Notes](https://github.com/LondheShubham153/90DaysOfDevOps/tree/master/2023/day06/notes)
        
    * Each of the three permissions are assigned to three defined categories of users. The categories are:
        
        * **Owner:** The owner of the file or application.
            
            * Use `chown` to change the ownership permission of a file or directory.
                
        * **Group:** The group that owns the file or application.
            
            * Use `chgrp` to change the group permission of a file or directory.
                
        * **Others:** All users with access to the system (outside the users in a group).
            
            * Use `chmod` to change the other users' permissions of a file or directory.
                
    * Task: Change the user permissions of the file and note the changes after running `ls -ltr`.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720957193954/d09b7c17-3872-4360-86c7-c89fc5dbbe2c.png align="center")
        
        ## • What is file permissions ?
        
        file permissions determine who can read, write, or execute a file. These permissions are represented by a combination of letters and symbols and are divided into three categories: owner user, group, and others users.
        
        1. **Owner user**: The user who owns the file.
            
        2. **Group**: The group that owns the file.
            
        3. **Others users**: All other users.
            
        
        Each category has three types of permissions:
        
        * **Read (r)**: Permission to read the file.
            
        * **Write (w)**: Permission to modify the file.
            
        * **Execute (x)**: Permission to execute the file (if it is a script or a program).
            
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720450650753/41a257b2-762a-46af-9970-444fb0595afe.png align="center")
        
        The permissions are displayed using the `ls -l` command, which shows a string of 10 characters. For example:
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720450695542/6bd4b931-d803-468f-8a42-8af747b1b21b.png align="center")
        
        You can see in this image drwxrwxr -&gt; in there d stand for directory and if there is (-) means it is a file
        
        Truth table for permission:-
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720450803197/36c16b9c-1ae3-4c74-b95a-76a3c6c11322.png align="center")
        
        1 means ture and 0 means false
        
        how to change file permission
        
    * How to change owner
        
        ```bash
        chown #username #filename
        ```
        
    
    How to change group
    

```bash
chgrp #groupname #file name
```

How to change file permissiom

```bash
chmod #value #filename
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720450966980/cddf7fd8-0828-43ed-ac42-059a05bbd7bb.png align="left")

## • **Access Control Lists (ACL):**

1. * Read about ACL and try out the commands `getfacl` and `setfacl`.
        
    * Task: Create a directory and set specific ACL permissions for different users and groups. Verify the permissions using `getfacl`.
        

Access Control Lists (ACL) provide a more flexible permission mechanism for file systems by allowing you to set permissions for individual users or groups beyond the standard owner, group, and others.

### **Steps to Use ACL:**

1. **Create a Directory:**
    
    ```bash
    mkdir acl  #first install acl usign sudo apt install acl
    ```
    
2. **Set ACL Permissions:** Use the `setfacl` command to set specific ACL permissions. For example, to give read and write permissions to user `user1` and read permissions to group `group1`:
    
    ```bash
    setfacl -m u:user1:rw my_directory
    setfacl -m g:group1:r my_directory
    ```
    
3. **Verify ACL Permissions:** Use the `getfacl` command to verify the ACL permissions set on the directory:
    
    ```bash
    getfacl my_directory
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720958157219/f82c34ee-b1a8-45a7-b624-a8bb9e822f52.png align="center")
    
    ## • **Additional Tasks:**
    

* **Task:** Create a script that changes the permissions of multiple files in a directory based on user input.
    
* **Task:** Write a script that sets ACL permissions for a user on a given file, based on user input.
    

```bash
#!/bin/bash

read -p "Enter path:" path
read -p "Enter permission:" permission
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720985333146/d2613ec8-7bf9-41e0-8269-598631b02a33.png align="center")

```bash
#!/bin/bash


read -p "Enter file path:" path
read -p "Enter username:" user
read -p "Enter permission(Ex:-rw,r,w):" permission

sudo setfacl -m u:$username:$permission $path
```

* ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720984826457/f5305e8f-0ca6-4324-92d6-edf46aa71199.png align="center")
    

## • **Understanding Sticky Bit, SUID, and SGID:**

* Read about sticky bit, SUID, and SGID.
    
* Task: Create examples demonstrating the use of sticky bit, SUID, and SGID, and explain their significance.
    

Sticky Bit, SUID, and SGID are special types of file permissions in Unix-like operating systems that provide additional security and functionality.

### Sticky Bit:

* **Purpose:** The sticky bit is used on directories to restrict file deletion. When the sticky bit is set on a directory, only the file's owner, the directory's owner, or the root user can delete or rename the files within that directory.
    
* **Usage Example:** Commonly used on directories like `/tmp` to prevent users from deleting each other's files.
    
* **Command to Set:**`chmod +t directory_name`
    
* **Example:**
    
    ```sh
    mkdir /tmp/testdir
    chmod +t /tmp/testdir
    ls -ld /tmp/testdir
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720986299929/95c01710-334f-47de-b8a7-cd17c79b551a.png align="center")
    
    The output will show a `t` at the end of the permissions string, indicating the sticky bit is set.
    

### SUID (Set User ID):

* **Purpose:** When the SUID bit is set on an executable file, it allows the file to be executed with the permissions of the file owner, rather than the user running the file. This is often used to allow users to execute programs with elevated privileges.(if there s in permission then any user can execute file cause that assume as root,if anyone will execute file this will say that rot user did it)
    
* **Usage Example:** Commonly used on programs like `passwd` to allow users to change their passwords.
    
* **Command to Set:**`chmod u+s file_name`
    
* **Example:**
    
    ```sh
    chmod u+s /path/to/executable
    ls -l /path/to/executable
    ```
    
    The output will show an `s` in the owner's execute position, indicating the SUID bit is set.
    

### SGID (Set Group ID):

* **Purpose:** When the SGID bit is set on a directory, new files and subdirectories created within inherit the group ID of the directory, rather than the primary group of the user who created the file. When set on an executable, it allows the file to be executed with the permissions of the group owner.
    
* **Usage Example:** Useful for collaborative directories where files need to be accessible by a specific group.
    
* **Command to Set:**`chmod g+s directory_name` or `chmod g+s file_name`
    
* **Example:**
    
    ```sh
    mkdir /shared
    chgrp somegroup /shared
    chmod g+s /shared
    ls -ld /shared
    ```
    
    The output will show an `s` in the group's execute position, indicating the SGID bit is set.
    

## • **Backup and Restore Permissions:**

* Task: Create a script that backs up the current permissions of files in a directory to a file.
    
* Task: Create another script that restores the permissions from the backup file.
    

```bash
#!/bin/bash


read -p "Enter path of directory" dir

getfacl -R $dir >> file.txt
echo "permisson backup successfully"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721147622047/dcb9d178-ed9d-4b5d-84ff-cb3602f285de.png align="center")

```bash
#!/bin/bash

echo "Enter file of path:"
read backup

setfacl --restore=$backup
echo "Permission restored successfully"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721148428766/3dc423f9-34a8-4663-87ec-44d46721748f.png align="center")

Thank you for reading!

<mark>© 2024 Anand Raval. All rights reserved.</mark>
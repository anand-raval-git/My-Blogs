---
title: "Day 4 [Part :- 1] :- Managing Users, Groups, and File Permissions in Ubuntu: A Comprehensive Guide"
seoTitle: "Ubuntu User, Group, Permission Guide"
seoDescription: "Comprehensive guide to managing users, groups, and file permissions on Ubuntu. Includes commands for adding users, groups, and changing permissions"
datePublished: 2024-07-08T15:09:59.730Z
cuid: clyd4cc36000609jsgow8g3tx
slug: day-4-part-1-managing-users-groups-and-file-permissions-in-ubuntu-a-comprehensive-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720553844964/be005af3-1e5f-40cb-a5ad-e394cd7ef4ed.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1720553858285/34a3aeb3-12d4-4130-b315-a936df50b545.png
tags: ubuntu, cli, devops, 90daysofdevops, trainwithshubham

---

## • How to add User ?

```bash
sudo adduser #user_name
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720379559488/8421fd9d-098d-46a6-857c-3d41a154c83f.png align="center")

## • How to Check User added or not ?

```bash
sudo cat /etc/passwd
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720379973303/33b7b581-c443-4d15-9b6d-f79662cb893f.png align="center")

## • How to add password ?

```bash
sudo passwd #username
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720380141058/44a398a1-da3f-49a6-8a7e-546782438210.png align="center")

## • How to Check user property?

```bash
sudo cat /etc/passwd | grep "#username"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720380280377/d50741f2-720b-4c0a-9086-21c88006618a.png align="center")

## • How to switch user?

```bash
su #username
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720380415610/a4f850ff-1c25-4af6-b7c0-8afd88d009d8.png align="center")

## • How to exit from user?

```bash
exit
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720380439687/25bf9929-620c-4a41-9833-420eed6ac5ec.png align="center")

## • How to delete user?

```bash
sudo userdel #username
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720380556342/71c33532-86d8-4d29-8025-d06bb9224f17.png align="center")

user deleted or not ? let's check it

```bash
sudo cat /etc/passwd
```

## • How to change user login name?

```bash
sudo usermod -l #newname #existance_user_name
```

## • What is group?

a group is a collection of users that share the same permissions and access rights to files, directories, and other system resources. Groups are used to simplify the management of user permissions. Instead of assigning permissions to each user individually, you can assign permissions to a group, and all users in that group will inherit those permissions.

For example, if you have a group called "developers" and you want all members of this group to have access to a specific directory, you can set the permissions for the directory to allow access to the "developers" group. Any user added to the "developers" group will automatically have access to that directory.

> Note :- If you add user then that will automatically add in group for example create user and check sudo cat /etc/group command you will get user name in group section

## • How to add group?

```bash
sudo groupadd #groupname
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720449271808/a30eca05-1791-4698-94f3-a69bfeed0ebd.png align="center")

## • How to delete group?

```bash
sudo groupdel #groupname
```

## • How to add user in group?

```bash
sudo usermod -aG #grou_name #user_name
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720449512496/362b76db-1598-41ee-b741-ebc9b8789063.png align="center")

## • How to check group property ? or group created or not ?

```bash
sudo cat /etc/group
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720449579716/5591fe2c-1712-4888-bdae-fa337841eee7.png align="center")

## • How to check group admin property ?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720449686402/07906482-edc1-45b8-b7da-b8117cb1b2e6.png align="center")

## • How to Remove group member ?

```bash
sudo gpasswd -d #user #group
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720449882668/308e73b1-0ac6-416f-8d6a-5bc1972d0725.png align="center")

## • How to make group admin ?

```bash
sudo gpasswd -A #username #groupname
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720450153029/8304bd6b-6ed7-4f11-a9a8-ceeafade83b1.png align="center")

## • How to add single member in group ?

```bash
sudo gpasswd -a  #username #groupname
```

## • How to add multiple member in group ?

```bash
sudo gpasswd -M #username1 #username2 #group
```

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

```bash
chmod 777 #filename/directoryname
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720450966980/cddf7fd8-0828-43ed-ac42-059a05bbd7bb.png align="center")

Thank you for reading!

<mark>© 2024 Anand Raval. All rights reserved.</mark>
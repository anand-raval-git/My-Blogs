---
title: "Day 14: 📝Create a Linux & Git-GitHub Cheat Sheet 📋"
seoTitle: "Linux & Git-GitHub Cheat Sheet Creation"
seoDescription: "Comprehensive Linux and Git-GitHub cheat sheet covering command usage, descriptions, and examples for efficient learning and quick reference"
datePublished: 2024-07-29T14:04:43.098Z
cuid: clz7299zu000209jyeogv1vmn
slug: day-14-create-a-linux-git-github-cheat-sheet
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1722261840417/c7874559-d6df-44f2-b723-7cddc8d4ed89.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1722261861405/c14116ab-b58a-4ec5-9bea-0d1ba679c9aa.png
tags: github, git, devops, 90daysofdevops, trainwithshubham

---

## Linux & Git-GitHub Cheat Sheet

### Linux Commands

1. **ls**
    
    * **Description**: Lists directory contents.
        
    * **Usage**: `ls [options] [directory]`
        
    * **Example**: `ls -l /home/user`
        
2. ### `ls *.sh`
    
    * **Description**: Lists all files in the current directory with a `.sh` extension.
        
    * **Usage**: `ls *.sh`
        
    * **Example**: If you have files named [`script1.sh`](http://script1.sh), [`script2.sh`](http://script2.sh), and `readme.txt` in the current directory, running `ls *.sh` will display:
        
    
3. ### `ls -i`**Command**
    
    * **Description**: Lists directory contents along with their inode numbers.
        
    * **Usage**: `ls -i [directory]`
        
    * **Example**: If you run `ls -i` in a directory, you might see output like:
        
        ```bash
        1234567 file1.txt
        1234568 file2.sh
        1234569 directory1
        ```
        
    
4. ### `ls -d */`
    
    * **Description**: Lists only directories in the current directory.
        
    * **Usage**: `ls -d */`
        
    * **Example**: If you have directories named `dir1`, `dir2`, and files named `file1.txt`, [`file2.sh`](http://file2.sh) in the current directory, running `ls -d */` will display:
        
        ```bash
        dir1/
        dir2/
        ```
        
    
5. **mkdir**
    
    * **Description**: Make new folder.
        
    * **Usage**: `mkdir [directory name]`
        
    * **Example**: `mkdir new folder`
        
6. **mkdir\[hidden\]**
    
    * **Description**: Make hidden new folder.
        
    * **Usage**: `mkdir .[directory name]`
        
    * **Example**: `mkdir .newfolder`
        
7. **mkdir\[multiple\]**
    
    * **Description**: Make multiple new folder.
        
    * **Usage**: `mkdir [folder1] [folder 2]`
        
    * **Example**: `mkdir A B C D`
        
8. **mkdir\[nested folder\]**
    
    * **Description**: Make nested new folder.
        
    * **Usage**: `mkdir -p`
        
    * **Example**: `mkdir -p A/B/C/D`
        
9. **cd**
    
    * **Description**: Changes the current directory.
        
    * **Usage**: `cd [directory]`
        
    * **Example**: `cd /var/log`
        
10. ### `cd`
    
    * **Description**: Changes the current directory to the user's home directory.
        
    * **Usage**: `cd` or `cd ~`
        
    * **Example**: If you are in `/home/user/documents`, running `cd` will take you to `/home/user`.
        
    
11. ### `cd ..`
    
    * **Description**: Changes the current directory to the parent directory.
        
    * **Usage**: `cd ..`
        
    * **Example**: If you are in `/home/user/documents`, running `cd ..` will take you to `/home/user`.
        
    
12. ### `cd ../..`
    
    * **Description**: Changes the current directory to the grandparent directory (two levels up).
        
    * **Usage**: `cd ../..`
        
    * **Example**: If you are in `/home/user/documents/projects`, running `cd ../..` will take you to `/home/user`.
        
    
    This command is useful for quickly navigating up multiple levels in the directory hierarchy.
    
13. * ### `cd -`
        
        * **Description**: **Go to the last working directory.**
            
        * **Usage**: `cd -`
            
        * **Example**: If you are in `/home/user/documents` and you switch to `/var/log`, running `cd -` will take you back to `/home/user/documents`.
            
        
14. **pwd**
    
    * **Description**: Prints the current working directory.
        
    * **Usage**: `pwd`
        
    * **Example**: `pwd`
        
15. ### `tail`
    
    * **Description**: Displays the last part of a file.
        
    * **Usage**: `tail [options] [file]`
        
    * **Example**: `tail -n 10 file.txt` will display the last 10 lines of `file.txt`.
        
    
16. ### `head`
    
    * **Description**: Displays the first part of a file.
        
    * **Usage**: `head [options] [file]`
        
    * **Example**: `head -n 10 file.txt` will display the first 10 lines of `file.txt`.
        
    
17. **cp**
    
    * **Description**: Copies files or directories.
        
    * **Usage**: `cp [options] source destination`
        
    * **Example**: `cp file.txt /home/user/`
        
18. **mv**
    
    * **Description**: Moves or renames files or directories.
        
    * **Usage**: `mv [options] source destination`
        
    * **Example**: `mv oldname.txt newname.txt`
        
19. **rm**
    
    * **Description**: Removes files or directories.
        
    * **Usage**: `rm [options] file`
        
    * **Example**: `rm -r /home/user/temp`
        
20. ### `useradd`
    
    * **Description**: Creates a new user account.
        
    * **Usage**: `useradd [options] username`
        
    * **Example**: `useradd newuser`
        
    
21. ### `usermod`
    
    * **Description**: Modifies an existing user account.
        
    * **Usage**: `usermod [options] username`
        
    * **Example**: `usermod -aG sudo newuser` (adds `newuser` to the `sudo` group)
        
    
22. ### `userdel`
    
    * **Description**: Deletes a user account.
        
    * **Usage**: `userdel [options] username`
        
    * **Example**: `userdel newuser`
        
    
23. ### `groupadd`
    
    * **Description**: Creates a new group.
        
    * **Usage**: `groupadd [options] groupname`
        
    * **Example**: `groupadd newgroup`
        
    
24. ### `groupmod`**Command**
    
    * **Description**: Modifies an existing group.
        
    * **Usage**: `groupmod [options] groupname`
        
    * **Example**: `groupmod -n newgroupname oldgroupname` (renames `oldgroupname` to `newgroupname`)
        
    
25. ### `groupdel`**Command**
    
    * **Description**: Deletes a group.
        
    * **Usage**: `groupdel groupname`
        
    * **Example**: `groupdel newgroup`
        
    
26. ### `sudo cat /etc/passwd`
    
    * **Description**: Displays the contents of the `/etc/passwd` file, which contains user account information.
        
    * **Usage**: `sudo cat /etc/passwd`
        
    * **Example**: Running `sudo cat /etc/passwd` will display lines similar to:
        
        ```bash
        root:x:0:0:root:/root:/bin/bash
        user:x:1000:1000:User Name,,,:/home/user:/bin/bash
        ```
        
    
27. ### `sudo usermod -l newname existing_username`
    
    * **Description**: Changes the login name of an existing user.
        
    * **Usage**: `sudo usermod -l newname existing_username`
        
    * **Example**: If you want to change the username `olduser` to `newuser`, you would run:
        
    
28. ### `sudo gpasswd -d user group`
    
    * **Description**: Removes a user from a group.
        
    * **Usage**: `sudo gpasswd -d user group`
        
    * **Example**: If you want to remove the user `john` from the group `developers`, you would run:
        
        ```bash
        sudo gpasswd -d john developers
        ```
        
    
29. ### `sudo gpasswd -A username groupname`
    
    * **Description**: Assigns a user as the administrator of a group.
        
    * **Usage**: `sudo gpasswd -A username groupname`
        
    * **Example**: If you want to assign the user `john` as the administrator of the group `developers`, you would run:
        
        ```bash
        sudo gpasswd -A john developers
        ```
        
    
30. ### `grep`**Command**
    
    #### **Basic Usage**
    
    * **Description**: Searches for patterns in files.
        
    * **Usage**: `grep 'pattern' filename`
        
    * **Example**: To search for the word "error" in `logfile.txt`, you would run:
        
        ```bash
        grep 'error' logfile.txt
        ```
        
    
    #### **Multiple Files**
    
    * **Description**: Searches for a pattern in multiple files.
        
    * **Usage**: `grep "pattern" filename1 filename2`
        
    * **Example**: To search for the word "error" in both `logfile1.txt` and `logfile2.txt`, you would run:
        
        ```bash
        grep "error" logfile1.txt logfile2.txt
        ```
        
    
    #### **Printing with Line Numbers**
    
    * **Description**: Prints the line number along with the matching lines.
        
    * **Usage**: `grep -n "pattern" filename`
        
    * **Example**: To search for the word "error" in `logfile.txt` and print the line numbers, you would run:
        
        ```bash
        grep -n "error" logfile.txt
        ```
        
    
31. ### `find`**Command**
    
    * **Description**: Searches for files and directories in a directory hierarchy based on specified criteria.
        
    * **Usage**: `find [path] [expression]`
        
    * **Example**: To find all `.txt` files in the `/home/user` directory, you would run:
        
        ```bash
        find /home/user -name "*.txt"
        ```
        
    
32. ### `awk`**Command**
    
    #### **Basic Usage**
    
    * **Description**: Processes and analyzes text files, allowing pattern matching and text manipulation.
        
    * **Usage**: `awk 'pattern {action}' filename`
        
    * **Example**: To print the first field of each line in `file.txt`, you would run:
        
        ```bash
        awk '{print $1}' file.txt
        ```
        
    
    #### **Multiple Fields**
    
    * **Description**: Prints multiple specified fields from each line in a file.
        
    * **Usage**: `awk '{print $1,$2,...}' file.txt`
        
    * **Example**: To print the first and second fields of each line in `file.txt`, you would run:
        
        ```bash
        awk '{print $1, $2}' file.txt
        ```
        
    
33. ### `sed`**Command**
    
    * **Description**: Stream editor for filtering and transforming text.
        
    * **Usage**: `sed [options] 'script' [file]`
        
    * **Example**: To replace all occurrences of "old" with "new" in `file.txt`, you would run:
        
        ```bash
        sed 's/old/new/g' file.txt
        ```
        
    
    #### **Common Options and Examples**
    
    1. **Substitute Text**
        
        * **Usage**: `sed 's/old/new/' file.txt`
            
        * **Example**: Replace the first occurrence of "old" with "new" in each line of `file.txt`.
            
    2. **Global Substitute**
        
        * **Usage**: `sed 's/old/new/g' file.txt`
            
        * **Example**: Replace all occurrences of "old" with "new" in each line of `file.txt`.
            
    3. **In-Place Editing**
        
        * **Usage**: `sed -i 's/old/new/g' file.txt`
            
        * **Example**: Replace all occurrences of "old" with "new" in `file.txt` and save the changes directly to the file.
            
    4. **Delete Lines Matching a Pattern**
        
        * **Usage**: `sed '/pattern/d' file.txt`
            
        * **Example**: Delete all lines containing "pattern" in `file.txt`.
            
    5. **Print Specific Lines**
        
        * **Usage**: `sed -n '2,4p' file.txt`
            
        * **Example**: Print lines 2 to 4 from `file.txt`.
            
    
34. ### `su #username`
    
    * **escription**: Switches the current user to another user account.
        
    * **Usage**: `su [username]`
        
    * **Example**: `su newuser`
        
    
35. **chmod**
    
    * **Description**: Changes file permissions.
        
    * **Usage**: `chmod [options] mode file`
        
    * **Example**: `chmod 755`[`script.sh`](http://script.sh)
        
36. **chown**
    
    * **Description**: Changes file owner and group.
        
    * **Usage**: `chown [options] owner[:group] file`
        
    * **Example**: `chown user:group file.txt`
        
37. **ps**
    
    * **Description**: Displays information about active processes.
        
    * **Usage**: `ps [options]`
        
    * **Example**: `ps aux`
        
38. ### `free`**Command**
    
    * **Description**: Displays the amount of free and used memory in the system.
        
    * **Usage**: `free [options]`
        
    * **Example**: Running `free` without any options will display a summary of the memory usage:
        
        ```bash
                     total        used        free      shared  buff/cache   available
        Mem:        16384000     1234567     2345678      345678     4567890    5678901
        Swap:        8192000      123456     2345678
        ```
        
    

### Git Commands

1. **git init**
    
    * **Description**: Initializes a new Git repository.
        
    * **Usage**: `git init`
        
    * **Example**: `git init my-repo`
        
2. **git clone**
    
    * **Description**: Clones a repository into a new directory.
        
    * **Usage**: `git clone [url]`
        
    * **Example**: `git clone`[`https://github.com/user/repo.git`](https://github.com/user/repo.git)
        
3. **git status**
    
    * **Description**: Shows the working tree status.
        
    * **Usage**: `git status`
        
    * **Example**: `git status`
        
4. **git add**
    
    * **Description**: Adds file contents to the index.
        
    * **Usage**: `git add [file]`
        
    * **Example**: `git add file.txt`
        
5. **git commit**
    
    * **Description**: Records changes to the repository.
        
    * **Usage**: `git commit -m "commit message"`
        
    * **Example**: `git commit -m "Initial commit"`
        
6. **git push**
    
    * **Description**: Updates remote refs along with associated objects.
        
    * **Usage**: `git push [repository] [branch]`
        
    * **Example**: `git push origin main`
        
7. **git pull**
    
    * **Description**: Fetches from and integrates with another repository or a local branch.
        
    * **Usage**: `git pull [repository] [branch]`
        
    * **Example**: `git pull origin main`
        
8. **git branch**
    
    * **Description**: Lists, creates, or deletes branches.
        
    * **Usage**: `git branch [branch-name]`
        
    * **Example**: `git branch feature-branch`
        
9. **git checkout**
    
    * **Description**: Switches branches or restores working tree files.
        
    * **Usage**: `git checkout [branch-name]`
        
    * **Example**: `git checkout main`
        
10. **git merge**
    
    * **Description**: Joins two or more development histories together.
        
    * **Usage**: `git merge [branch-name]`
        
    * **Example**: `git merge feature-branch`
        
11. Local to remote push using ssh key
    
    * **Description**: Add public ssh key in github
        
    * **Usage**: `git push origin main file`
        
    * **Example**: `git push origin main`
        
12. Local to remote pull
    
    * **Description**: Add public ssh key in github
        
    * **Usage**: `git pull origin filename`
        
    * **Example**: `git pull origin #filename`
        
13. ### `git revert`
    
    **Description**: Creates a new commit that undoes the changes made by a specified commit.
    
    **Usage**: `git revert <commit>`
    
    **Example**: To revert the changes made by commit `abc123`, you would run:
    
    ```bash
    git revert abc123
    ```
    
14. ### `git reset`
    
    **Description**: Moves the current branch to a specified commit. It can also modify the index and the working directory depending on the options used.
    
    **Usage**: `git reset [options] <commit>`
    
    **Options**:
    
    * `--soft`: Moves the branch pointer to the specified commit but does not change the index or working directory.
        
    * `--mixed` (default): Moves the branch pointer and resets the index, but not the working directory.
        
    * `--hard`: Moves the branch pointer and resets both the index and working directory.
        
    
    **Example**: To reset the current branch to commit `abc123` and update the working directory and index, you would run:
    
    ```bash
    git reset --hard abc123
    ```
    
15. ### `git rebase`
    
    **Description**: Re-applies commits from the current branch onto another branch. This can be used to integrate changes from one branch into another.
    
    **Usage**: `git rebase [options] <branch>`
    
    **Options**:
    
    * `--interactive` (`-i`): Allows you to edit commits, reorder them, or squash them together.
        
    
    **Example**: To rebase the current branch onto `main`, you would run:
    
    ```bash
    git rebase main
    ```
    
    **Interactive Rebase Example**: To start an interactive rebase for the last 3 commits, you would run:
    
    ```bash
    git rebase -i HEAD~3
    ```
    
16. ### `git cherry-pick`
    
    **Description**: Applies the changes introduced by an existing commit onto the current branch.
    
    **Usage**: `git cherry-pick <commit>`
    
    **Example**: To apply the changes from commit `abc123` to the current branch, you would run:
    
    ```bash
    git cherry-pick abc123
    ```
    
17. ### `git squash`
    
    **Description**: Squashes multiple commits into a single commit. This is typically done during an interactive rebase.
    
    **Usage**: `git rebase -i <commit>`
    
    **Example**: To squash the last 3 commits into a single commit, you would run:
    
    ```bash
    git rebase -i HEAD~3
    ```
    
    In the interactive rebase editor that opens, change the word "pick" to "squash" (or "s") for the commits you want to squash into the previous commit. Save and close the editor to complete the rebase.
    

Thank you for reading!

<mark>© 2024 Anand Raval. All rights reserved.</mark>
---
title: "Day 13 :- Advance Git & GitHub for DevOps Engineers 🛠️"
seoDescription: "Advance Git & GitHub: Learn branching, reverting, resetting, merging, rebasing, fetching, pulling, cherry-picking, squashing, and resolving conflicts"
datePublished: 2024-07-27T13:01:38.471Z
cuid: clz454gfb001409le7bb1e6nt
slug: day-13-advance-git-github-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1722084971183/7ebd1331-f1c7-4f46-b76b-66ad1e9813aa.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1722084994181/5e5d8d2a-01ed-4aa1-9aad-8e280e019b9e.png
tags: github, git, devops, 90daysofdevops, trainwithshubham

---

## Day 13 :- TASK

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721480823333/9cd96dce-52ec-4b04-af0f-b342fcd0a541.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721480851213/31f0c373-b691-4401-b970-718c1bc323b3.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721480878717/8666d60b-6648-426d-aa55-d2f3fc20f51e.png align="center")

## • What is Branching strategy in git

Git branching is a feature in Git that allows you to create separate lines of development within a repository. Each branch can be thought of as an independent version of the project, where you can work on different features, bug fixes, or experiments without affecting the main codebase.

Branches are lightweight and can be created, merged, and deleted easily. The most common branches are:

* **Main (or Master)**: The default branch where the stable code resides.
    
* **Feature Branches**: Used to develop new features. These branches are typically short-lived and merged back into the main branch once the feature is complete.
    
* **Bugfix Branches(Hotfix branch)**: Used to fix bugs. Similar to feature branches, they are merged back into the main branch after the bug is fixed.
    
* **Release Branches**: Used to prepare for a new release. These branches allow for final testing and bug fixing before merging into the main branch and creating a release.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721481606024/5e473bcd-e2f5-4cdf-ab45-27732caeb284.webp align="center")

Branching allows multiple developers to work on different parts of a project simultaneously without interfering with each other's work. Once the work on a branch is complete, it can be merged back into the main branch, integrating the changes.

## • What is Git Revert and Reset

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721481836196/d6ca245b-b57f-425f-887b-0835ce513c8b.png align="center")

Git Revert is a command in Git that allows you to undo changes by creating a new commit that reverses the changes made by a previous commit. Unlike Git Reset, which can alter the commit history, Git Revert is a safe way to undo changes because it does not delete any commits. Instead, it adds a new commit that negates the effects of the specified commit, preserving the integrity of the project history.

This command is particularly useful when you need to undo changes in a shared repository, as it maintains a clear and traceable history of what was changed and why.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721483439698/29c81142-2ec1-46a6-9f8d-c049398fcc0d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721483467780/c60debdf-5239-4186-9868-cb251f24f219.png align="center")

### **Example:**

If you want to revert a commit with the hash `b12371a`, you would use:

```bash
git revert b12371a
```

This will create a new commit that undoes the changes introduced by the commit `abc123`. This approach is particularly useful in a shared repository, as it maintains a clear and traceable history of what was changed and why.

## Reset

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721483800274/b166217b-38bb-49d2-8012-d6529f486deb.png align="center")

Git Reset is a command in Git that allows you to undo changes by moving the current branch to a specified commit. It can modify the commit history and the working directory, depending on the options used. There are three main forms of Git Reset:

1. **\--soft**: Moves the branch pointer to the specified commit but leaves the working directory and the index (staging area) unchanged.
    
2. **\--mixed** (default): Moves the branch pointer to the specified commit and resets the index, but leaves the working directory unchanged.
    
3. **\--hard**: Moves the branch pointer to the specified commit and resets both the index and the working directory to match the specified commit.
    

### Commands:

* **Soft Reset**:
    
    ```bash
    git reset --soft <commit-hash>
    ```
    
* **Mixed Reset** (default):
    
    ```bash
    git reset --mixed <commit-hash>
    ```
    
* **Hard Reset**:
    
    ```bash
    git reset --hard <commit-hash>
    ```
    

### Example:

If you want to reset to a commit with the hash `abc123`:

* **Soft Reset**:
    
    ```bash
    git reset --soft abc123
    ```
    
* **Mixed Reset**:
    
    ```bash
    git reset --mixed abc123
    ```
    
* **Hard Reset**:
    
    ```bash
    git reset --hard abc123
    ```
    

Each type of reset serves different purposes, with `--soft` being the least destructive and `--hard` being the most.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721483875767/bab67835-40bc-47cd-8b0a-4b7b47d3d16e.png align="center")

## • What is Git Rebase and Merge

## Merge :

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721486503559/d4f8935d-ec1c-442d-a1b5-a3b1eaa3b561.png align="center")

Git Merge is a command in Git that allows you to combine the changes from one branch into another. It is commonly used to integrate changes from a feature branch(dev branch )into the main(master) branch. When you perform a merge, Git takes the contents of the source branch and integrates them into the target branch.

### Example:

Suppose you have two branches: `master` and `dev`. You want to merge the changes from the `dev` branch into the `master` branch.

### **Steps and Commands:**

1. **Switch to the target branch (**`master`**in this case)**:
    
    ```bash
    git checkout master
    ```
    
2. **Merge the source branch (**`dev`**) into the target branch**:
    
    ```bash
    git merge dev
    ```
    

### **Example Code:**

Let's say you have the following branches and commits:

* `master` branch:
    
    ```bash
    A---B---C
    ```
    
* `dev` branch:
    
    ```bash
        D---E
    ```
    

To merge `dev` into `master`, you would use the following commands:

1. Switch to the `master` branch:
    
    ```bash
    git checkout master
    ```
    
2. Merge `dev` into `master`:
    
    ```bash
    git merge dev
    ```
    

After the merge, the commit history would look like this:

```bash
A---B---C---F
       \   /
        D---E
```

Here, `F` is the new merge commit that combines the changes from both branches.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721486848637/52a05715-6abe-4a68-bd47-8c3da3444225.png align="center")

## Rebase :

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721487289707/2b9a06f1-6a64-499e-9c0e-68063b98941a.webp align="center")

Git Rebase is a command in Git that allows you to move or combine a sequence of commits to a new base commit. It is often used to keep a feature branch up to date with the main branch or to clean up commit history before merging.

### **Example with**`master` Branch and `dev` Branch

Suppose you have two branches: `master` and `dev`. You want to rebase the `dev` branch onto the `master` branch to incorporate the latest changes from `master` into `dev`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721487487751/83e42507-276b-46d1-aced-7eb05bb8148d.png align="center")

### **Steps and Commands:**

1. **Switch to the source branch (**`dev`**in this case)**:
    
    ```bash
    git checkout dev
    ```
    
2. **Rebase the source branch (**`dev`**) onto the target branch (**`master`):
    
    ```bash
    git rebase master
    ```
    

### **Example Code:**

Let's say you have the following branches and commits:

* `master` branch:
    
    ```bash
    A---B---C
    ```
    
* `dev` branch:
    
    ```bash
        D---E
    ```
    

To rebase `dev` onto `master`, you would use the following commands:

1. Switch to the `dev` branch:
    
    ```bash
    git checkout dev
    ```
    
2. Rebase `dev` onto `master`:
    
    ```bash
    git rebase master
    ```
    

After the rebase, the commit history would look like this:

```bash
A---B---C---D'---E'
```

Here, `D'` and `E'` are the rebased commits from the `dev` branch. The `dev` branch now includes the latest changes from the `master` branch, and the commit history is linear.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721488606014/f764fac8-e340-4e30-8a72-a949cc044cfc.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721488620041/4782948f-5197-4c86-b302-06db4eec9b8f.png align="center")

## • What is difference between git fech and git pull

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721490692159/89f6dabe-889d-479a-9f04-b501f5d85164.png align="center")

### `git fetch`**:**

* **Function**: Downloads commits, files, and references from a remote repository into your local repository.
    
* **Effect**: Updates your local copy of the remote branches but does not merge any changes into your working directory or current branch.
    
* **Usage**: Useful when you want to see what others have been working on without affecting your current work.
    

### **Command:**

```bash
git fetch
```

### `git pull`**:**

* **Function**: Fetches changes from a remote repository and immediately attempts to merge those changes into the current branch.
    
* **Effect**: Combines the actions of `git fetch` and `git merge`. It updates your local copy of the remote branches and merges the changes into your current branch.
    
* **Usage**: Convenient when you want to update your current branch with the latest changes from the remote repository in one step.
    

### **Command:**

```bash
git pull
```

### **Summary:**

* `git fetch`: Downloads changes but does not apply them to your current branch.
    
* `git pull`: Downloads changes and merges them into your current branch.
    

## • What is Cherry pick

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721490822673/2f08918a-f034-4073-b689-3c7e6c073305.png align="center")

Cherry-pick is a command in Git that allows you to apply the changes introduced by an existing commit to another branch. This is useful when you want to incorporate specific changes from one branch into another without merging the entire branch.

### Command:

To cherry-pick a commit, you use the following command:

```bash
git cherry-pick <commit-hash>
```

### Example:

Suppose you have a commit with the hash `abc123` on a feature branch, and you want to apply this commit to the `main` branch.

1. **Switch to the target branch (**`main` in this case):
    
    ```bash
    git checkout main
    ```
    
2. **Cherry-pick the commit**:
    
    ```bash
    git cherry-pick abc123
    ```
    

This will create a new commit on the `main` branch that contains the changes from the commit `abc123`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721501296663/97e16f08-b4c6-4b77-86d8-be64aa36d33f.png align="center")

.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721491413451/9177e595-82cf-4417-932e-3dd658a90196.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721491480496/be087e93-5e29-40ec-b650-233849877559.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721491515806/35f661ca-0062-47c2-bed2-2b60f8f785c1.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721491534770/d86d14f7-55d2-46bc-be1f-1f972d203f3c.png align="center")

## Squash

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721501301205/2ec10294-f193-4c6b-bf8a-39faba826005.png align="center")

Squash in Git is a technique used to combine multiple commits into a single commit. This is useful for cleaning up a commit history before merging a feature branch into the main branch. Here's a beginner-friendly explanation with an example involving `master` and `dev` branches:

### What is Squash?

Imagine you are working on a project and you have a `master` branch, which is the main version of your project, and a `dev` branch, where you are developing a new feature. Over time, you make several commits on the `dev` branch to save your progress. Each commit represents a small change or improvement.

Before you merge the `dev` branch back into the `master` branch, you might want to combine all those small commits into a single, clean commit. This process is called "squashing."

### Example:

1. **Current Situation:**
    
    * `master` branch:
        
        * Commit A
            
    * `dev` branch:
        
        * Commit A (from master)
            
        * Commit B (small change)
            
        * Commit C (another small change)
            
        * Commit D (yet another small change)
            
2. **Goal:**
    
    * Combine commits B, C, and D into a single commit on the `dev` branch before merging it into `master`.
        

### Steps to Squash Commits:

1. **Switch to the**`dev` branch:
    
    ```bash
    git checkout dev
    ```
    
2. **Start an interactive rebase:**
    
    ```bash
    git rebase -i master
    ```
    
3. **Interactive Rebase:**
    
    * An editor will open showing a list of commits. It will look something like this:
        
        ```bash
        pick b123456 Commit B
        pick c123456 Commit C
        pick d123456 Commit D
        ```
        
    * Change the word `pick` to `squash` (or `s`) for commits C and D:
        
        ```bash
        pick b123456 Commit B
        squash c123456 Commit C
        squash d123456 Commit D
        ```
        
4. **Save and Close the Editor:**
    
    * After saving and closing the editor, Git will combine commits B, C, and D into a single commit. You will be prompted to edit the commit message for the new squashed commit.
        
5. **Finalize the Commit Message:**
    
    * Edit the commit message to describe the combined changes, then save and close the editor.
        
6. **Merge**`dev` into `master`:
    
    ```bash
    git checkout master
    git merge dev
    ```
    

### Result:

* `master` branch:
    
    * Commit A
        
    * Commit E (squashed commit from `dev`)
        
* `dev` branch:
    
    * Commit A (from master)
        
    * Commit E (squashed commit)
        

By squashing commits, you keep the commit history clean and easy to understand, which is especially helpful when collaborating with others.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721501899346/a23d0689-be90-44b7-8223-a9fe30af36e4.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721914115710/4afc50fa-60b7-474c-bfa5-2a0998ef556f.png align="center")

## Merge conflict

A merge conflict in Git happens when two branches have changes in the same part of a file, and Git doesn't know which change to keep. Here's a beginner-friendly explanation using a simple example with `master` and `dev` branches:

### Imagine This Scenario:

1. **You have a**`master` branch: This is the main version of your project.
    
2. **You create a**`dev` branch: This is where you work on a new feature.
    

### Changes in Both Branches:

* **On the**`master` branch, you change a line in a file to say: "Hello, World!"
    
* **On the**`dev` branch, you change the same line in the same file to say: "Hi, Universe!"
    

### Merging `dev` into `master`:

When you try to merge the `dev` branch back into the `master` branch, Git sees that the same line has been changed in both branches. It doesn't know whether to keep "Hello, World!" or "Hi, Universe!" This is a merge conflict.

### How to Resolve It:

1. **Git will alert you**: It will show a message saying there's a conflict in the file.
    
2. **Open the file**: You'll see something like this:
    

```bash
<<<<<<< HEAD
Hello, World!
=======
Hi, Universe!
>>>>>>> dev
```

3. **Choose the correct version**: You decide which line to keep or combine them in a way that makes sense. For example, you might change it to:
    

```bash
Hello, World and Universe!
```

4. **Save the file**: After resolving the conflict, save the file.
    
5. **Tell Git the conflict is resolved**: Use the command `git add <file>` to mark the conflict as resolved.
    
6. **Complete the merge**: Finally, commit the changes with `git commit`.
    

A merge conflict happens when changes in two branches overlap. You resolve it by choosing which changes to keep and then telling Git the conflict is resolved. This ensures that your project has the correct and intended changes.

In dev branch:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721936210800/0372f8a4-4991-4512-8f72-b9f999d86f07.png align="center")

In master branch:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721936305304/208d5a7e-52b8-4afc-84dd-e43fcb7d4b06.png align="center")

Now git merge dev

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721936355842/e271ce4f-7e92-4b85-bca7-cfe64c4faa37.png align="center")

committed

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721936372084/4889cae9-e284-4ca5-a066-3055bf039467.png align="center")

Now open conflict file

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721936444543/bbcb776a-53c9-4ec9-b24d-d0084d29a876.png align="center")

Edit conflict file

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721936507716/9ace3d0d-fe30-4712-bbb6-47930a708244.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721936558712/1a4ff12e-39ab-4e0e-99f5-482d6161ca66.png align="center")

Thank you for reading!

<mark>© 2024 Anand Raval. All rights reserved.</mark>
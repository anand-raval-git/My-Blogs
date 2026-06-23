---
title: "Day 01: Kodekloud Engineer"
slug: day-01-kodekloud-engineer

---

### 📝 Task

Create a user named **ravi** on **App Server 2** so that this user cannot log in (non-interactive user, only for tools/agents).

---

### ✅ Solution

1. Login to App Server 2:
    
    ```python
    ssh steve@stapp02.stratos.xfusioncorp.com
    ```
    
    Password: `Am3ric@`
    
2. Run this command to create the user:
    
    ```python
    sudo useradd -s /sbin/nologin ravi
    ```
    
3. Check the user details:
    
    ```python
    grep ravi /etc/passwd
    ```
    
    You will see `/sbin/nologin` → means ravi cannot log in.
    

---

👉 In simple words:  
We created a **dummy user (ravi)** that exists for the backup tool, but **cannot log in like normal users**.
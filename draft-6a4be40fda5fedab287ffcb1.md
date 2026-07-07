---
title: "AWS Day 35: Deploying and Managing Applications on AWS"

---

The Nautilus DevOps team needs a new private RDS instance for their application. They need to set up a MySQL database and ensure that their existing EC2 instance can connect to it. This will help in managing their database needs efficiently and securely.

1.  **Task Details:**
    

1.  Create a private RDS instance named `datacenter-rds` using a `sandbox` template.
    
2.  The engine type must be `MySQL v8.4.5`, and it must be a `db.t3.micro` type instance.
    
3.  The master username must be `datacenter_admin` with an appropriate password.
    
4.  The RDS storage type must be `gp2`, and the storage size must be `5GiB`.
    
5.  Create a database named `datacenter_db`.
    
6.  Keep the rest of the configurations as `default`. Ensure the instance is in `available` state.
    
7.  Adjust the security groups so that the `datacenter-ec2` instance can connect to the RDS on `port 3306` and also open port `80` for the instance.
    

2.  An EC2 instance named `datacenter-ec2` exists. Connect to this instance from the AWS console. Create an SSH key (`/root/.ssh/id_rsa`) on the `aws-client` host if it doesn't already exist. Add the public key to the authorized keys of the `root` user on the EC2 instance for password-less SSH access.
    
3.  There is a file named `index.php` under the `/root` directory on the `aws-client` host. Copy this file to the `datacenter-ec2` instance under the `/var/www/html/` directory. Make the appropriate changes in the file to connect to the RDS.
    
4.  You should see a `Connected successfully` message in the browser once you access the instance using the public IP.
    

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/de46e407-636a-41b5-9a8e-71961c51c730.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/85aaa730-cd12-4afe-811e-b28d1e5b98c4.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/d75f100b-4db6-4bb4-b118-891958aa3c85.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/996b857e-b755-4638-b50e-0d38e2288310.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/e497c76a-e1cc-4668-9a08-6c48f0a22a6b.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/7ffc9748-1b1b-4e8d-a8b5-8257271fcb21.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/9d8b2708-3981-4738-b8a8-1e860648f5d9.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/07489781-fd25-4a3b-be2c-a5bde05a24d9.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/6272954b-4f06-4e73-827e-49885c6f7b89.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/468e7184-b985-4a8f-9c6e-4c27c7998698.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/40f2f638-ab31-46c4-82d0-de96b2ea2864.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/ec6944ea-459c-4e03-b881-e74c3c530a9a.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/9b621a55-5527-4603-b46a-02d005cf3bb3.png align="center")
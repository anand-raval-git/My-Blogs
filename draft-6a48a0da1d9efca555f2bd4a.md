---
title: "AWS Day 31: Configuring a Private RDS Instance for Application Development
"

---

The Nautilus Development Team is working on a new application feature that requires a reliable and scalable database solution. To facilitate development and testing, they need a new private RDS instance. This instance will be used to store critical application data and must be provisioned using the AWS free tier to minimize costs during the initial development phase. The team has chosen MySQL as the database engine due to its compatibility with their existing systems. The DevOps team has been tasked with setting up this RDS instance, ensuring that it is correctly configured and available for use by the development team.

As a member of the Nautilus DevOps Team, your task is to perform the following:

1.  **Provision a Private RDS Instance:** Create a new private RDS instance named `datacenter-rds` using the `Full configuration` database creation method, and select the `Free tier` template. Further, it must be a `db.t3.micro` type instance.
    
2.  **Engine Configuration:** Use the `MySQL` engine with version `8.4.x`.
    
3.  **Enable Storage Autoscaling:** Enable storage autoscaling and set the threshold value to `50GB`. Keep the rest of the configurations as default.
    
4.  **Instance Availability:** Ensure the instance is in the `available` state before submitting this task.
    

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/a563083a-896f-43b9-bba6-cc279aee4e95.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/02ab5e0a-9d7e-40a0-9ad6-237d0d27cfd3.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/3ac000fe-8c7e-4a26-a6d8-3a81e5cef016.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/b86e6360-7151-424f-a1f9-63542158845b.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/70c3a0cc-7fb8-407f-a484-08ca06c6d1c3.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/afd7bab7-573d-4a47-99bc-8a0e371d1ec5.png align="center")
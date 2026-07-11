---
title: "AWS Day 40: Troubleshooting Internet Accessibility for an EC2-Hosted Application"

---

The Nautilus Development Team recently deployed a new web application hosted on an EC2 instance within a public VPC named `nautilus-vpc`. The application, running on an Nginx server, should be accessible from the internet on port 80. Despite configuring the security group `nautilus-sg` to allow traffic on port 80 and verifying the EC2 instance settings, the application remains inaccessible from the internet. The team suspects that the issue might be related to the VPC configuration, as all other components appear to be set up correctly. The DevOps team has been asked to troubleshoot and resolve the issue to ensure the application is accessible to external users.

As a member of the Nautilus DevOps Team, your task is to perform the following:

1.  **Verify VPC Configuration:** Ensure that the VPC `nautilus-vpc` is properly configured to allow internet access.
    
2.  **Ensure Accessibility:** Make sure the EC2 instance `nautilus-ec2` running the Nginx server is accessible from the internet on port 80.
    

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/b02f5b1c-c1c4-4fe7-b09e-8c0b60c39252.png align="center")

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/b7f30b42-982a-4c58-875e-14c5c00def04.png align="center")
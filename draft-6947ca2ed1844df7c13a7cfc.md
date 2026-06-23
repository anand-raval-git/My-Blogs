---
title: "kodekloud azure day 02"
slug: kodekloud-azure-day-02

---

The Nautilus DevOps team is planning to migrate a portion of their infrastructure to the Azure cloud incrementally. As part of this migration, you are tasked with creating an Azure Virtual Machine (VM).

The requirements are:

1) Use the existing resource group.

2) The VM name must be `nautilus-vm`, it should be in `West US` region.

3) Use the `Ubuntu 22.04 LTS` image for the VM.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1766312672740/0d7e731b-59c8-4fa2-8187-ef1f2b062a5a.png align="center")

4) The VM size must be `Standard_B1s`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1766312745448/24cc991f-5289-49a5-af61-6f925ac4f3a4.png align="center")

5) Attach a default Network Security Group (NSG) that allows inbound SSH (port 22).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1766312809930/7b488a83-dd14-4b39-bb70-71e108dd324f.png align="center")

6) Attach a 30 GB storage disk of type `Standard HDD`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1766312856240/b0a0c123-6966-4b75-b03b-13ae6044c55b.png align="center")

7) The rest of the configurations should remain as default.

After completing these steps, make sure you can SSH into the virtual machine.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1766313217294/5fe13f87-6aba-47fa-9dc0-524ffe9958cf.png align="center")
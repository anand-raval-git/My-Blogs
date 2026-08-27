---
title: "Day 50: Expanding EC2 Instance Storage for Development Needs"
seoTitle: "Day 50: Expand EC2 EBS Volume from 8 GiB to 12 GiB "
seoDescription: "Learn how to expand an AWS EC2 EBS root volume from 8 GiB to 12 GiB using AWS Console, growpart, and xfs_growfs with step-by-step Linux verification."
datePublished: 2026-08-27T03:43:25.051Z
cuid: cmtaz9u1t00000ajgegzm26jz
slug: day-50-expanding-ec2-instance-storage-for-development-needs
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/72132331-7b1a-4b07-8fc9-245f0ab35d47.png
tags: ec2, aws, ebs, kodekloud, anand-raval

---

Running out of disk space on an EC2 instance is a common problem in development and production environments. As applications, logs, packages, Docker images, and other data grow, the underlying storage may need to be expanded without replacing the EC2 instance.

As part of **100 Days of Cloud (AWS)** on KodeKloud, Day 50 focuses on expanding the storage of an existing EC2 instance.

In this lab, the `devops-ec2` instance had an **8 GiB EBS root volume**, and the requirement was to increase it to **12 GiB** while making the additional storage immediately available to the root filesystem.

## Step 1: Identify the EC2 Instance

First, locate the `devops-ec2` instance from the AWS EC2 console.

Navigate to:

```plaintext
AWS Console
   ↓
EC2
   ↓
Instances
   ↓
devops-ec2
```

Open the instance details and check the **Storage** section.

The root device was attached to an EBS volume with an initial size of:

```plaintext
8 GiB
```

The root device inside the Linux instance was:

```plaintext
/dev/xvda
```

with the root partition:

```plaintext
/dev/xvda1
```

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/8f30286f-31fc-4a1e-89e1-4cce52861f59.png align="center")

## Step 2: Modify the EBS Volume

Navigate to:

```plaintext
EC2
   ↓
Volumes
```

Locate the **8 GiB EBS volume attached to** `devops-ec2`.

Select the volume and choose:

```plaintext
Actions → Modify volume
```

Change the size from:

```plaintext
8 GiB
```

to:

```plaintext
12 GiB
```

Then select **Modify**.

The important point here is that we are **modifying the existing root volume**, not creating a new EBS volume.

After the modification, AWS increases the underlying EBS block device.

However, the operating system may still report the original partition size.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/db172938-d77a-4c7b-a827-64339c71e9e6.png align="center")

## Step 3: SSH Into the EC2 Instance

The task provides the SSH key on the `aws-client` host:

```plaintext
/root/devops-keypair.pem
```

First, make sure the private key has the correct permissions:

```plaintext
chmod 400 /root/devops-keypair.pem
```

Then connect to the EC2 instance:

```plaintext
ssh -i /root/devops-keypair.pem ec2-user@<EC2-PUBLIC-IP>
```

Once connected, verify that you are working on the correct instance.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/3ce151bd-9160-48c0-b400-b52e9dbf6e47.png align="center")

## Step 4: Check the Existing Disk and Partition

Before changing anything inside Linux, check the block devices:

```plaintext
lsblk
```

Initially, the output showed an 8 GiB root disk similar to:

```plaintext
NAME        SIZE TYPE MOUNTPOINTS
xvda          8G disk
├─xvda1       8G part /
├─xvda127     1M part
└─xvda128    10M part /boot/efi
```

This is important because it establishes the original state.

The structure is:

```plaintext
/dev/xvda       → EBS disk
/dev/xvda1      → root partition
/               → root filesystem
```

After modifying the EBS volume, the underlying disk becomes **12 GiB**, but the partition can still remain **8 GiB**.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/f92c1543-fbf8-4bdf-b1a3-e0926bba6376.png align="center")

## Step 5: Verify the Filesystem Type

Before expanding the filesystem, determine which filesystem is being used.

For example:

```plaintext
df -Th
```

In this environment, the root filesystem was **XFS**.

The root filesystem was mounted at:

```plaintext
/
```

This matters because different filesystems use different expansion commands.

For XFS, we use:

```plaintext
xfs_growfs
```

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/ca9b2d4d-a61d-4927-955b-ca0284f4929c.png align="center")

## Step 6: Verify the Final Storage Size

Now verify the root filesystem:

```plaintext
df -h /
```

The final output showed:

```plaintext
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda1       12G  1.6G   11G  13% /
```

The most important value is:

```plaintext
/dev/xvda1       12G
```

This confirms that the root filesystem is now using the expanded **12 GiB** capacity.

You can also run:

```plaintext
lsblk
```

to confirm the disk and partition sizes.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/522e1b64-e5b4-40ba-ae64-801172617620.png align="center")

## Conclusion

Day 50 of the **100 Days of Cloud (AWS)** challenge demonstrated a practical storage-management scenario that frequently occurs in real DevOps environments.

The `devops-ec2` instance originally had an **8 GiB root EBS volume**. I expanded the existing EBS volume to **12 GiB**, expanded the root partition using `growpart`, and then expanded the XFS filesystem using `xfs_growfs`.

The final verification confirmed:

```plaintext
/dev/xvda1 → 12 GiB → /
```

This lab reinforced an important operational principle: **expanding cloud storage is a multi-layer process**. The cloud provider's block device, the operating-system partition, and the filesystem must all be considered when increasing available disk capacity.
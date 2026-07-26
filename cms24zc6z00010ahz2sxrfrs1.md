---
title: "AWS Day 39: Hosting a Static Website on AWS S3"
seoTitle: "AWS Day 39: Hosting a Static Website on AWS S3"
seoDescription: "Learn how to host a static website on Amazon S3 by creating a bucket, enabling static website hosting, configuring public access, and uploading HTML."
datePublished: 2026-07-26T18:33:35.109Z
cuid: cms24zc6z00010ahz2sxrfrs1
slug: aws-day-39-hosting-a-static-website-on-aws-s3
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/15c210f7-429e-477e-a43c-e908c946a20e.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/6ec16996-dbcf-4719-bfd1-8ecc78a7de55.png
tags: aws, s3, kodekloud, s3-static-website-hosting

---

Static websites are one of the simplest and most cost-effective ways to host web content in the cloud. Instead of managing virtual machines or web servers, Amazon S3 allows you to store HTML, CSS, JavaScript, images, and other static assets while serving them directly to users.

This approach is ideal for personal portfolios, documentation sites, landing pages, and internal information portals because it requires minimal infrastructure management and offers high availability.

In this hands-on lab, I created an Amazon S3 bucket, enabled static website hosting, uploaded an HTML page, configured public access, and successfully accessed the website using the Amazon S3 website endpoint.

## Step 1 – Create an Amazon S3 Bucket

Created a new S3 bucket named:

```plaintext
nautilus-web-1451225450
```

The bucket was created in the **US East (N. Virginia)** Region using the default General Purpose bucket type.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/fb9fbb81-ac66-4c72-b073-71d6d74a9446.png align="center")

## Step 2 – Upload Website Files

Uploaded the **index.html** file from the AWS client to the S3 bucket using the AWS CLI.

```plaintext
aws s3 cp index.html s3://nautilus-web-1451225450/
```

This uploaded the main web page that will be served as the website's home page.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/672b4756-05c8-4b4b-86a2-fe696888ef58.png align="center")

## Step 3 – Configure Public Access

By default, Amazon S3 blocks all public access to protect stored objects.

To make the website publicly accessible:

*   Disabled **Block Public Access**
    
*   Saved the updated bucket settings
    

This allows external users to access the website through the S3 website endpoint.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/6b234991-98e4-4974-9376-4b6932851ad6.png align="center")

## Step 4 – Enable Static Website Hosting

Enabled **Static Website Hosting** for the bucket.

Configured:

*   Hosting Type: **Host a Static Website**
    
*   Index Document:
    

```plaintext
index.html
```

Amazon S3 automatically generated a website endpoint for serving the static website.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/f8080a53-608c-46fc-9502-1557669f98fc.png align="center")

## Step 5 – Configure Bucket Permissions

Since static websites must be publicly accessible, the bucket requires permissions that allow users to read website files.

A bucket policy was applied to allow public **GetObject** access for all objects inside the bucket.

Example policy:

```plaintext
{
  "Version":"2012-10-17",
  "Statement":[
    {
      "Sid":"PublicRead",
      "Effect":"Allow",
      "Principal":"*",
      "Action":"s3:GetObject",
      "Resource":"arn:aws:s3:::nautilus-web-1451225450/*"
    }
  ]
}
```

> **Note:** Public bucket policies should only be used for websites intended for public access.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/c6957eeb-a14d-4d62-a586-54f969fb071c.png align="center")

## Step 6 – Verify Website

After enabling static website hosting and configuring permissions, the generated S3 website endpoint displayed the uploaded web page successfully.

The homepage loaded correctly using:

```plaintext
http://bucket-name.s3-website-region.amazonaws.com
```

## Conclusion

Amazon S3 Static Website Hosting provides a simple, scalable, and cost-effective solution for hosting static websites without managing servers. By creating an S3 bucket, uploading website files, configuring public access, and enabling static website hosting, you can publish web content in just a few steps.

For production workloads, combining Amazon S3 with Amazon CloudFront and AWS Certificate Manager (ACM) enables HTTPS, global content delivery, and improved security, making it a powerful solution for modern static web applications.
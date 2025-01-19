# Launch a Website on Amazon S3 and Route 53

This project demonstrates how to host a static website on Amazon S3 and map a custom domain using Amazon Route 53. The following steps guide you through the process of creating an S3 bucket, uploading your website files, and setting up DNS routing to point to the S3 bucket.

## Table of Contents

- [Overview](#overview)
- [AWS Services Used](#aws-services-used)
- [Setting Up the Website](#setting-up-the-website)
  - [Create an S3 Bucket](#create-an-s3-bucket)
  - [Upload Website Files](#upload-website-files)
  - [Enable Static Website Hosting](#enable-static-website-hosting)
  - [Update Bucket Policy](#update-bucket-policy)
- [Set Up Domain in Route 53](#set-up-domain-in-route-53)
  - [Create a Record in Route 53](#create-a-record-in-route-53)
  - [Check Domain](#check-domain)
- [Conclusion](#conclusion)

---

## Overview

In this project, we’ll set up a static website on Amazon S3, using Amazon Route 53 to map a custom domain to the S3 bucket. The following instructions will guide you step-by-step on how to:

- Create and configure an S3 bucket for static website hosting.
- Upload an `index.html` file for your website.
- Update the S3 bucket policy to allow public access.
- Set up Route 53 DNS records to map your custom domain to your S3 bucket.

---

## AWS Services Used

- **Amazon S3**: To store and serve static website files.
- **Amazon Route 53**: For domain registration and DNS management.
- **IAM (Identity and Access Management)**: For managing access permissions to the S3 bucket.

---

## Setting Up the Website

### Create an S3 Bucket

1. Log in to your **AWS Management Console**.
2. Navigate to **S3** and create a new bucket.
3. Use your custom domain name as the **bucket name** (e.g., `martinsobike.com`).
4. Choose your desired AWS region for the bucket.
5. Leave other options as default and click **Create Bucket**.

### Upload Website Files

1. After the bucket is created, click on the bucket name to open it.
2. Click the **Upload** button and upload your `index.html` file (and any other necessary files like CSS, JS, etc.).
3. Once the files are uploaded, ensure the S3 bucket has the correct permission to allow public access to the static website.

### Enable Static Website Hosting

1. Inside the S3 bucket, go to the **Properties** tab.
2. Scroll to the **Static website hosting** section and click **Edit**.
3. Enable **Static website hosting** and set the **Index document** to `index.html` (or your preferred file).
4. Click **Save changes**.

### Update Bucket Policy

To make sure that users can access the website, you need to add a bucket policy:

1. Go to the **Permissions** tab of the bucket.
2. Click on **Bucket Policy** and add the following policy (replace `your-bucket-name` with the actual bucket name, e.g., `martinsobike.com`):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::martinsobike.com/*"
    }
  ]
}

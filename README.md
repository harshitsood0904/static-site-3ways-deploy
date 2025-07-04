# 🌐 Deploying a Static Website on AWS using S3

This project demonstrates how to host and deploy a fully functional **static website** on **Amazon Web Services (AWS)** using the **S3 (Simple Storage Service)**. No backend server is involved; it's entirely front-end and cloud-based.

---

## 🧠 Prerequisites

Before you begin, ensure the following:

- ✅ Basic knowledge of AWS S3 and static website hosting
- ✅ AWS Account ([Sign Up Here](https://aws.amazon.com/))
- ✅ A simple HTML/CSS website ready to deploy
- ✅ AWS CLI (Optional, for command-line setup)

---

## 🛠️ Tools & Services Used

- **AWS S3** – To store and serve the website files
- **AWS Management Console** – To configure the S3 bucket
- **(Optional)** AWS CLI – For faster command-line operations
- **Any Code Editor** – (e.g., VS Code) to manage local website files

---

## 📁 Project Folder Structure

Your local project should look like this:
my-static-site/
├── index.html
├── styles.css
├── about.html
└── images/
└── logo.png
---

## 🚀 Step-by-Step Deployment Guide

### 1️⃣ Create an S3 Bucket

1. Go to the AWS Management Console.
2. Navigate to **S3** service.
3. Click on **"Create Bucket"**.
4. Set a globally unique bucket name (e.g., `my-static-site-bucket`).
5. Choose the appropriate region (e.g., `us-east-1`).
6. **Uncheck** “Block all public access” under **Object Ownership** → Permissions.
7. Click **Create Bucket**.
8. ![Create S3 Bucket](https://github.com/harshitsood0904/static-website-deploy-S3/blob/main/Images/Bucket.png)

---

### 2️⃣ Enable Static Website Hosting

1. Open your newly created bucket.
2. Go to the **Properties** tab.
3. Scroll down to **Static website hosting**.
4. Click **Edit**.
5. Enable it and set:
   - **Index document**: `index.html`
   - **Error document**: `error.html` (optional)
6. Save the changes.
7. ![Static Website Hosting](https://github.com/harshitsood0904/static-website-deploy-S3/blob/main/Images/Editing%20Static%20Website%20hosting.png)
---

### 3️⃣ Upload Website Files

1. Go to the **Objects** tab in the bucket.
2. Click **Upload** → **Add Files** or **Add Folder**.
3. Upload all files including `index.html`, `styles.css`, and image folders.
4. After upload, select all files → **Actions** → **Make public**.

   *(Note: If using S3 Object Ownership, you might need to modify bucket policies instead. See step 4.)*

---

### 4️⃣ (Optional) Set Bucket Policy for Public Access

If some files aren’t accessible publicly, add a **bucket policy**:

1. Go to **Permissions** → **Bucket Policy**.
2. Paste the following JSON (replace `"my-static-site-bucket"` with your bucket name):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-static-site-bucket/*"
    }
  ]
}
```
3.Click Save.
![Bucket Policy](https://github.com/harshitsood0904/static-website-deploy-S3/blob/main/Images/bucket%20policy.png)

### 5️⃣ CI/CD Pipeline (AWS CodePipeline)
Go to the AWS Console → CodePipeline service.
Create a new pipeline and connect it to your GitHub repository using the GitHub App.
Set the Deploy provider as Amazon S3, and choose your static website bucket.
Every time you push code to the connected branch, the pipeline will:
Automatically pull source code from GitHub.
Deploy the updated files to your S3 bucket.
✅ Your pipeline automates static website updates — no manual uploads needed!
![AWS CodePipeline Working](https://github.com/harshitsood0904/static-website-deploy-S3/blob/main/Images/Pipeline.png)

### 6️⃣ Access Your Static Website
Go to the Properties tab → Static website hosting section.
Click the Endpoint URL provided.
Your static site should now be live 🎉

Example:
"http://my-static-site-bucket.s3-website-us-east-1.amazonaws.com"
### 7️⃣ Live Website with Automated Update
1. Visit your hosted website using the S3 Static Website Hosting Endpoint.
2. Here’s a screenshot of the initial hosted website:
![Initial Website](https://github.com/harshitsood0904/static-website-deploy-S3/blob/main/Images/Wesbite%20Hosted.png)
3. Next, go to your GitHub repository and make a code change — for example, update text in index.html:
<!-- <h1>Welcome to My Cloud-Powered Website 🚀</h1> -->
<!-- Updated from "Hello World!" -->
4. Commit and push the changes:
<!-- git add index.html
git commit -m "Updated website header"
git push origin main -->
5. AWS CodePipeline detects the change and redeploys the updated file to S3 automatically ✅.
6. After a few seconds, refresh the website — the new changes are now live �
### 📸 Supporting Screenshots
1. Initial Website View
![Initial Website](https://github.com/harshitsood0904/static-website-deploy-S3/blob/main/Images/Wesbite%20Hosted.png)
2. Code Change on GitHub
![GitHub Code Change](https://github.com/harshitsood0904/static-website-deploy-S3/blob/main/Images/Github%20update.png)
3. Updated Live Website
![Updated Website](https://github.com/harshitsood0904/static-website-deploy-S3/blob/main/Images/Changed%20Website.png)

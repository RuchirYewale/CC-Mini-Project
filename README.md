# Cloud Portfolio & Documentation Site

A sleek, modern, self-contained personal developer portfolio site built with responsive HTML5, CSS3, and Vanilla JavaScript (zero external dependencies). Designed to be hosted on **AWS S3 with Amazon CloudFront CDN** (for your Mini Project No. 2) or deployed in under 2 minutes on **Render**.

Live Reference Style: [https://deokju33tvu1l.cloudfront.net](https://deokju33tvu1l.cloudfront.net)

---

## 📋 Mini Project Requirements Covered

| Step | Requirement | Implementation |
|---|---|---|
| **1** | Create a simple portfolio/documentation website | Included (`index.html`) with Hero, About, Skills, Projects, Credentials, Contact, and Code window. |
| **2** | Create an Amazon S3 bucket | Documented below with bucket policy template (`s3-bucket-policy.json`). |
| **3** | Upload your website files to S3 | Upload `index.html` to root of bucket. |
| **4** | Make website accessible from the internet | Enable "Static website hosting" + Bucket Policy. |
| **5** | Create AWS CloudFront distribution | Connect S3 endpoint as Origin. |
| **6** | Enable HTTPS through CloudFront | CloudFront default SSL certificate (`*.cloudfront.net`). |
| **7** | Open CloudFront URL and verify | Test global latency and HTTPS padlock. |

---

## 🚀 Quick Customization

Open `index.html` in your browser:
1. Click the **"Customize My Info"** button in the top banner.
2. Enter your Name, Branch/Degree, Email, GitHub, and LinkedIn.
3. Click **"Save & Update Site"** (updates in real time and remembers across refreshes).
4. Click **"Download Single index.html"** to get your fully personalized file ready for deployment!

*Or edit lines directly in `index.html` with your code editor.*

---

## 🌐 Deployment Option 1: Deploy on Render (Takes 2 Minutes)

Render provides free, fast static site hosting with automated SSL/HTTPS and global CDN.

### Steps:
1. Push this project folder to a GitHub repository:
   ```bash
   git init
   git add .
   git commit -m "Initial commit of cloud portfolio"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/cloud-portfolio.git
   git push -u origin main
   ```
2. Go to [https://dashboard.render.com/](https://dashboard.render.com/) and sign in with GitHub.
3. Click **"New +"** and choose **"Static Site"**.
4. Select your `cloud-portfolio` repository.
5. Fill in the details:
   - **Name**: `yourname-portfolio`
   - **Branch**: `main`
   - **Build Command**: *(leave blank)*
   - **Publish Directory**: `.` *(or `./`)*
6. Click **"Create Static Site"**.
7. Render will build and provide a live URL like `https://yourname-portfolio.onrender.com` with HTTPS enabled!

---

## ☁️ Deployment Option 2: Deploy on AWS S3 + CloudFront (Mini Project Rubric)

Follow these exact steps to complete Mini Project No. 2:

### Step 1: Create an S3 Bucket
1. Log in to [AWS Management Console](https://console.aws.amazon.com/) and open the **S3** service.
2. Click **Create bucket**.
3. Choose a globally unique bucket name (e.g. `yourname-portfolio-2026`).
4. Select your preferred AWS Region (e.g. `ap-south-1` Mumbai or `us-east-1` N. Virginia).
5. Under **Block Public Access settings for this bucket**:
   - Uncheck **Block *all* public access**.
   - Check the acknowledgement box *"I understand that the bucket and objects will become public"*.
6. Click **Create bucket**.

### Step 2: Upload Files
1. Open your newly created bucket.
2. Click **Upload** -> **Add files** -> Select `index.html`.
3. Click **Upload**.

### Step 3: Enable Static Website Hosting
1. In your bucket, go to the **Properties** tab.
2. Scroll to the bottom to **Static website hosting** and click **Edit**.
3. Choose **Enable**.
4. In **Index document**, type `index.html`.
5. Click **Save changes**.
6. Copy the **Bucket website endpoint** (e.g., `http://yourname-portfolio-2026.s3-website.ap-south-1.amazonaws.com`).

### Step 4: Add Bucket Policy (Make Objects Public)
1. In your bucket, go to the **Permissions** tab.
2. Scroll to **Bucket policy** and click **Edit**.
3. Paste the following JSON (replace `yourname-portfolio-2026` with your bucket name):
   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Sid": "PublicReadGetObject",
         "Effect": "Allow",
         "Principal": "*",
         "Action": "s3:GetObject",
         "Resource": "arn:aws:s3:::yourname-portfolio-2026/*"
       }
     ]
   }
   ```
4. Click **Save changes**. Test your S3 website endpoint in a browser!

### Step 5 & 6: Create CloudFront Distribution & Enable HTTPS
1. Go to the **CloudFront** service in the AWS Console.
2. Click **Create distribution**.
3. Under **Origin domain**:
   - Paste the **S3 static website endpoint** hostname (from Step 3, without `http://`).
   *(Tip: Using the website endpoint preserves clean URL handling)*.
4. Under **Default cache behavior**:
   - **Viewer protocol policy**: Select **Redirect HTTP to HTTPS**.
   - **Allowed HTTP methods**: Select `GET, HEAD`.
5. Under **Settings**:
   - **Default root object**: Type `index.html`.
6. Click **Create distribution**.
7. Wait 2–5 minutes until the status becomes **Enabled** / **Deployed**.

### Step 7: Verify the CloudFront HTTPS Site
1. Copy the **Distribution domain name** (e.g. `https://dXXXXXXXXXXXXX.cloudfront.net`).
2. Open it in your browser.
3. Verify that the site loads securely over HTTPS with a green padlock, identical to `https://deokju33tvu1l.cloudfront.net`!

---

## 🎓 Mini Project Viva Questions & Answers

1. **What is Amazon S3?**
   - Simple Storage Service (S3) is an object storage service designed to store and retrieve data with 99.999999999% (11 9's) durability. It provides built-in static website hosting.

2. **Why do we use CloudFront with S3?**
   - S3 static website hosting alone only supports HTTP (no custom HTTPS without CloudFront).
   - CloudFront acts as a Content Delivery Network (CDN) with edge locations worldwide, caching assets close to the end user to drastically reduce latency and protect S3 from high traffic costs.

3. **What is an Edge Location?**
   - A physical site running CloudFront CDN servers that caches copies of content geographically closer to users.

4. **How does CloudFront provide HTTPS?**
   - CloudFront terminates the SSL/TLS connection at the edge server closest to the viewer using default AWS certificates (`*.cloudfront.net`) or custom domain certificates from AWS Certificate Manager (ACM).

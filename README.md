# Cloud Portfolio & Documentation Site — Ruchir Yewale

A sleek, modern, self-contained personal developer portfolio site built with responsive HTML5, CSS3, and Vanilla JavaScript (zero external dependencies). Designed to be hosted on **AWS S3 with Amazon CloudFront CDN** (for Mini Project No. 2) or deployed in under 2 minutes on **Render**.

- **Student Name**: Ruchir Yewale
- **Degree**: Computer Engineering Student
- **Email**: ruchiryewale2@gmail.com
- **LinkedIn**: [https://www.linkedin.com/in/ruchir-yewale-53ab56143/](https://www.linkedin.com/in/ruchir-yewale-53ab56143/)
- **Live Reference Style**: [https://deokju33tvu1l.cloudfront.net](https://deokju33tvu1l.cloudfront.net)

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

## 🚀 Quick Preview & Customization

Open `index.html` in your browser:
- You will see **Ruchir Yewale**'s portfolio loaded with your exact contact details and LinkedIn.
- You can click **"Download Single index.html"** at any time to export the file.
- If you ever need to adjust anything, click **"Edit Profile Info"** in the top banner.

---

## 🌐 Deployment Option 1: Deploy on Render (Takes 2 Minutes)

Render provides free, fast static site hosting with automated SSL/HTTPS and global CDN.

### Steps:
1. Push this project folder to your GitHub:
   ```bash
   git add .
   git commit -m "Update portfolio for Ruchir Yewale"
   git branch -M main
   git remote add origin https://github.com/<YOUR_GITHUB_USERNAME>/ruchir-portfolio.git
   git push -u origin main
   ```
2. Go to [https://dashboard.render.com/](https://dashboard.render.com/) and sign in with GitHub.
3. Click **"New +"** and choose **"Static Site"**.
4. Select your `ruchir-portfolio` repository.
5. Fill in the details:
   - **Name**: `ruchir-yewale-portfolio`
   - **Branch**: `main`
   - **Build Command**: *(leave blank)*
   - **Publish Directory**: `.` *(or `./`)*
6. Click **"Create Static Site"**.
7. Render will build and provide a live URL like `https://ruchir-yewale-portfolio.onrender.com` with HTTPS enabled!

---

## ☁️ Deployment Option 2: Deploy on AWS S3 + CloudFront (Mini Project Rubric)

Follow these exact steps to complete Mini Project No. 2:

### Step 1: Create an S3 Bucket
1. Log in to [AWS Management Console](https://console.aws.amazon.com/) and open the **S3** service.
2. Click **Create bucket**.
3. Choose a globally unique bucket name (e.g. `ruchir-portfolio-2026`).
4. Select your AWS Region (e.g. `ap-south-1` Mumbai or `us-east-1` N. Virginia).
5. Under **Block Public Access settings for this bucket**:
   - Uncheck **Block *all* public access**.
   - Check the acknowledgement box *"I understand that the bucket and objects will become public"*.
6. Click **Create bucket**.

### Step 2: Upload Files
1. Open your bucket `ruchir-portfolio-2026`.
2. Click **Upload** -> **Add files** -> Select `index.html`.
3. Click **Upload**.

### Step 3: Enable Static Website Hosting
1. In your bucket, go to the **Properties** tab.
2. Scroll to the bottom to **Static website hosting** and click **Edit**.
3. Choose **Enable**.
4. In **Index document**, type `index.html`.
5. Click **Save changes**.
6. Copy the **Bucket website endpoint** (e.g., `http://ruchir-portfolio-2026.s3-website.ap-south-1.amazonaws.com`).

### Step 4: Add Bucket Policy (Make Objects Public)
1. In your bucket, go to the **Permissions** tab.
2. Scroll to **Bucket policy** and click **Edit**.
3. Paste the following JSON (replace `ruchir-portfolio-2026` with your exact bucket name):
   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Sid": "PublicReadGetObject",
         "Effect": "Allow",
         "Principal": "*",
         "Action": "s3:GetObject",
         "Resource": "arn:aws:s3:::ruchir-portfolio-2026/*"
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

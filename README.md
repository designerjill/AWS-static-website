File provided for this project

---

## 📌 Overview
- **Source:** GitHub (or AWS CodeCommit) repository  
- **Deploy Target:** Amazon S3 bucket with static website hosting enabled  
- **CI/CD Service:** AWS CodePipeline  
- **Trigger:** Commit to the chosen repository branch  

---

## 🛠️ Setup (AWS Console)

### 1. Create Repository
- **If using GitHub:**
  1. Create a new repository in GitHub.  
  2. Upload your `index.html` file through the GitHub web interface (*Add file → Upload files*).  

- **If using AWS CodeCommit:**
  1. In the AWS Console, go to **CodeCommit → Repositories → Create repository**.  
  2. Upload your `index.html` file via the CodeCommit console (*Add file → Upload file*).  

---

### 2. Create and Configure S3 Bucket
1. In AWS Console, open **S3 → Create bucket**.  
2. Enter a unique name (e.g., `my-static-site-demo-123`).  
3. Uncheck **Block all public access** (for demo purposes).  
4. Once created, open the bucket → **Properties → Static website hosting** → Enable → set `index.html` as the root.  
5. Go to **Permissions → Bucket policy**, and paste the following (replace `BUCKET_NAME` with your bucket name):  

```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Sid": "PublicReadGetObject",
    "Effect": "Allow",
    "Principal": "*",
    "Action": ["s3:GetObject"],
    "Resource": ["arn:aws:s3:::BUCKET_NAME/*"]
  }]
}

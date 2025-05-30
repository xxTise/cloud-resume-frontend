📚 Cloud Resume Challenge (Frontend)

This is the frontend repository for my Cloud Resume Challenge project. It hosts my resume as a static website using HTML and CSS, deployed to AWS S3 and distributed globally through CloudFront. It also includes a live visitor counter powered by a backend Lambda function.

🌐 Live Demo

https://d4g127h1nwgia.cloudfront.net

🌈 Architecture Diagram



⚖️ Tech Stack / Tools Used

HTML/CSS (Resume styling and structure)

AWS S3 (Static website hosting)

AWS CloudFront (CDN and HTTPS)

AWS Route 53 (Domain routing - optional)

GitHub Actions (CI/CD pipeline)

API Gateway (Invoke backend Lambda)

JavaScript (Visitor counter script)

⚙️ How It Works

HTML and CSS files are hosted in an S3 bucket.

CloudFront provides global distribution and HTTPS.

A JavaScript function calls an API Gateway endpoint.

API Gateway triggers a Lambda function that updates DynamoDB.

The visitor count is returned and displayed on the resume.

🚀 Deployment Steps

1. Manual Setup (for reference)

Create an S3 bucket, enable static website hosting.

Upload index.html and style.css.

Set bucket policy for public read (or use OAC with CloudFront).

Create CloudFront distribution.

name: Deploy Frontend
on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Sync to S3
        run: aws s3 sync . s3://tise-cloud-resume-2025-tise --delete
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_REGION: 'us-east-1'

      - name: Invalidate CloudFront Cache
        run: aws cloudfront create-invalidation --distribution-id YOUR_DISTRIBUTION_ID --paths "/*"
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}

🛠️ Notable Challenges

Bucket Policy Access Denied — Resolved by setting correct IAM policy and using CloudFront OAC.

ACL errors — Resolved by disabling ACLs and updating Terraform configuration.

Real-time updates — Set up GitHub Actions to push changes directly from local machine.

✨ Outcome

Fully deployed static resume

Real-time visitor counter using serverless stack

Hands-on with frontend hosting on AWS


### Frontend Repo:
📁 cloud-resume-frontend
┣ 📄 index.html
┣ 📄 style.css
┣ 📁 .github/workflows
┃ ┗ 📄 deploy.yml
┗ 📄 README.md




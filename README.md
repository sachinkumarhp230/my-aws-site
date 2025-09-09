Static Website Hosting with AWS S3, CloudFront & GitHub Actions

This project demonstrates how to deploy a static website using:

Amazon S3 → Storage for static files (HTML, CSS, JS).

Amazon CloudFront (with OAC) → CDN for fast, secure global delivery.

GitHub Actions → CI/CD automation for deployments.

---

Architecture
GitHub Repository → GitHub Actions → Amazon S3 → Amazon CloudFront → User


Developer pushes code → GitHub Actions triggers.

GitHub Actions uploads files to S3.

CloudFront fetches files securely via Origin Access Control (OAC).

End-users access website through CloudFront distribution URL.

----

Tech Stack

AWS S3 – Static website hosting

AWS CloudFront (OAC) – Secure content delivery

GitHub Actions – CI/CD automation

HTML / CSS / JS – Website content

---

Setup Instructions

Create an S3 Bucket

Bucket name: my-aws-site-sachinkumarhp230

Disable public access.

Enable Static Hosting

Upload website files (index.html, error.html).

Configure CloudFront with OAC

Create a new CloudFront distribution.

Set the S3 bucket as the origin.

Enable Origin Access Control (OAC) to restrict direct S3 access.

Update Bucket Policy

Grant CloudFront OAC permission to read from the bucket.

Add GitHub Actions Workflow (.github/workflows/deploy.yml)

name: Deploy to S3

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1

      - name: Deploy to S3
        run: aws s3 sync . s3://my-aws-site-sachinkumarhp230 --delete


Commit & Push Code

Website auto-deploys on push to main.

---

Live Website

👉 https://d38gsbue97vxxs.cloudfront.net

---

Website Preview

<img width="1450" height="516" alt="image" src="https://github.com/user-attachments/assets/8f5a3a99-031d-4c7d-bef5-2e39199de113" />

---

Common Issues & Fixes

AccessDenied Error → Fixed by updating bucket policy with OAC permissions.

Invalid Principal Error → Occurs if OAI is used with OAC. Ensure correct OAC setup.

Cache not updating → Invalidate CloudFront cache after deployments.

---

Future Improvements

Add custom domain via Route 53.

Enable HTTPS with AWS Certificate Manager.

Add automated tests before deployment.

---

Author

Sachinkumar H P

💼 LinkedIn

💻 GitHub: sachinkumarhp230

✅ Project complete – Static website is live via AWS S3 + CloudFront + GitHub Actions!

# Static Website Hosting with AWS S3, CloudFront & GitHub Actions

This project demonstrates how to deploy a static website using:

- **Amazon S3** – Storage for static files (HTML, CSS, JS)  
- **Amazon CloudFront (with OAC)** – CDN for fast, secure global delivery  
- **GitHub Actions** – CI/CD automation for deployments  

---

## Architecture

GitHub Repository → GitHub Actions → Amazon S3 → Amazon CloudFront → User

- Developer pushes code → GitHub Actions triggers  
- GitHub Actions uploads files to S3  
- CloudFront fetches files securely via Origin Access Control (OAC)  
- End-users access the website through CloudFront distribution URL  

---

## Tech Stack

- **AWS S3** – Static website hosting  
- **AWS CloudFront (OAC)** – Secure content delivery  
- **GitHub Actions** – CI/CD automation  
- **HTML / CSS / JS** – Website content  

---

## Setup Instructions

### 1. Create an S3 Bucket
- Bucket name: `my-aws-site-sachinkumarhp230`  
- Disable public access  
- Enable **Static Website Hosting**  
- Upload website files: `index.html`, `error.html`  

### 2. Configure CloudFront with OAC
- Create a new **CloudFront distribution**  
- Set the S3 bucket as the **origin**  
- Enable **Origin Access Control (OAC)** to restrict direct S3 access  

### 3. Update Bucket Policy
- Grant CloudFront OAC permission to read from the bucket  

### 4. Add GitHub Actions Workflow
Create `.github/workflows/deploy.yml`:

```yaml
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

# Commands to push code
git add .
git commit -m "Initial commit"
git push origin main

## Live Website
[View Live Website](https://d38gsbue97vxxs.cloudfront.net)

## Website Preview
<img width="1450" height="516" alt="image" src="https://github.com/user-attachments/assets/0d492234-3e30-4091-a9b7-01fd471f67da" />

## Common Issues & Fixes
- **AccessDenied Error** → Update bucket policy with OAC permissions
- **Invalid Principal Error** → Ensure correct OAC setup; do not mix OAI with OAC
- **Cache not updating** → Invalidate CloudFront cache after deployments

## Future Improvements
- Add a custom domain via Route 53
- Enable HTTPS with AWS Certificate Manager
- Add automated tests before deployment

## Author
**Sachinkumar H P**  
- LinkedIn: [www.linkedin.com/in/sachinkumarhp](https://www.linkedin.com/in/sachinkumarhp)  
- GitHub: [sachinkumarhp230](https://github.com/sachinkumarhp230)

## Project complete
Static website is live via AWS S3 + CloudFront + GitHub Actions

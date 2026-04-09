# 🚀 Automated AWS Cloud Hosting Pipeline

[![Deploy Static Website](https://github.com/thefurqanx/aws-static-website/actions/workflows/deploy.yml/badge.svg)](https://github.com/thefurqanx/aws-static-website/actions)

## 🌐 Live Project
**URL:** [https://dcq5segpjkbw7.cloudfront.net](https://dcq5segpjkbw7.cloudfront.net)

## 📝 Executive Summary
This project demonstrates a fully automated **CI/CD pipeline** for hosting high-performance static websites. By leveraging **AWS (S3 & CloudFront)** and **GitHub Actions**, I have eliminated manual deployments, ensuring that any code change pushed to the repository is globally live within seconds.

---

## 🏗️ Architecture Overview
The system is built on a "Serverless" architecture to ensure maximum uptime and minimum cost.

* **Hosting:** **Amazon S3** serves as the origin storage for all web assets.
* **CDN:** **Amazon CloudFront** provides global edge caching and HTTPS termination.
* **Automation:** **GitHub Actions** handles the build, sync, and cache invalidation.
* **Security:** Integrated **DevSecOps** principles using AWS IAM and Secret Management.

---

## 🔒 Security Focus (DevSecOps)
Coming from a **Cybersecurity background** (Google Cybersecurity Professional Certificate & TryHackMe), I prioritized a "Security-First" approach for this infrastructure:

* **Principle of Least Privilege:** Instead of using root credentials, I configured a dedicated IAM user with a scoped policy restricted strictly to S3 syncing and CloudFront invalidation.
* **Secret Masking:** Sensitive AWS Access Keys are never hardcoded. They are managed via **Encrypted GitHub Secrets**, ensuring they are masked in logs and protected from unauthorized access.
* **Secure Delivery:** Forced HTTPS through CloudFront to ensure data in transit is encrypted.

---

## ⚙️ Technical Deep Dive: The Pipeline
The "Brain" of this project is the `.github/workflows/deploy.yml` file. Here is how it functions:

1.  **Trigger:** The workflow initiates only on a `push` to the `main` branch.
2.  **Environment:** GitHub spins up a temporary **Ubuntu Linux** runner.
3.  **Authentication:** The runner logs into AWS using secure environment variables.
4.  **S3 Sync:** The `aws s3 sync` command updates only changed files and removes deleted ones to maintain a clean origin.
5.  **Invalidation:** A CloudFront Invalidation is created for `/*` to purge the edge cache and deliver fresh content instantly.

---

## 🛠️ Deployment Workflow
To update the live site, I follow the standard Git-based DevOps workflow:

```bash
# 1. Stage changes
git add .

# 2. Create a versioned snapshot
git commit -m "feat: description of update"

# 3. Trigger the automated pipeline
git push origin main

# 🚀 Automated AWS Cloud Hosting Pipeline

[![Deploy Static Website](https://github.com/thefurqanx/aws-static-website/actions/workflows/deploy.yml/badge.svg)](https://github.com/thefurqanx/thefurqanx/actions)

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
* **Security:** Managed via **AWS IAM** with the Principle of Least Privilege.



---

## ⚙️ Technical Deep Dive: The Pipeline
The "Brain" of this project is the `.github/workflows/deploy.yml` file. Here is how it functions:

1.  **Trigger:** The workflow initiates only on a `push` to the `main` branch.
2.  **Environment:** GitHub spins up a temporary **Ubuntu Linux** runner.
3.  **Authentication:** The runner logs into AWS using **Encrypted GitHub Secrets**.
4.  **S3 Sync:** The `aws s3 sync` command updates only the changed files and removes deleted ones.
5.  **Invalidation:** A CloudFront Invalidation is created for `/*` to ensure users see the fresh content immediately instead of the old cached version.

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

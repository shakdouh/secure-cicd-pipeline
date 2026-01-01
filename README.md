# DevSecOps Pipeline: Automated Vulnerability Scanning with Jenkins & Trivy

This project demonstrates a production-ready **DevSecOps pipeline** that integrates automated security gates into the CI/CD workflow. It ensures that no container image with **Critical** or **High** vulnerabilities is ever deployed to production.

## 🚀 Project Overview
In modern software development, security cannot be an afterthought. This pipeline implements a **"Security-First"** approach by:
1.  Building a containerized Node.js application.
2.  Scanning the image for OS and Library vulnerabilities using **Trivy**.
3.  Generating a visual HTML security report.
4.  Enforcing a "Fail-Fast" policy where builds are aborted if critical risks are detected.

## 🛠 Tech Stack
* **CI/CD Orchestration:** Jenkins (Pipeline-as-Code)
* **Containerization:** Docker (Engine-based on WSL2)
* **Security Scanning:** Aqua Security Trivy
* **Application:** Node.js / Express
* **Reporting:** Jenkins HTML Publisher Plugin

## 🏗 Pipeline Architecture
The `Jenkinsfile` defines the following stages:
* **Checkout:** Pulls the latest code from GitHub.
* **Build Image:** Creates a Docker image using an optimized `Dockerfile`.
* **Security Scan (Trivy):** * Generates a full HTML report for audit purposes.
    * Performs a hard-stop check for `CRITICAL` vulnerabilities (`--exit-code 1`).
* **Deploy:** Runs the application container only if it passes all security gates.

## 🔌 Vulnerability Management Strategy
To ensure a secure yet functional deployment, the following strategies were implemented:
* **Base Image Optimization:** Migrated from `node:slim` (Debian-based) to `node:alpine` to reduce the attack surface.
* **Dependency Hardening:** Upgraded NPM packages to versions with patched vulnerabilities.
* **Risk Mitigation:** Configured the pipeline to handle "Will Not Fix" upstream vulnerabilities while blocking exploitable critical threats.

## 📊 Visual Security Reports
After each build, a detailed security report is published directly within Jenkins:

### 1. Security Scan Results (HTML Report)
![Trivy Report](https://github.com/shakdouh/secure-cicd-pipeline/blob/main/screenshots/01%20Trivy%20Security%20Report.png)
*Visual breakdown of vulnerabilities by severity.*

### 2. Jenkins Pipeline Stage View
![Pipeline View](https://github.com/shakdouh/secure-cicd-pipeline/blob/main/screenshots/02%20The%20pipeline%20success%20.png)
*The pipeline successfully passing all security gates.*

## 📋 Local Setup (WSL2)
1.  **Install Trivy inside Jenkins Container:**
    ```bash
    wget [https://github.com/aquasecurity/trivy/releases/download/v0.49.1/trivy_0.49.1_Linux-64bit.deb](https://github.com/aquasecurity/trivy/releases/download/v0.49.1/trivy_0.49.1_Linux-64bit.deb)
    dpkg -i trivy_0.49.1_Linux-64bit.deb
    ```
2.  **Jenkins Plugin Configuration:** Install the `HTML Publisher` plugin to view security reports.
3.  **Run Pipeline:** Point your Jenkins Pipeline job to this repository.

## 💡 Key DevSecOps Learnings
* Integrating **Vulnerability Scanning** into automated workflows.
* Managing **Compliance Gates** using exit codes in CI/CD.
* Optimizing Docker Images for security using **Minimal Base Images (Alpine)**.
* Analyzing **CVE (Common Vulnerabilities and Exposures)** reports.

---
**Connect with me:** [Hesham Shakdouh] - [www.linkedin.com/in/hesham-shakdouh-87bb57201]

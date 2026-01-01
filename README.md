# Secure-App CI/CD: Professional DevSecOps Pipeline

This repository demonstrates a comprehensive **DevSecOps Lifecycle**. It is not just a deployment script; it is a security-hardened pipeline that integrates **Automated Vulnerability Scanning**, **Visual Security Reporting**, and **Real-time Alerting**.

## 🚀 The Mission
This project implements a **"Security-First"** approach. The pipeline automatically blocks any deployment containing **CRITICAL** vulnerabilities, protecting the production environment from known exploits (CVEs).

## 🛠 Tech Stack
* **Orchestration:** Jenkins (Declarative Pipeline)
* **Runtime:** Docker (Engine on WSL2)
* **Security Scanner:** Aqua Security Trivy
* **Environment:** Node.js / Express.js
* **Reporting:** Jenkins HTML Publisher
* **Notifications:** SMTP / Jenkins Mailer

## 🏗 Pipeline Architecture
The pipeline is divided into strategic stages:
1. **Checkout:** Syncs code from GitHub.
2. **Build:** Creates a Docker image using an optimized `node:alpine` base.
3. **Security Scan:** Generates HTML reports and enforces a "Fail-Fast" policy for `CRITICAL` risks.
4. **Deploy:** Only runs if the security gate is passed.
5. **Post-Actions:** Sends email alerts on failure.

---

## 📸 Project Showcases (Screenshots)

### 1. Jenkins Pipeline Workflow
This shows the successful execution of all stages from checkout to deployment.
![Pipeline View](https://github.com/shakdouh/secure-cicd-pipeline/blob/main/screenshots/02%20The%20pipeline%20success%20.png)

### 2. Trivy Visual Security Report
A detailed HTML report published inside Jenkins, showing the breakdown of vulnerabilities.
![Trivy Report](https://github.com/shakdouh/secure-cicd-pipeline/blob/main/screenshots/01%20Trivy%20Security%20Report.png)

### 3. Automated Email Alert
The notification sent to the security team when a critical vulnerability is detected.
![Email Alert](https://github.com/shakdouh/secure-cicd-pipeline/blob/main/screenshots/04%20Email%20Alert.PNG)

---

## 🔌 Ports & Infrastructure
| Port | Service | Purpose |
| :--- | :--- | :--- |
| **8080** | **Jenkins Dashboard** | CI/CD Management. |
| **3000** | **Production Web App** | The live Node.js application. |

## 📧 Automated Alerting
If a critical threat is found, the deployment is blocked, and an email is triggered with a direct link to the report:
> "⚠️ Security Alert: Pipeline Failed - Build #XX. Please check the detailed Trivy Report."

## 📋 How to Replicate
1. **Clone the Repository:**
   ```bash
   git clone [https://github.com/shakdouh/secure-cicd-pipeline.git](https://github.com/shakdouh/secure-cicd-pipeline.git)


2. Prepare Jenkins: Install Trivy inside your Jenkins container:
   wget [https://github.com/aquasecurity/trivy/releases/download/v0.49.1/trivy_0.49.1_Linux-64bit.deb](https://github.com/aquasecurity/trivy/releases/download/v0.49.1/trivy_0.49.1_Linux-64bit.deb)
dpkg -i trivy_0.49.1_Linux-64bit.deb

3. Configure SMTP: Enable email alerts in Manage Jenkins > System.
## 💡 Key DevSecOps Hardening
* Minimal Base Images: Using alpine to reduce attack surface.

* Fail-Fast Strategy: Blocking insecure code before it runs.

* Observability: Turning raw data into actionable visual reports.

Maintained by: [Hesham Shakdouh]


**Connect with me:** [Hesham Shakdouh] - [www.linkedin.com/in/hesham-shakdouh-87bb57201]

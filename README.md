# 🚀 End-to-End DevOps CI/CD Pipeline (Jenkins + Docker + SonarQube + AWS)

## 📌 Project Overview

This project demonstrates a complete CI/CD pipeline that automates build, code quality analysis, containerization, and deployment to AWS EC2.

---

## 🛠️ Tech Stack

* Jenkins (CI/CD)
* Docker (Containerization)
* SonarQube (Code Quality Analysis)
* AWS EC2 (Deployment)
* GitHub (Source Control)

---

## 🔄 Pipeline Workflow

1. Code pushed to GitHub
2. Jenkins triggers pipeline
3. SonarQube performs code analysis
4. Quality Gate validation
5. Docker image build
6. Push image to DockerHub
7. Deploy container to AWS EC2

---

## 🧩 Architecture

(Add diagram image here)

---

## 📸 Screenshots

### Jenkins Pipeline

![Pipeline](screenshots/pipeline-success.png)

### SonarQube Report

![Sonar](screenshots/sonar-report.png)

### Deployed Application

![App](screenshots/deployed-app.png)

---

## ⚙️ Key Features

* Automated CI/CD pipeline
* Integrated code quality checks
* Containerized deployment
* Cloud-based hosting

---

## 🚀 How to Run

1. Clone repo
2. Configure Jenkins
3. Add credentials
4. Run pipeline

---

## 📈 Future Improvements

* Add Kubernetes deployment
* Add security scanning (Trivy)
* Implement monitoring (Prometheus + Grafana)

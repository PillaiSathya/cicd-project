# 🚀 End-to-End CI/CD GitOps Pipeline with Jenkins, Docker, Kubernetes & ArgoCD

## 📖 Project Overview

This project demonstrates an end-to-end CI/CD GitOps pipeline that automates the complete software delivery lifecycle—from source code changes to deployment on Kubernetes.

The pipeline builds a Java application using Maven, creates and pushes a Docker image to Docker Hub, automatically updates the Kubernetes deployment manifest with the latest image tag, commits the updated manifest back to GitHub, and lets ArgoCD automatically synchronize the Kubernetes cluster.

The project was built to gain practical experience with modern DevOps practices including CI/CD automation, GitOps, containerization, Kubernetes deployments, rolling updates, and infrastructure automation.

---

# 🛠️ Tech Stack

* Java
* Maven
* Git & GitHub
* Jenkins
* Docker
* Docker Hub
* Kubernetes
* ArgoCD
* Linux (Ubuntu WSL)
* Ansible (initial deployment phase)

---

# 🏗️ Project Architecture

```text
Developer
    │
    │ git push
    ▼
GitHub Repository
    │
    ▼
Jenkins Pipeline
    │
    ├── Maven Build
    ├── Unit Testing
    ├── Docker Build
    ├── Docker Push
    ├── Update Kubernetes Manifest
    └── Commit & Push Manifest
                │
                ▼
          GitHub Repository
                │
                ▼
         ArgoCD Auto Sync
                │
                ▼
       Kubernetes Cluster
                │
                ▼
      Rolling Update Deployment
```

---

# ✨ Features

* Automated Maven Build
* Automated Unit Testing
* Docker Image Creation
* Docker Image Push to Docker Hub
* Automatic Kubernetes Manifest Update
* GitOps Workflow using ArgoCD
* Automatic Kubernetes Deployment
* Rolling Updates with Zero Downtime
* Jenkins Credential Management
* GitHub Integration
* Docker Hub Integration

---

# 📁 Project Structure

```text
.
├── Dockerfile
├── Jenkinsfile
├── README.md
├── pom.xml
├── ansible/
├── k8s/
│   ├── deployment.yaml
│   └── service.yaml
├── screenshots/
│   ├── cicd_main/
│   └── K8s/
└── src/
    ├── main/
    └── test/
```

---

# ⚙️ Jenkins Pipeline Stages

### 1. Source Checkout

Fetches the latest source code from GitHub.

### 2. Maven Build

Compiles the Java application and generates the executable JAR.

### 3. Unit Testing

Executes Maven test cases to validate the application.

### 4. Docker Build

Builds a Docker image from the generated application.

### 5. Docker Login

Authenticates Jenkins with Docker Hub using stored credentials.

### 6. Docker Push

Pushes the newly built image to Docker Hub using the Jenkins build number as the image tag.

### 7. Update Kubernetes Manifest

Automatically updates the image version inside `k8s/deployment.yaml`.

Example:

```yaml
image: pillaisathya/cicd-project:32
```

### 8. Commit & Push Manifest

Commits the updated Kubernetes manifest and pushes it back to GitHub.

---

# ☸️ GitOps Workflow

ArgoCD continuously monitors the GitHub repository.

Whenever Jenkins updates the Kubernetes manifest:

* ArgoCD detects the Git commit.
* Synchronizes the cluster automatically.
* Deploys the latest Docker image.
* Performs a Kubernetes Rolling Update.

No manual `kubectl apply` command is required after the initial setup.

---

# 🔄 Kubernetes Rolling Update

The deployment strategy ensures zero downtime.

During each deployment:

* New Pods are created.
* Health is verified.
* Old Pods are terminated only after the new Pods become ready.

---

# 📷 Project Screenshots

The repository includes screenshots demonstrating:

* Maven Build
* Docker Image Push
* Jenkins Pipeline Success
* Kubernetes Deployment
* Kubernetes Service
* ArgoCD Installation
* ArgoCD Application
* Rolling Update
* GitOps Deployment
* Final Working Application

---

# 🎯 Key Learnings

During this project I learned:

* Building CI/CD pipelines using Jenkins
* Docker image creation and publishing
* Kubernetes Deployments and Services
* ReplicaSets and Rolling Updates
* GitOps concepts using ArgoCD
* Jenkins Credentials Management
* GitHub automation
* Kubernetes manifest management
* Troubleshooting Jenkins, Docker and Kubernetes issues
* Resolving recursive CI trigger loops caused by Jenkins committing back to the same repository

---

# 🚀 Future Improvements

* GitHub Webhooks using ngrok
* Helm Charts
* Kubernetes Ingress
* Prometheus Monitoring
* Grafana Dashboards
* Deploy to AWS EKS
* SonarQube Quality Gates
* Nexus Artifact Repository Integration

---

# 👨‍💻 Author

**Pillai Sathya Sudalai**

DevOps Engineer Aspirant

* GitHub: https://github.com/PillaiSathya

---

## ⭐ If you found this project useful, consider giving it a star.


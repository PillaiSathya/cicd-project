# Automated CI/CD Pipeline with Jenkins

## Project Overview

This project demonstrates a complete CI/CD pipeline using Jenkins for automating build, code analysis, artifact management, containerization, and deployment.

The pipeline automates the software delivery process from source code commit to application deployment using modern DevOps tools and practices.

---

## Technologies Used

- Jenkins
- Git & GitHub
- Maven
- SonarQube
- Nexus Repository
- Docker
- Ansible
- Java
- Linux

---

## Project Architecture

Developer Push → GitHub → Jenkins Pipeline → Maven Build → SonarQube Analysis → Nexus Artifact Upload → Docker Build → Ansible Deployment → Application Running

---

## Pipeline Stages

### 1. Checkout Source Code
Jenkins pulls the latest code from GitHub repository.

### 2. Build Application
Maven compiles the Java application and generates the JAR file.

### 3. Code Quality Analysis
SonarQube performs static code analysis and validates code quality.

### 4. Publish Artifact
Generated JAR artifact is uploaded to Nexus Repository.

### 5. Docker Build
Docker image is created using the generated application artifact.

### 6. Application Deployment
Ansible playbook deploys and starts the application automatically.

---

## Project Structure

```bash
.
├── ansible/
├── src/
├── target/
├── .mvn/
├── Dockerfile
├── Jenkinsfile
├── pom.xml
└── README.md
```

## Jenkins Pipeline Stages

1. Source Code Checkout

Jenkins pulls the latest source code from GitHub repository.

2. Maven Build

The application is compiled and packaged into a JAR file using Maven.

3. SonarQube Analysis

Static code analysis is performed to validate code quality.

4. Artifact Upload

The generated artifact is uploaded to Nexus Repository.

5. Docker Build

A Docker image is created using the generated JAR file.

6. Deployment using Ansible

Ansible playbook deploys and starts the application automatically.

## Sample Successful Pipeline Output

TASK [Start application] ************************************************

changed: [localhost]

PLAY RECAP **************************************************************

localhost : ok=5 changed=3 unreachable=0 failed=0 skipped=0 rescued=0 ignored=1

Finished: SUCCESS

## Screenshots Included

Jenkins Pipeline Success
Nexus Artifact Upload
Maven Build Output
CI/CD Console Logs
SonarQube Integration

## Author

Sathya
DevOps Engineer Aspirant
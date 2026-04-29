# Content for the README.md file
readme_content = """# 🚀 SkillPulse: Automated 3-Tier Application Deployment

This repository contains a full-stack **SkillPulse** application deployed using a modern DevSecOps pipeline with **GitHub Actions**, **Docker Compose**, and **AWS EC2**.

---

## 🏗️ Architecture Overview

The project implements a classic 3-tier architecture:
1.  **Frontend**: Nginx serving a React application (Web Layer).
2.  **Backend**: Go-based REST API (Application Layer).
3.  **Database**: MySQL 8.4 (Data Layer).

The CI/CD pipeline automates the build process, pushes images to Docker Hub, and triggers a remote deployment on an AWS EC2 instance.

---

## 🛠️ Tech Stack
- **Cloud**: AWS (EC2)
- **Containerization**: Docker, Docker Compose
- **CI/CD**: GitHub Actions
- **Backend**: Go (Golang)
- **Frontend**: React / Nginx
- **Database**: MySQL

---

## 🚀 Setup & Deployment Steps

### 1. Prerequisites
- An AWS EC2 instance (Ubuntu/Amazon Linux) with Docker and the Docker Compose plugin installed.
- A Docker Hub account.
- GitHub repository with the project code.

### 2. Configure GitHub Secrets
Add the following secrets to your GitHub repository (**Settings > Secrets and variables > Actions**):
- `DOCKERHUB_USERNAME`: Your Docker Hub username.
- `DOCKERHUB_TOKEN`: Your Docker Hub Personal Access Token.
- `HOST`: Your EC2 Public IP address.
- `EC2_USER`: The SSH username (e.g., `ubuntu` or `ec2-user`).
- `EC2_SSH_KEY`: The content of your `.pem` private key file.

### 3. Prepare the EC2 Environment
Ensure the Docker Compose plugin is globally accessible. If you encounter a "command not found" error during the action, run these commands on your EC2:
```bash
sudo mkdir -p /usr/lib/docker/cli-plugins
sudo cp /root/.docker/cli-plugins/docker-compose /usr/lib/docker/cli-plugins/
sudo chmod +x /usr/lib/docker/cli-plugins/docker-compose

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
```

4. Running the Pipeline
CI Workflow: Triggered on every push to the main branch. It builds images and pushes them to Docker Hub.

CD Workflow: Automatically starts after a successful CI run. It SSHes into your EC2, pulls the latest images, and restarts the containers.

5. Manual Execution (Optional)
If you wish to run the project manually on the EC2:
```
git clone [https://github.com/vishalrwagh1999/github-action-CI-CD-dockerCompose.git](https://github.com/vishalrwagh1999/github-action-CI-CD-dockerCompose.git)
cd github-action-CI-CD-dockerCompose
export DOCKERHUB_USERNAME=your_username
docker compose up -d
```
⚠️ Troubleshooting & Lessons Learned
Environment Variables: Docker Compose requires the DOCKERHUB_USERNAME to be exported in the shell session to resolve image names in the YAML file.

SSH Path Issues: Non-interactive SSH shells might not load the same PATH as manual logins. Always ensure the Docker Compose plugin is in /usr/lib/docker/cli-plugins/.

Database Persistence: Ensure the mysql_data volume is defined to keep your data safe during container restarts.

🔮 Future Roadmap: Kubernetes
The next phase of this project involves migrating from Docker Compose to Kubernetes (K8s) to leverage:

Self-healing: Auto-restarting failed pods.

Auto-scaling: Scaling based on traffic via HPA.

Zero-downtime: Rolling updates for seamless deployments.

Developed by Vishal Wagh.

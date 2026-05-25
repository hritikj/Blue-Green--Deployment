# 🔵🟢 Blue-Green Deployment for Python Tic Tac Toe Application

## 📌 Project Overview

This project demonstrates a complete Blue-Green Deployment strategy using:

* Python Flask Application
* Docker Multi-Stage Build
* Docker Compose
* Jenkins CI/CD Pipeline
* NGINX Reverse Proxy
* GitHub Webhook Integration

The application is a simple Tic Tac Toe web game built in Python and deployed using a zero-downtime deployment strategy.

---

# 🚀 Tech Stack

| Technology     | Purpose                           |
| -------------- | --------------------------------- |
| Python Flask   | Web Application                   |
| Docker         | Containerization                  |
| Docker Compose | Multi-container deployment        |
| Jenkins        | CI/CD Automation                  |
| NGINX          | Reverse Proxy & Traffic Switching |
| GitHub         | Source Code Management            |
| Linux          | Deployment Environment            |

---

# 🏗️ Blue-Green Deployment Architecture

## Architecture Flow

User → NGINX Reverse Proxy → Blue/Green Container → Python Flask App

---

# 🔁 What is Blue-Green Deployment?

Blue-Green deployment is a deployment strategy used to reduce downtime and risk during application releases.

## How it Works

* BLUE = Current live version
* GREEN = New version being deployed
* NGINX switches traffic between Blue and Green
* If Green is healthy → traffic switches to Green
* If deployment fails → rollback to Blue

---

# 📂 Project Structure

```bash
Blue-Green/
│
├── app.py
├── requirements.txt
├── Dockerfile
├── Jenkinsfile
├── docker-compose.yml
│
├── nginx/
│   └── nginx.conf
│
└── templates/
    └── index.html
```

---

# 🐳 Docker Multi-Stage Build

The project uses a multi-stage Docker build for optimized image size.

## Docker Build Stages

### Stage 1

* Install Python dependencies
* Use builder image

### Stage 2

* Copy dependencies from builder stage
* Copy application code
* Run Flask application

---

# ⚙️ Jenkins CI/CD Pipeline

The Jenkins pipeline automates:

✅ GitHub code checkout
✅ Docker image build
✅ Green environment deployment
✅ Health checks
✅ NGINX traffic switching
✅ Blue environment shutdown
✅ Automatic rollback on failure

---

# 🔄 Deployment Workflow

## Step 1: Developer Pushes Code

```bash
git push origin main
```

---

## Step 2: Jenkins Triggered Automatically

GitHub webhook triggers Jenkins pipeline.

---

## Step 3: Docker Image Build

```bash
docker build -t tic-app:latest .
```

---

## Step 4: Deploy GREEN Environment

```bash
docker-compose up -d
```

GREEN container runs on:

```bash
http://localhost:5002
```

---

## Step 5: Health Check

Jenkins validates GREEN deployment:

```bash
curl -f http://localhost:5002
```

---

## Step 6: Switch Traffic to GREEN

NGINX configuration changes:

```nginx
server tic-green:5000;
```

NGINX restart:

```bash
docker restart nginx-proxy
```

---

## Step 7: Stop BLUE Environment

```bash
docker stop tic-blue
```

---

# 🔐 Reverse Proxy Configuration

NGINX acts as a reverse proxy.

## Responsibilities

* Route user traffic
* Switch between Blue and Green environments
* Improve scalability
* Reduce downtime

---

# 🧪 Health Check Strategy

Before switching traffic:

* Jenkins validates Green deployment
* Checks application availability
* Prevents broken deployments from going live

---

# 🚨 Rollback Strategy

If GREEN deployment fails:

* Traffic automatically switches back to BLUE
* Existing production version remains active
* Prevents downtime

Rollback handled inside Jenkins post-failure block.

---

# ▶️ Running the Project

## Clone Repository

```bash
git clone https://github.com/hritikj/Blue-Green.git
```

---

## Start Jenkins

Ensure Jenkins and Docker are installed.

---

## Run Docker Compose

```bash
docker-compose up -d
```

---

## Access Application

```bash
http://localhost
```

---

# 🛠️ Useful Commands

## View Running Containers

```bash
docker ps
```

---

## View Logs

```bash
docker logs nginx-proxy
```

---

## Stop Containers

```bash
docker-compose down
```

---

## Restart NGINX

```bash
docker restart nginx-proxy
```

---

# 📈 Features

✅ Zero-downtime deployment
✅ Automated CI/CD pipeline
✅ Blue-Green deployment strategy
✅ Docker multi-stage build
✅ Jenkins automation
✅ NGINX reverse proxy
✅ Automated rollback
✅ Health monitoring

---

# 🔥 Future Enhancements

* Kubernetes deployment
* AWS ECS/EKS deployment
* Monitoring with Prometheus & Grafana
* Canary deployment strategy
* Automated testing stage
* HTTPS with SSL certificates
* Load balancing

---

# 📚 Learning Outcomes

This project helps understand:

* Blue-Green deployment strategy
* CI/CD pipelines using Jenkins
* Docker multi-stage builds
* Reverse proxy configuration
* Automated rollback mechanisms
* Zero downtime deployments
* DevOps automation workflows

---

# 👨‍💻 Author

Developed as a DevOps hands-on project to demonstrate Blue-Green Deployment using Python, Docker, Jenkins, and NGINX.

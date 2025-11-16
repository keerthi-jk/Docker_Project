Flask + Redis | Docker | Kubernetes | Helm | GitHub Actions (CI/CD)

This project demonstrates a complete DevOps pipeline using Docker,Docker Compose, Kubernetes, Helm, Redis, and GitHub Actions.
It deploys a Python Flask application that displays pod details, health checks, and a Redis-backed visit counter.

Features
💻 Web Application

Python Flask app
Displays hostname + pod IP
/details page shows a Redis-powered visit counter
/health endpoint used for probes

🐳 Containerization
Dockerfile optimized for Python
Multi-tag push: latest + commit SHA
Healthcheck built into image

☸️ Kubernetes Deployment
Flask Deployment + Service
Redis Deployment + Service
ConfigMap for environment variables
Full inter-service communication over ClusterIP
Liveness & readiness probes

🎛 Helm Chart
Fully parameterized
Manages both Redis and Flask
Easy overrides through values.yaml
Environment injection through ConfigMaps

🔄 CI/CD (GitHub Actions)
CI: Build & push Docker images to Docker Hub
CD: Helm-based deployment pipeline (cloud-ready)
Modular workflow divided into build and deploy jobs

📦 Technologies Used
Python, Flask
Redis
Docker, Docker Compose
Kubernetes (Deployments, Services, ConfigMaps)
Helm
GitHub Actions (CI + CD)
Minikube 

🔧 How to Deploy Using Helm
Install:
helm install webapp ./helm/webapp-python

Upgrade:
helm upgrade webapp ./helm/webapp-python \
  --set image.tag=latest

Remove:
helm uninstall webapp


📜 GitHub Actions Workflow
CI: Build + Push Docker image
CD: Helm upgrade (cloud-ready)
helm upgrade --install webapp ./helm/webapp-python \
  --set image.repository=keerthi973/webapp \
  --set image.tag=${{ github.sha }}

🧪 Local Testing (Minikube)
minikube start
helm install webapp ./helm/webapp-python
minikube service python-webapp-service --url

🐳 Local Development with Docker Compose
For local testing without Kubernetes, you can run the app and Redis together using Docker Compose:
docker compose up --build
This will start:
webapp → Flask container listening on port 5000
redis → Redis container on port 6379
Then visit:
http://localhost:5000/
http://localhost:5000/details (shows hostname, IP and Redis-backed visit counter)


This project demonstrates real-world DevOps practices including containerization, cloud-native application deployment, Helm packaging, Redis integration, and GitHub Actions CI/CD workflows.



Environment injection through ConfigMaps

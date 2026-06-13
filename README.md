# 💬 QuickChat — Real-Time MERN Chat App with Full DevOps Pipeline

A full-stack real-time chat application built with the MERN stack (MongoDB, Express, React, Node.js) and Socket.io — fully containerized, automated with CI/CD, and deployed to the cloud using Docker, GitHub Actions, AWS EC2, and Kubernetes.

🌐 **Live Demo**: [http://13.51.204.208:8080](http://13.51.204.208:8080)

---

## 📌 Overview

QuickChat lets users sign up, find other users, and chat in real-time using WebSockets. This project goes beyond just building the app — it demonstrates a complete **DevOps lifecycle**: containerization, automated builds, cloud deployment, and container orchestration.

---

## ✨ Features

- 🔐 JWT-based authentication & secure password hashing
- ⚡ Real-time messaging with Socket.io
- 🟢 Online/offline user status
- 🖼️ Profile pictures & image sharing via Cloudinary
- 📱 Responsive UI built with React + Tailwind CSS

---

## 🛠️ Tech Stack

**Frontend:** React, Vite, Tailwind CSS, Socket.io-client, Axios
**Backend:** Node.js, Express, Socket.io, MongoDB (Mongoose), JWT
**Database:** MongoDB Atlas (cloud)

**DevOps & Infrastructure:**
- 🐳 **Docker** — Multi-stage builds for client (React + Nginx) and server (Node.js)
- 🧩 **Docker Compose** — Local multi-container orchestration
- ⚙️ **GitHub Actions** — CI/CD pipeline that auto-builds and pushes images to DockerHub on every push
- ☁️ **AWS EC2** — Live cloud deployment
- ☸️ **Kubernetes (Minikube)** — Deployments, Services, and Secrets for container orchestration

---

## 🏗️ Architecture

![Architecture Diagram](docs/architecture-diagram.png)

The pipeline flow:
1. Code pushed to GitHub triggers **GitHub Actions**
2. Actions builds Docker images for client & server
3. Images are pushed to **DockerHub**
4. Images are pulled and run on **AWS EC2** (live deployment)
5. The same images can be deployed to a **Kubernetes cluster** via Deployment/Service manifests

---

## 📸 Screenshots

| Login Page | Chat Interface |
|---|---|
| ![Login](docs/login-screenshot.png) | ![Chat](docs/chat-screenshot.png) |

---

## 🚀 Getting Started (Local Development)

### Prerequisites
- Node.js v18+
- Docker & Docker Compose
- MongoDB Atlas account

### 1. Clone the repository
```bash
git clone https://github.com/Laxmikant-SB/chatapp-devops.git
cd chatapp-devops
```

### 2. Set up environment variables

Create `server/.env`:
MONGODB_URI=your_mongodb_connection_string

PORT=5000

JWT_SECRET=your_jwt_secret

CLOUDINARY_CLOUD_NAME=your_cloud_name

CLOUDINARY_API_KEY=your_api_key

CLOUDINARY_API_SECRET=your_api_secret
Create `client/.env`:
VITE_BACKEND_URL=http://localhost:5000
### 3. Run with Docker Compose
```bash
docker-compose up --build
```

Visit: `http://localhost:8080`

---

## ⚙️ CI/CD Pipeline

Every push to `main` triggers a GitHub Actions workflow ([`.github/workflows/docker-build.yml`](.github/workflows/docker-build.yml)) that:
1. Builds Docker images for client and server
2. Pushes them to DockerHub:
   - `laxmikant07/chatapp-server`
   - `laxmikant07/chatapp-client`

---

## ☁️ Cloud Deployment (AWS EC2)

The app is deployed on an AWS EC2 instance running Ubuntu, with both containers pulled directly from DockerHub:

```bash
docker run -d -p 5000:5000 --env-file server.env --name chatapp-server --restart unless-stopped laxmikant07/chatapp-server:latest
docker run -d -p 8080:80 --name chatapp-client --restart unless-stopped laxmikant07/chatapp-client:latest
```

---

## ☸️ Kubernetes Deployment

The app can also be deployed on a Kubernetes cluster using the manifests in [`/k8s`](./k8s):

```bash
kubectl create secret generic chatapp-server-secret --from-env-file=server/.env
kubectl apply -f k8s/server-deployment.yaml
kubectl apply -f k8s/client-deployment.yaml
```

This creates:
- **Deployments** for client and server (auto-restart on failure)
- **NodePort Services** to expose both apps
- **Secrets** for secure environment variable management

---

## 📁 Project Structure
chatapp-devops/

├── client/                 # React frontend

│   ├── Dockerfile

│   ├── nginx.conf

│   └── src/

├── server/                  # Node.js backend

│   ├── Dockerfile

│   └── ...

├── k8s/                     # Kubernetes manifests

│   ├── server-deployment.yaml

│   └── client-deployment.yaml

├── .github/workflows/       # CI/CD pipeline

│   └── docker-build.yml

├── docker-compose.yml

└── README.md
---

## 👤 Author

**Laxmikant** — [GitHub](https://github.com/Laxmikant-SB)

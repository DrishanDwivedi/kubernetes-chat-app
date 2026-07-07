# 🚀 Real-Time Chat Application Deployment on Kubernetes

A production-ready deployment of a **Full Stack Real-Time Chat Application** using Docker and Kubernetes.

The application provides real-time messaging functionality and has been containerized and deployed using Kubernetes concepts like Deployments, Services, Secrets, Persistent Storage, and Ingress routing.

---

# 📌 Overview

This project focuses on deploying a MERN-based real-time chat application using cloud-native DevOps practices.

The application was migrated from a Docker Compose based setup to Kubernetes, where every component runs independently as a containerized service.

---

# ✨ Features

- 💬 Real-time messaging using Socket.io
- 🔐 Secure Authentication and Authorization using JWT
- 👤 User profile management
- 🟢 Online/offline user status tracking
- 📸 Profile image upload support
- 🎨 Responsive UI built with React and TailwindCSS

---

# 🛠️ Tech Stack

## Frontend

- React.js
- TailwindCSS
- DaisyUI
- Zustand
- Nginx

## Backend

- Node.js
- Express.js
- MongoDB
- Socket.io
- JSON Web Token (JWT)

## DevOps

- Docker
- Docker Compose
- Kubernetes
- Kubernetes Services
- Kubernetes Secrets
- Persistent Volume (PV)
- Persistent Volume Claim (PVC)
- Nginx Ingress Controller

---

# 🏗️ Architecture


```text
                  USER
                   |
                   |
             chat-dd.com
                   |
                   |
          +----------------+
          |    Ingress     |
          +----------------+
                   |
        ----------------------
        |                    |
        |                    |
        v                    v

 Frontend Service       Backend Service
        |                    |
        |                    |
        v                    v

 React + Nginx Pod     Node.js API Pod
                             |
                             |
                     MongoDB Service
                             |
                             |
                       MongoDB Pod
                             |
                             |
                    Persistent Volume
```

---

# 📂 Project Structure


```text
chat-app-kubernetes/

├── backend/
│   ├── Dockerfile
│   └── src/
│
├── frontend/
│   ├── Dockerfile
│   ├── nginx.conf
│   └── src/
│
├── k8s/
│   |
│   ├── namespace.yml
│   |
│   ├── frontend-deployment.yml
│   ├── frontend-service.yml
│   |
│   ├── backend-deployment.yml
│   ├── backend-service.yml
│   |
│   ├── mongodb-deployment.yml
│   ├── mongodb-service.yml
│   ├── mongodb-pv.yml
│   ├── mongodb-pvc.yml
│   |
│   ├── ingress.yml
│   └── secrets.yml
│
├── docker-compose.yml
└── README.md
```

---

# 🐳 Docker Deployment

Build and run using Docker Compose:

```bash
docker-compose up -d --build
```

Check containers:

```bash
docker ps
```

Application:

```text
http://localhost
```

---

# ☸️ Kubernetes Deployment

Create namespace:

```bash
kubectl apply -f k8s/namespace.yml
```

Deploy application:

```bash
kubectl apply -f k8s/
```

Verify pods:

```bash
kubectl get pods -n chat-app
```

Verify services:

```bash
kubectl get svc -n chat-app
```

---

# 🔐 Secrets Management

Sensitive application data is managed using **Kubernetes Secrets**.

The application uses secrets for:

- JWT authentication secret
- Sensitive environment variables

Example Secret:

```yaml
apiVersion: v1
kind: Secret

metadata:
  name: chatapp-secrets

type: Opaque

data:
  jwt: <base64-encoded-value>
```

The JWT secret is injected into the backend container:

```yaml
env:
  - name: JWT_SECRET
    valueFrom:
      secretKeyRef:
        name: chatapp-secrets
        key: jwt
```

The backend uses this secret to:

- Generate JWT tokens after login
- Validate authenticated requests
- Protect private API routes

---

# 💾 Database Persistence

MongoDB data persistence is handled using:

- Persistent Volume (PV)
- Persistent Volume Claim (PVC)

This ensures MongoDB data remains available even if pods restart.

---

# 🌐 Ingress Configuration

Nginx Ingress Controller is used for routing external traffic.

Enable ingress:

```bash
minikube addons enable ingress
```

Apply ingress:

```bash
kubectl apply -f k8s/ingress.yml
```



Ingress handles routing:

```text
/       → Frontend Service

/api    → Backend Service
```

---

# 🔥 Deployment Issues Solved

During Kubernetes migration, several real-world deployment issues were resolved:

- Fixed CrashLoopBackOff errors
- Configured Kubernetes environment variables
- Debugged MongoDB authentication issues
- Implemented service-to-service communication
- Fixed Kubernetes DNS resolution problems
- Configured persistent MongoDB storage
- Fixed frontend/backend routing through Ingress
- Managed application secrets securely

---

# 🚀 Future Improvements

- Helm Chart implementation
- CI/CD pipeline with Jenkins/GitHub Actions
- Monitoring using Prometheus and Grafana
- AWS EKS deployment
- Automated image builds

---


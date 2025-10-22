# DevOps Assignment: Jenkins CI/CD with Nginx Docker

## 🚀 Project Overview

This project demonstrates a **CI/CD pipeline using Jenkins** to build, push, and deploy a **static website served by Nginx** inside a Docker container.
The pipeline is fully automated and triggers on GitHub commits using a webhook.

---

## 📁 Project Structure

```
/project-root
│── Dockerfile        # Dockerfile to build Nginx image
│── index.html        # Simple static website
│── Jenkinsfile       # Jenkins pipeline for CI/CD
```

---

## 🐳 Docker Image

* **DockerHub Image:** [https://hub.docker.com/r/tejaswinism/nginx-app](https://hub.docker.com/r/tejaswinism/nginx-app)
* Built and pushed automatically from Jenkins pipeline.

---

## 🧪 Running Locally

1. Clone the repository:

```bash
git clone https://github.com/tejaswini2704/jenkins-demo.git
cd jenkins-demo
```

2. Build Docker image:

```bash
docker build -t tejaswinism/nginx-app:latest .
```

3. Run the container:

```bash
docker run -d -p 9090:80 --name nginx-app tejaswinism/nginx-app:latest
```

4. Open in browser:

```
http://localhost:9090
```

---

## ⚙️ Jenkins Pipeline (Jenkinsfile)

The pipeline automates CI/CD with the following stages:

1. **Checkout** – Clones the repository from GitHub
2. **Build** – Builds Docker image for Nginx
3. **Push to DockerHub** – Pushes Docker image to DockerHub
4. **Deploy** – Removes previous container (if any) and runs the new container

> Jenkins credentials (ID: `dockerhub`) use a DockerHub **personal access token** for authentication.

---

## 🔗 GitHub Webhook Setup

To automatically trigger the pipeline on GitHub commits:

1. Add a webhook in GitHub **Settings → Webhooks**:

   * Payload URL: `http://<jenkins-server-ip>:8080/github-webhook/`
   * Content type: `application/json`
   * Event: **Just the push event**
2. In Jenkins job → Configure → Build Triggers:

   * Enable **GitHub hook trigger for GITScm polling**

> If using local Jenkins, you can use **ngrok** to expose it temporarily.

---

## 📌 Notes

* Docker container exposes **port 80** internally, mapped to **host port 8080**.
* Jenkins user must have permission to run Docker (`jenkins` in Docker group).
* Replace DockerHub username in Jenkinsfile and commands with your own: `tejaswinism`.

---

## 🔗 Links

* **GitHub Repository:** [https://github.com/tejaswini2704/jenkins-demo](https://github.com/tejaswini2704/jenkins-demo)
* **DockerHub Image:** [https://hub.docker.com/r/tejaswinism/nginx-app](https://hub.docker.com/r/tejaswinism/nginx-app)
* **Deployed App URL:** `http://<your-server-ip>:9090`

---

## ✅ Author

* **Name:** Tejaswini Shirke

<img width="1888" height="958" alt="Screenshot 2025-10-22 214638" src="https://github.com/user-attachments/assets/e2311fe8-5306-4bfd-b6d6-d823772ea1fd" />

<img width="1904" height="953" alt="Screenshot 2025-10-22 214700" src="https://github.com/user-attachments/assets/db33be7f-9085-4c34-b4f0-2ea05ac48cc4" />



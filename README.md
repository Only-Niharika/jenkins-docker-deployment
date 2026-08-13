# Jenkins Docker Deployment Project

## Overview

This project demonstrates a simple **CI/CD pipeline using Jenkins and Docker**. Jenkins automatically pulls the latest code from GitHub, builds a Docker image, removes any existing container, and deploys a new container running an Apache web server.

The application is a basic static website hosted inside a Docker container using the official Apache HTTP Server image.

---

## Project Architecture

```text
GitHub Repository
        │
        ▼
     Jenkins
        │
        ▼
 Docker Build
        │
        ▼
 Docker Image
        │
        ▼
 Docker Container
        │
        ▼
 Static Website on Apache
```

---

## Technologies Used

* Jenkins
* Docker
* Apache HTTP Server (httpd)
* Git & GitHub
* HTML

---

## Project Structure

```text
jenkins-docker-deployment/
│
├── Jenkinsfile
├── Dockerfile
├── index.html
└── README.md
```

---

## Jenkins Pipeline Stages

### 1. Checkout

Pulls the latest source code from the GitHub repository.

```groovy
git branch: 'main',
    url: 'https://github.com/Only-Niharika/jenkins-docker-deployment.git'
```

### 2. Build Docker Image

Builds a Docker image named:

```bash
docker build -t jenkins-docker-app .
```

### 3. Stop Old Container

Stops the running container if it exists.

```bash
docker stop jenkins-docker-container || true
```

### 4. Remove Old Container

Removes the old container to avoid conflicts.

```bash
docker rm jenkins-docker-container || true
```

### 5. Run New Container

Creates and runs a new container.

```bash
docker run -d -p 80:80 --name jenkins-docker-container jenkins-docker-app
```

---

## Docker Configuration

### Base Image

```dockerfile
FROM httpd
```

### Copy Website Files

```dockerfile
COPY . /usr/local/apache2/htdocs/
```

### Expose Port

```dockerfile
EXPOSE 80
```

### Start Apache Server

```dockerfile
CMD ["httpd-foreground"]
```

---

## Website Preview

The deployed website displays:

```html
This Is A Demo Project!!
Testing
Project created by a citizen of earth.
Thanks for reading...
```

---

## How to Run Manually

### Clone Repository

```bash
git clone https://github.com/Only-Niharika/jenkins-docker-deployment.git
cd jenkins-docker-deployment
```

### Build Docker Image

```bash
docker build -t jenkins-docker-app .
```

### Run Container

```bash
docker run -d -p 80:80 --name jenkins-docker-container jenkins-docker-app
```

### Verify Container

```bash
docker ps
```

### Access Application

Open your browser and visit:

```text
http://<EC2-Public-IP>
```

or

```text
http://localhost
```

---

## Jenkins Setup Requirements

* Jenkins installed and running
* Docker installed on Jenkins server
* Jenkins user added to Docker group

```bash
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
```

---

## Future Enhancements

* Add GitHub Webhooks for automatic builds
* Push Docker images to Docker Hub
* Deploy on AWS EC2
* Add Jenkins notifications
* Integrate security scanning tools
* Implement multi-stage Docker builds

---

## Author

**Niharika Karkra**

GitHub: https://github.com/Only-Niharika

---

## License

This project is created for learning and practice purposes as part of DevOps and CI/CD training.

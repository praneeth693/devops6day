# 💊 Medical Billing App - Docker Deployment Guide

This repository outlines how I deployed the **Medical Billing Application** using **Docker** on an AWS EC2 instance. The application uses a multi-container setup to separate the frontend and MongoDB backend, all orchestrated through Docker Compose.

---

## 🚀 Project Overview

- **Frontend**: UI for managing medical billing records
- **Database**: MongoDB NoSQL database
- **Infrastructure**: Deployed on Ubuntu EC2 instance
- **Deployment**: Dockerized using custom Dockerfile and `docker-compose.yml`

---

## 🏠 EC2 Instance Setup

1. **Launch EC2 Instance**

   - OS: Ubuntu
   - Instance type: `t2.medium`
   - Storage: 20GB

2. **Create Key Pair**

   - Format: `.ppk` for PuTTY
   - Download and save locally

3. **Configure Security Group**

   - Open required ports (All TCP or custom as needed)

4. **Connect to EC2 Using PuTTY**
   - Enter host (EC2 Public IP)
   - Browse and add `.ppk` key under SSH > Auth
   - Connect and accept prompt

---

## 🛠️ Server Configuration

### Switch to Root & Update System

```bash
sudo -i
apt update -y
```

### Clone the Project

```bash
git clone https://github.com/Davidgit526/MedicalBilling.git
cd MedicalBilling
```

---

## 🧰 Install Docker & Docker Compose

### Add Docker's GPG Key and Repo

```bash
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo \"${UBUNTU_CODENAME:-$VERSION_CODENAME}\") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
```

### Install Docker Engine & Plugins

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Verify Installation

```bash
docker --version
```

If not visible:

```bash
service docker restart
```

---

## 🚧 Run the Application

### Start Containers

```bash
docker compose up -d
```

- Two containers will be created: Frontend and MongoDB
- Ensure relevant ports are open in EC2 security group

---

## 🔍 Access the App

Open your browser:

```bash
http://<EC2-PUBLIC-IP>:<PORT>
```

Replace `<PORT>` with the app's exposed port.

---

## 🧰 Check MongoDB Data

### Access MongoDB Shell

```bash
docker exec -it <mongodb_container_name> bash
mongosh
```

### View Databases and Collections

```js
show dbs
use <database_name>
show collections
```

---

## ❌ Cleanup

### Stop & Remove Containers

```bash
docker compose down
```

### Terminate EC2 & Related Resources

- Delete EC2 instance
- Remove security group, key pair, etc.

---

## 🙌 Summary

This deployment gave me real-world experience with:

- Docker multi-container orchestration
- AWS EC2 configuration and security
- Working with MongoDB in containers

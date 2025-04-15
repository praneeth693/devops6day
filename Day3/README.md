# 🏢 College Admission Form App - Docker Deployment

This repository demonstrates the end-to-end deployment of a **College Admission Form Application** using **Docker** and **AWS EC2**. The project involves setting up a multi-container architecture with a frontend and MongoDB backend, all managed via Docker Compose.

---

## 🚀 Project Overview

- **Frontend**: Web interface for admission form
- **Database**: MongoDB for storing form data securely
- **Infrastructure**: Hosted on Ubuntu EC2 instance
- **Containerization**: Docker & Docker Compose

---

## 📆 Steps I Followed

### 1. 🏠 Launched an EC2 Instance

- OS: Ubuntu
- Instance Type: t2.medium
- Storage: 20GB
- Created Key Pair (.ppk format) for PuTTY
- Configured Security Group (opened required TCP ports)

### 2. ⚖️ Connected via PuTTY

- Downloaded and launched PuTTY
- Added host IP and authentication key
- Connected and switched to root user

```bash
sudo -i
```

### 3. ⬆️ Updated the Server

```bash
apt update -y
```

---

## 💾 Cloned the Repository

```bash
git clone https://github.com/Davidgit526/DataDogCasestudy.git
cd DataDogCasestudy
```

---

## 🧰 Installed Docker and Docker Compose

### Add Docker GPG Key and Repo

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

### Install Docker Engine & Compose

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Verify Docker Installation

```bash
docker --version
```

If Docker is inactive:

```bash
service docker restart
```

---

## 🏠 Deploying the Application

### Run Docker Compose

```bash
docker compose up -d
```

- This starts both the frontend and MongoDB containers.
- Ensure TCP ports or specific app port are allowed in EC2 security group.

---

## 🔍 Access the App

```bash
http://<EC2-Public-IP>:<App-Port>
```

> Example: `http://13.234.56.78:3000`

---

## 📉 Manage Containers

### Stop and Remove Containers

```bash
docker compose down
```

---

## ❌ Clean-Up

After testing:

- Delete EC2 instance
- Remove associated resources (EBS, security group, key pair)

---

## 🙌 Conclusion

This deployment project helped me learn:

- Dockerizing multi-container apps
- Using Docker Compose efficiently
- Deploying on EC2 and managing infrastructure

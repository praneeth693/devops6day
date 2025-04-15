# 🛒 Retail App Kubernetes Deployment via Jenkins

This project showcases how I deployed a **Retail App** onto an **EKS Kubernetes cluster** using a fully automated **CI/CD pipeline** built in **Jenkins**.

---

## 🏠 Infrastructure Overview

### EC2 Setup for Kubernetes Master

- OS: Ubuntu
- Instance Type: `t2.medium`
- Storage: 30 GB

### Tools Installed:

- **eksctl** (for creating EKS cluster)
- **kubectl** (to manage Kubernetes)
- **AWS CLI** (to authenticate and configure IAM)

### IAM Setup

- Created an IAM user with `AdministratorAccess` policy
- Generated and configured AWS Access Key and Secret on EC2

```bash
aws configure
```

---

## 🌐 EKS Cluster Setup

Created the EKS Cluster using the following command:

```bash
eksctl create cluster \
  --name retail-cluster \
  --region <your-region> \
  --zones <availability-zones> \
  --nodegroup-name retail-nodes \
  --node-type t2.medium \
  --nodes 2
```

---

## 💪 Jenkins Server Setup

### EC2 Instance

- OS: Ubuntu
- Instance Type: `t2.medium`
- Storage: 25 GB

### Jenkins Installation

```bash
apt update -y
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update
sudo apt-get install jenkins
```

### Java Installation

```bash
sudo apt install fontconfig openjdk-17-jre
```

### Start Jenkins

```bash
sudo systemctl enable jenkins
sudo systemctl start jenkins
```

### Open Jenkins

- Access via: `http://<EC2-PUBLIC-IP>:8080`
- Open port 8080 in Security Group

---

## 🧰 Kubeconfig Setup in Jenkins

On Jenkins server:

```bash
aws eks update-kubeconfig --name retail-cluster --region <your-region>
```

```bash
sudo mkdir -p /home/jenkins/.kube
sudo cp /root/.kube/config /home/jenkins/.kube/config
sudo chown -R jenkins:jenkins /home/jenkins/.kube
```

Set AWS credentials on Jenkins user:

```bash
sudo su - jenkins
aws configure
```

---

## 🔧 Jenkins Configuration

### Plugins Installed

- AWS Credentials
- Kubernetes CLI
- Kubernetes :: Pipeline :: DevOps Steps

### Credentials Setup

- AWS credentials (access key + secret)
- Kubeconfig token (copy from `/root/.kube/config`)
- DockerHub credentials

---

## 📝 Jenkins Pipeline Script

```groovy
pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git 'https://github.com/Msocial123/Retail-App_kubernetes.git'
            }
        }

        stage('Docker Build, Tag, Push') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred') {
                        sh 'docker build -t retail-app-1 .'
                        sh 'docker tag retail-app-1 muralisocial123/retail-app-1:latest'
                        sh 'docker push muralisocial123/retail-app-1:latest'
                        sh 'docker run -d --name retail-app -p 80:80 retail-app-1:latest'
                        sh 'docker compose up -d'
                    }
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                script {
                    withKubeConfig(credentialsId: 'k8s-token') {
                        sh 'kubectl apply -f mongodb-deployment.yml'
                        sh 'kubectl apply -f mongodb-service.yml'
                        sh 'kubectl apply -f userprofile-deployment.yml'
                        sh 'kubectl apply -f usernode-js-service.yml'
                    }
                }
            }
        }
    }
}
```

---

## 🚧 Pre-Deployment Cleanup

```bash
sudo chown -R jenkins:jenkins /var/lib/jenkins/workspace/Retail-app
sudo chmod -R 777 /var/lib/jenkins/workspace/Retail-app
sudo rm -rf /var/lib/jenkins/workspace/Retail-app/data
```

---

## 🚀 Final Deployment

- Saved pipeline and clicked **Build Now**
- Verified deployment on EKS via `kubectl get pods` and `kubectl get services`
- Application deployed successfully and accessible via LoadBalancer IP

---

## 🙌 Outcome

- Fully automated Jenkins CI/CD pipeline
- Built, pushed, and deployed Docker containers
- Successfully deployed Retail App on AWS EKS

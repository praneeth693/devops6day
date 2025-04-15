# 🌐 Kubernetes Deployment - Microservices on Cloud

This README showcases how I deployed microservices on Kubernetes using both CLI and GUI tools. I leveraged Kubernetes clusters on managed cloud services like **GKE**, **EKS**, and **AKS** with core deployment and scaling capabilities using **kubectl** and **GCP Workload GUI**.

---

## 🚀 Project Highlights

- Deployed Spring Boot REST API on Kubernetes
- Used Docker container images via DockerHub
- Scaled deployments using ReplicaSets
- Achieved zero-downtime upgrades using Deployment strategies
- Exposed services using LoadBalancer

---

## 🤝 Cloud Platforms Used

- **Google Kubernetes Engine (GKE)**
- **Elastic Kubernetes Service (EKS)**
- **Azure Kubernetes Service (AKS)**

Managed services made cluster provisioning, scaling, and monitoring much easier.

---

## 🏠 Kubernetes Architecture

### Master Node Components:

- **etcd**: Distributed database storing all cluster data
- **kube-apiserver**: Frontend for Kubernetes control plane
- **kube-scheduler**: Schedules pods to nodes based on resource availability
- **kube-controller-manager**: Monitors and enforces desired cluster state

### Worker Node Components:

- **kubelet**: Reports node status and ensures container health
- **kube-proxy**: Manages pod-to-service networking
- **Container Runtime**: Docker (OCI-compliant)

---

## 📆 Creating a Deployment

```bash
# Create a deployment from DockerHub image
kubectl create deployment hello-world-rest-api \
  --image=muralisocial123/hello-world-rest-api:0.0.1.RELEASE

# Expose the deployment using LoadBalancer
kubectl expose deployment hello-world-rest-api \
  --type=LoadBalancer --port=8080
```

---

## 🤸️ Pods & ReplicaSets

- **Pod**: Smallest deployable unit; wraps around one or more containers.
- **ReplicaSet**: Ensures the desired number of pods are always running.

```bash
# View current pods
kubectl get pods -o wide

# Scale to 3 pods
kubectl scale deployment hello-world-rest-api --replicas=3

# Verify
kubectl get replicaset
kubectl get events --sort-by=.metadata.creationTimestamp
```

---

## 🏛️ Deployment Strategies

Used **Rolling Updates** for version upgrades with zero downtime:

```bash
# Upgrade to new image version
kubectl set image deployment hello-world-rest-api \
  hello-world-rest-api=muralisocial123/hello-world-rest-api:0.0.2.RELEASE
```

- Upgraded pods one by one
- No downtime for users

---

## 🔗 Exposing Services

```bash
# Get all services and their external IPs
kubectl get services
```

- Kubernetes service ensures stable endpoint even if pods are recreated.
- GCP LoadBalancer handles pod IP mapping.

---

## 📊 GCP Workload UI

### Actions:

- Expose
- Rolling Update
- Auto Scaling
- Manual Scaling

### Edit YAML:

- Modify deployment or service YAML on-the-fly

---

## 🛠️ Setup Tools

### Install Google Cloud SDK

- [GCloud Install Docs](https://cloud.google.com/sdk/docs/install)

### Install kubectl

- [kubectl Install Docs](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/)

---

## 🙌 Key Takeaways

- Gained hands-on with full lifecycle of app deployment on Kubernetes
- Practiced CLI (`kubectl`) and GUI (GCP Workloads)
- Understood the architecture behind resilient cloud-native deployments

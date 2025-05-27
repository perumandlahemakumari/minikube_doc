
# Kubernetes Minikube Setup and Pod Management

This document guides you through setting up Minikube on a Linux system, creating and managing Kubernetes pods using `kubectl`, and working with YAML configurations.

## 🚀 Minikube Setup

# 🖥️ AWS EC2 Setup Guide

This guide explains how to launch a new EC2 instance on AWS with the specified configuration.

## 📌 EC2 Instance Configuration

- **Instance Type:** `t2.medium`
- **Operating System:** Ubuntu Server 22.04 LTS
- **Storage:** 25 GB (General Purpose SSD recommended)

Create and run the installation script:

```bash
vi minikube.sh
sh minikube.sh
```

### 📜 `minikube.sh` Script Content

```bash
apt update -y
sudo apt install curl wget apt-transport-https -y
sudo curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo mv minikube-linux-amd64 /usr/local/bin/minikube
sudo chmod +x /usr/local/bin/minikube
sudo minikube version
sudo curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
sudo echo "$(cat kubectl.sha256) kubectl" | sha256sum --check
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
sudo minikube start --driver=docker --force
```

Check Minikube status:

```bash
minikube status
```

## 🧪 Pod Operations

### Create a pod using an image:

```bash
kubectl run pod-1 --image=nginx
kubectl get pods
```

### Using YAML to create Pods

Create `pod.yml`:

```yaml
---
apiVersion: v1
kind: Pod
metadata:
  name: pod1
spec:
  containers:
   - name: cont1
     image: nginx
     ports:
      - containerPort: 80
```

Apply the YAML:

```bash
kubectl create -f pod.yml
```

### `hema.yml` Example

```yaml
---
apiVersion: v1
kind: Pod
metadata:
  name: pod3
  labels:
    course: devops
spec:
  containers:
   - name: cont1
     image: httpd
     ports:
      - containerPort: 80
```

### Manage Pods

```bash
kubectl get po
kubectl api-resources
kubectl get pod -o wide
kubectl describe pod pod1
kubectl describe pod pod2
kubectl describe po -o yaml
kubectl exec -it pod2 -- /bin/bash
kubectl logs pod1 -c cont1
kubectl get po --show-labels
kubectl get po -l course=devops
kubectl get po -l env=dev
kubectl get po -l env!=de
kubectl get po -l 'env in (dev,test)'
kubectl delete pod -l course=devops
kubectl delete pod --all
```

Repeat creation/deletion as needed with updated YAMLs.

## 🔧 Manage Pods with Descriptions

| 🔢 No. | 🧩 Command | 📘 Description |
|------|------------|----------------|
| 1️⃣ | `kubectl get po` | Get a list of all pods. |
| 2️⃣ | `kubectl api-resources` | List all supported API resources in the cluster. |
| 3️⃣ | `kubectl get pod -o wide` | Get detailed pod information including node name, IP, etc. |
| 4️⃣ | `kubectl describe pod pod1` | Show detailed info about `pod1` including events and container states. |
| 5️⃣ | `kubectl describe pod pod2` | Show detailed info about `pod2`. |
| 6️⃣ | `kubectl describe po -o yaml` | Display all pods in YAML format. |
| 7️⃣ | `kubectl exec -it pod2 -- /bin/bash` | Open an interactive shell session in `pod2`. |
| 8️⃣ | `kubectl logs pod1 -c cont1` | View logs for container `cont1` in `pod1`. |
| 9️⃣ | `kubectl get po --show-labels` | Show pods with their associated labels. |
| 🔟 | `kubectl get po -l course=devops` | List pods with label `course=devops`. |
| 1️⃣1️⃣ | `kubectl get po -l env=dev` | List pods with label `env=dev`. |
| 1️⃣2️⃣ | `kubectl get po -l env!=de` | List pods with label `env` not equal to `de`. |
| 1️⃣3️⃣ | `kubectl get po -l 'env in (dev,test)'` | List pods where `env` is either `dev` or `test`. |
| 1️⃣4️⃣ | `kubectl delete pod -l course=devops` | Delete all pods with label `course=devops`. |
| 1️⃣5️⃣ | `kubectl delete pod --all` | Delete all pods in the current namespace. |

# 🚀 Kubernetes CRD Demo

A hands-on demonstration of creating and deploying a **Custom Resource Definition (CRD)** on Kubernetes using **Minikube** and **Amazon Linux EC2**.  
This project showcases how Kubernetes APIs can be extended using CRDs to define and manage custom resources for real-world platform automation.

---

## 📘 Project Overview

This project defines a **custom Kubernetes resource** called `MyPlatform`, which allows you to create, configure, and manage platform-specific workloads declaratively — just like built-in Kubernetes resources such as Deployments or Services.

You’ll learn how to:
- Create and register a **Custom Resource Definition (CRD)**
- Define custom fields and schemas for the CRD
- Deploy a sample **Custom Resource (CR)** to test the CRD
- Run everything locally using **Minikube** on an **Amazon Linux EC2 instance**

---

## 🏗️ Tech Stack

| Tool | Purpose |
|------|----------|
| **Kubernetes** | Cluster orchestration |
| **Minikube** | Local Kubernetes cluster |
| **Docker** | Container runtime for Minikube |
| **kubectl** | Kubernetes CLI |
| **Amazon Linux EC2** | Host environment |
| **YAML** | CRD and resource configuration |

---

## ⚙️ Prerequisites

Before you begin, ensure you have:
- An **AWS EC2 instance** running **Amazon Linux 2**
- **Root access** or `sudo` privileges
- Basic understanding of Kubernetes YAML manifests

---

## 🪜 Step 1: Install and Configure Minikube on EC2
``` bash
# Update packages
sudo yum update -y

# Install Docker
sudo amazon-linux-extras install docker -y
sudo systemctl start docker
sudo systemctl enable docker

# Install conntrack and Minikube
sudo yum install conntrack -y
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# Start Minikube
sudo minikube start --force --driver=docker
```

## Step 2: Install Git and Kubectl
``` bash
# Install Git
sudo yum install git -y

# Install kubectl
curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.20.4/2021-04-12/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl

# Verify
kubectl version --short --client
```
## Step 3: Clone the Repository
``` bash
git clone https://github.com/satheesh-kamadani/kubernetes-crd-demo.git
cd kubernetes-crd-demo
```

## Step 4: Deploy the CRD and Custom Resource
``` bash
# Apply the CRD
kubectl apply -f custom_resource_definition.yml

# Verify CRD registration
kubectl api-resources | grep myplatform

# Apply the custom resource
kubectl apply -f custom_resource.yml

# View custom resource
kubectl get myp
```
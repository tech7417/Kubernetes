# 📌 **Kubernetes Setup & Interview Guide**

## **📖 Table of Contents**
1. Introduction
2. Kubernetes Basics
3. Local Setup using Minikube
4. Essential Kubernetes Commands
5. Kubernetes Architecture & Concepts
6. Interview Questions
7. Additional Resources

---

## **1️⃣ Introduction**
### ❓ **Why Learn Kubernetes?**
✅ **A:** Kubernetes is the industry-standard container orchestration platform, widely used in production environments to manage containerized applications efficiently.

### ❓ **Who Uses Kubernetes?**
✅ **A:** Major tech companies (Google, Amazon, Microsoft, etc.), startups, and enterprises that deploy microservices architectures.

---

## **2️⃣ Kubernetes Basics**
- **Pods:** The smallest deployable unit in Kubernetes, containing one or more containers.
- **Nodes:** Machines (physical/virtual) that run workloads.
- **Cluster:** A set of nodes managed by Kubernetes.
- **Namespace:** A way to divide cluster resources between multiple users.
- **Services:** Allow communication between different parts of an application.

---

## **3️⃣ Local Setup using Minikube**

### **Step 1: Install Dependencies**
1. **Install Docker**
   ```sh
   sudo apt update
   sudo apt install docker.io -y
   ```
2. **Install kubectl (Kubernetes CLI)**
   ```sh
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
   chmod +x kubectl
   sudo mv kubectl /usr/local/bin/
   ```
3. **Install Minikube**
   ```sh
   curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
   sudo install minikube-linux-amd64 /usr/local/bin/minikube
   ```

### **Step 2: Start Minikube**
```sh
minikube start --driver=docker
```

### **Step 3: Verify Installation**
```sh
kubectl get nodes
```

### **Step 4: Deploy a Sample Application**
```sh
kubectl create deployment hello-node --image=k8s.gcr.io/echoserver:1.4
kubectl expose deployment hello-node --type=NodePort --port=8080
```

### **Step 5: Access the Application**
```sh
minikube service hello-node
```

---

## **4️⃣ Essential Kubernetes Commands**
- **Get cluster info:** `kubectl cluster-info`
- **List nodes:** `kubectl get nodes`
- **List pods:** `kubectl get pods`
- **Describe a pod:** `kubectl describe pod <pod-name>`
- **Delete a pod:** `kubectl delete pod <pod-name>`
- **Deploy an app:** `kubectl apply -f deployment.yaml`

---

## **5️⃣ Kubernetes Architecture & Concepts**
### **Kubernetes Architecture Diagram**
```plaintext
+-----------------+        +-----------------+
|  Master Node   |        |  Worker Node   |
+-----------------+        +-----------------+
| API Server     |        | Kubelet         |
| Controller     |        | Container Runtime |
| Scheduler      |        | Pods            |
+-----------------+        +-----------------+
```

### **Components of Kubernetes**
- **Master Node:** Controls the cluster, runs the API server, scheduler, and controllers.
- **Worker Nodes:** Execute applications inside pods.
- **Kubelet:** Manages the lifecycle of pods on each node.
- **Kube Proxy:** Handles networking between pods and external services.

---

## **6️⃣ Interview Questions**

### **Basic Questions:**
1. What is Kubernetes, and why is it used?
2. Explain the difference between Pods and Nodes.
3. What are Namespaces in Kubernetes?
4. How does Kubernetes handle networking?

### **Advanced Questions:**
1. How does Kubernetes perform load balancing?
2. What are the different types of services in Kubernetes?
3. Explain the Kubernetes control plane components.
4. How can you scale applications in Kubernetes?
5. What is a DaemonSet, and when would you use it?

---

## **7️⃣ Additional Resources**
- [Kubernetes Official Documentation](https://kubernetes.io/docs/)
- [Minikube Setup Guide](https://minikube.sigs.k8s.io/docs/start/)
- [CKA Certification Study Guide](https://training.linuxfoundation.org/certification/certified-kubernetes-administrator-cka/)

🚀 **Follow this guide to master Kubernetes from beginner to advanced levels!**


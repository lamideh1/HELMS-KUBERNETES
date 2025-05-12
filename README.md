# HELMS-KUBERNETES
Great! You're working on a **mini project to deploy a web application using Helm in Kubernetes**. Let’s break this down **step-by-step**, assuming you're using **Windows** and **VS Code** as instructed.

---

### **Step-by-Step Guide to Deploying a Web App Using Helm on Kubernetes**

---

## **PHASE 1: Set Up Your Environment**

### **1. Open VS Code as Administrator**

* Right-click on VS Code → Run as administrator.

### **2. Open Terminal in VS Code**

* `Terminal` → `New Terminal`

---

### **3. Install Helm via Chocolatey**

(If you don’t have Chocolatey installed, [install it from here](https://chocolatey.org/install))

```powershell
choco install kubernetes-helm
```

### **4. Verify Helm Installation**

```bash
helm version
```

---

## **PHASE 2: Create Your Helm Chart Project**

### **1. Create Your Project Folder**

```bash
mkdir helm-web-app
cd helm-web-app
```

### **2. Scaffold a New Helm Chart**

```bash
helm create webapp
```

This creates a folder called `webapp/` with all the necessary chart structure:

```
webapp/
├── charts/
├── templates/
├── values.yaml
├── Chart.yaml
```

---

## **PHASE 3: Initialize Git Repository**

### **1. Initialize Git and Commit**

```bash
git init
git add .
git commit -m "Initial Helm webapp chart"
```

---

### **2. Push to Remote Repository**

Go to GitHub and:

* Create a new repository (e.g., `helm-webapp`)
* Follow GitHub instructions:

```bash
git remote add origin https://github.com/your-username/helm-webapp.git
git branch -M main
git push -u origin main
```

---

## **PHASE 4: Deploy the Helm Chart to Kubernetes**

> Prerequisites:
>
> * A running Kubernetes cluster (local: Minikube / remote: EKS, GKE, etc.)
> * `kubectl` configured and connected to the cluster.

### **1. Check Cluster Connection**

```bash
kubectl get nodes
```

### **2. Install Your Chart**

Navigate to the parent directory (outside `webapp/`):

```bash
helm install my-webapp ./webapp
```

> Replace `my-webapp` with any release name of your choice.

---

### **3. Verify Deployment**

```bash
kubectl get all
```

---

### **4. Access the App**

If it's a NodePort service (default from Helm template):

```bash
kubectl get svc
```

Then open your browser with:

```
http://<NODE-IP>:<NODE-PORT>
```

> Use `minikube service my-webapp` if using Minikube, to open directly.

---

## **PHASE 5: Optional Customization**

* Edit `values.yaml` to configure app name, image, port, etc.
* Modify templates in `/templates/deployment.yaml` or `/templates/service.yaml` for more control.

---

## **What’s Next?**

* Add Ingress support to expose the app via DNS.
* Deploy to a cloud provider (e.g., AWS EKS).
* Automate deployment via CI/CD tools (GitHub Actions, Jenkins, etc.).

---

Would you like me to walk you through **customizing your `values.yaml`**, **creating a basic web app container**, or **adding Ingress for external access**?

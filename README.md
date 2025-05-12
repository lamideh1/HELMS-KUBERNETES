Great — let’s **start from the beginning** and go step by step to properly **deploy a web application using Helm in Kubernetes**, **meet your project requirements**, and **fully align with the instructor's expectations**.

---

## 🧠 **Overview**

You'll be deploying a basic NGINX web application using Helm on Kubernetes. Helm helps package and manage Kubernetes manifests using charts.

---

## 🧰 **Step-by-Step Breakdown**

---

### 🟨 **Step 1: Prerequisites**

Before starting, make sure you have:

| Tool               | Required                                      |
| ------------------ | --------------------------------------------- |
| Kubernetes Cluster | ✅ (e.g., Minikube, Docker Desktop, EKS, etc.) |
| kubectl CLI        | ✅                                             |
| Helm CLI           | ✅                                             |
| Git Installed      | ✅                                             |
| GitHub Account     | ✅                                             |

---

### 🟦 **Step 2: Install Helm**

#### 🪟 For **Windows** (PowerShell with Admin rights):

```powershell
choco install kubernetes-helm
```

> 🔍 Verify:

```powershell
helm version
```

If you’re **not using Chocolatey**, install manually via [Helm Releases](https://github.com/helm/helm/releases).

---

### 🟩 **Step 3: Create Helm Chart**

Create a new directory and initialize a Helm chart:

```bash
mkdir helm-web-app
cd helm-web-app
helm create webapp
```

This creates a folder called `webapp` with a sample Helm chart.

---

### 🟪 **Step 4: Customize Helm Chart Files**

You'll modify:

* `Chart.yaml`: Metadata
* `values.yaml`: Config values
* `templates/deployment.yaml`: Pod spec
* `templates/service.yaml`: Service definition

---

#### ✏️ 1. Edit `Chart.yaml`

```yaml
apiVersion: v2
name: webapp
description: A simple NGINX Helm chart
version: 0.1.0
appVersion: "1.0"
```

---

#### ✏️ 2. Edit `values.yaml`

This is your config for the app.

```yaml
replicaCount: 2

image:
  repository: nginx
  pullPolicy: IfNotPresent
  tag: latest

service:
  type: NodePort
  port: 80
  nodePort: 30080

resources:
  limits:
    cpu: 200m
    memory: 256Mi
  requests:
    cpu: 100m
    memory: 128Mi

ingress:
  enabled: false
```

---

#### ✏️ 3. Edit `templates/deployment.yaml`

Make sure these lines use your `values.yaml` settings:

```yaml
spec:
  replicas: {{ .Values.replicaCount }}
  containers:
    - name: nginx
      image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}"
      ports:
        - containerPort: 80
      resources:
        limits:
          memory: {{ .Values.resources.limits.memory }}
          cpu: {{ .Values.resources.limits.cpu }}
        requests:
          memory: {{ .Values.resources.requests.memory }}
          cpu: {{ .Values.resources.requests.cpu }}
```

---

#### ✏️ 4. Edit `templates/service.yaml`

Make sure the NodePort is defined:

```yaml
spec:
  type: {{ .Values.service.type }}
  ports:
    - port: {{ .Values.service.port }}
      targetPort: 80
      nodePort: {{ .Values.service.nodePort }}
```

---

### 🟥 **Step 5: Deploy Using Helm**

First, make sure your cluster is running. Then:

```bash
kubectl config current-context      # confirm context
helm install my-webapp ./webapp
```

> 🔍 Verify resources:

```bash
kubectl get all
kubectl get svc
```

---

### 🟧 **Step 6: Test the Web App**

Get the IP of your Kubernetes node:

```bash
minikube ip   # Or check your cluster IP
```

Then access via browser or curl:

```
http://<NODE-IP>:30080
```

---

### 🟫 **Step 7: Version Control with Git**

Initialize and push to GitHub:

```bash
cd helm-web-app
git init
git add .
git commit -m "Initial Helm webapp chart"
git remote add origin https://github.com/your-username/helm-web-app.git
git push -u origin master
```

---

### 🟦 **Step 8: Cleanup (Optional)**

```bash
helm uninstall my-webapp
kubectl delete all --all
```

---

### ✅ **Optional Enhancements (to impress the instructor)**

1. **Add a CI/CD workflow** (GitHub Actions or Jenkins).
2. **Include a values-production.yaml** file.
3. **Simulate traffic and scale using `kubectl scale` or HPA.**
4. **Document security measures (e.g., RBAC, ServiceAccount).**

---

### 📄 **Documentation to Submit**

Include in your project:

* Explanation of all files edited.
* Screenshot of the deployed service.
* Helm commands used.
* Link to your GitHub repo.
* Troubleshooting steps (if any).

---

Would you like me to generate a sample GitHub README and folder structure for this project?

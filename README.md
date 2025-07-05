# kubernetes-1

# 🚀 My Kubernetes Project: Auto Scaling, Load Balancing & Full App Deployment on AWS

This is a hands-on Kubernetes project I built from scratch, where I:
- ✅ Deployed a containerized application on a custom Kubernetes cluster
- ✅ Set up **Horizontal Pod Autoscaler (HPA)** to handle real-time load
- ✅ Configured **LoadBalancer service** to expose the frontend
- ✅ Used **ClusterIP service** to expose the backend internally
- ✅ Managed the entire infrastructure using **Kops on AWS EC2**
- ✅ Used **AWS S3** to store Kubernetes cluster state
- ✅ Verified the app with a working **web interface**

---

## 🧰 Tools & Technologies I Used

- **AWS EC2** for master and worker nodes
- **Kops** to create and manage the Kubernetes cluster
- **kubectl** to apply and manage resources
- **Docker** for app containerization
- **HPA** for auto scaling
- **S3** for storing Kops cluster configs
- **LoadBalancer (ELB)** to expose frontend
- **ClusterIP** for backend service

---

## 📸 Screenshots

You can find all screenshots in the zip file below:
- Deployment and service creation via `kubectl`
- EC2 instances running the Kubernetes cluster
- S3 bucket setup for Kops
- App exposed via LoadBalancer
- Web UI working output (Reverse and Summation)
- Autoscaler and scaling in action

📁 [Download Project Screenshots](./Kubernetes_Project_Screenshots.zip)

---

## 🧪 How I Deployed It

1. **Created an S3 bucket to store cluster state:**
   ```bash
   aws s3api create-bucket --bucket july-03-maruf --region us-east-1
   export KOPS_STATE_STORE=s3://july-03-maruf
   ```

2. **Used Kops to create the cluster:**
   ```bash
   kops create cluster --name=feb-23.k8s.local --zones=us-east-1b \
     --node-count=2 --node-size=t2.medium --master-size=t2.medium
   kops update cluster --name feb-23.k8s.local --yes
   ```

3. **Deployed backend and frontend using YAML:**
   ```bash
   kubectl apply -f namespace.yaml
   kubectl apply -f backend-deployment.yaml
   kubectl apply -f backend-service.yaml
   kubectl apply -f frontend-deployment.yaml
   kubectl apply -f frontend-service.yaml
   ```

4. **Exposed frontend with a LoadBalancer:**
   ```bash
   kubectl expose deployment frontend --type=LoadBalancer --port=80 --target-port=3000
   ```

5. **Enabled auto scaling for the backend:**
   ```bash
   kubectl autoscale deployment backend --cpu-percent=50 --min=2 --max=5
   ```

---

## 🌐 Live App Output (Example)

- I tested the app by submitting inputs like `1254` and `1458`  
- The frontend returned correct reverse and summation responses:
  - 1254 → 4521 (Reverse)
  - 1458 → 18 (Sum)

---

## 💡 What I Learned

- How to deploy and manage workloads in Kubernetes using `kubectl`
- How to expose services with LoadBalancer and ClusterIP
- How to scale applications dynamically using HPA
- How to provision clusters using Kops, EC2, and S3

---

## 📂 Files Included

- `namespace.yaml` – Namespace definition
- `backend-deployment.yaml` – Backend deployment
- `backend-service.yaml` – Backend ClusterIP service
- `frontend-deployment.yaml` – Frontend deployment
- `frontend-service.yaml` – Frontend LoadBalancer service
- `Kubernetes_Project_Screenshots.zip` – Visual output of the project

---

## ✅ Status

✅ **Successfully Deployed & Tested!**  
This project helped me gain confidence in deploying real-world Kubernetes workloads in a cloud environment.

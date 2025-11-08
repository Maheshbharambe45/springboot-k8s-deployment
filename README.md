# Deploying a Spring Boot Application on Kubernetes (K8s) using Docker, Minikube, and EC2

## Project Overview
This project demonstrates how to deploy a **Spring Boot application** on a **Kubernetes (K8s) cluster**, ensuring seamless **integration, scalability, and management**.  
![Website Screenshot](assets/Screenshot%202025-11-08%20201112.png)

Inbound rules for security group

 ![Website Screenshot](assets/Screenshot%202025-11-08%20201023.png)

##  Objectives
- Deploy Spring Boot microservice in a **cloud-native environment**.
- Containerize the application using **Docker**.
- Set up and manage a **Kubernetes cluster** using **Minikube**.
- Deploy both **Spring Boot application** and **MySQL database** on Kubernetes.
- Manage and access the application via **Kubernetes services** and **port forwarding**.
- Utilize **Kubernetes Dashboard** for monitoring and management.

## 🏗️ Technologies Used
- AWS EC2 (Amazon Linux 2)
- Docker
- Minikube
- Kubernetes (kubectl)
- Spring Boot
- MySQL Database
- GitHub
- Maven

## ⚙️ Setup and Deployment Steps

### 1️⃣ Update and Install Dependencies
```bash
sudo yum update -y
sudo yum install docker -y
sudo systemctl start docker
sudo systemctl enable docker
```

### 2️⃣ Install Minikube and Kubectl
```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

### 3️⃣ Start Minikube Cluster
```bash
minikube start --driver=docker --force
minikube status
```
 ![Website Screenshot](assets/Screenshot%202025-11-08%20115108.png)

### 4️⃣ Clone the GitHub Repository
```bash
git clone https://github.com/SushantOps/SpringBootOnK8S_PS.git
cd SpringBootOnK8S_PS/
```

### 5️⃣ Deploy MySQL Database on Kubernetes
```bash
kubectl apply -f db-deployment.yaml
kubectl get pods
kubectl exec -it <mysql-pod-name> -- bash
```
 ![Website Screenshot](assets/Screenshot%202025-11-08%20115642.png)

### 6️⃣ Build and Deploy Spring Boot Application
```bash
sudo yum install maven -y
mvn clean package
kubectl apply -f app-deployment.yaml
kubectl get pods
```

### 7️⃣ Expose Services and Access Application
```bash
kubectl get svc
minikube ip
kubectl port-forward --address 0.0.0.0 svc/springboot-crud-svc 8080:8080 &
```
Access your application at: **http://<EC2-Public-IP>:8080**

### 8️⃣ Access Kubernetes Dashboard
```bash
minikube dashboard --url
```
Or through SSH tunneling:
```bash
ssh -i MY-KEY.pem -L 8001:127.0.0.1:<port> ec2-user@<EC2-Public-IP>
```
Then visit:  
**http://127.0.0.1:8001/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/**


## Results
 ![Website Screenshot](assets/Screenshot%202025-11-08%20124900.png)

## 🔗 GitHub Repository
[Visit Project on GitHub](https://github.com/Maheshbharambe45/springboot-k8s-deployment.git)

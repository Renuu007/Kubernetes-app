# Kubernetes-app

[GitHub Repository](https://github.com/Renuu007/Kubernetes-app)

## Overview
This project demonstrates how to deploy and manage a simple application (nginx) on a local Kubernetes cluster using Docker Desktop (with Kubernetes enabled), kind, or kubeadm. You will learn how to create deployments and services using YAML files, scale your application, and troubleshoot common issues.

---

## Cloning the Repository
To get started, first clone this repository to your local machine:
```sh
# Using HTTPS
git clone https://github.com/Renuu007/Kubernetes-app.git
# Or using SSH
git clone git@github.com:Renuu007/Kubernetes-app.git
cd Kubernetes-app
```

---

## Prerequisites
- **Docker Desktop** (with Kubernetes enabled) OR a local Kubernetes cluster via kind/kubeadm
- **kubectl** command-line tool
- **Internet connection** (to pull images from Docker Hub)

---

## Setup Steps

### 1. Enable Kubernetes
- **Docker Desktop:**
  - Go to **Settings > Kubernetes**
  - Enable Kubernetes and select your provisioning method (preferably kind or kubeadm if Docker Desktop's default is not available)
  - Click **Apply & Restart**
- **kind/kubeadm:**
  - Follow the official documentation to create a cluster with 1 node (recommended for this project)

### 2. Verify Cluster
```sh
kubectl version --client
kubectl cluster-info
kubectl get nodes
```

---

## Deploy the Application

### 3. Create `deployment.yaml`
- Use the provided `deployment.yaml` file in this repository.

### 4. Apply the Deployment
```sh
kubectl apply -f deployment.yaml
kubectl get deployments
kubectl get pods
```

---

## Expose the Application

### 5. Create `service.yaml`
- Use the provided `service.yaml` file in this repository.

### 6. Apply the Service
```sh
kubectl apply -f service.yaml
kubectl get services
```

---

## Access the Application

### 7. Port Forwarding (if LoadBalancer external IP is not available)
```sh
kubectl port-forward service/nginx-service 8080:80
```
Then open your browser to [http://localhost:8080](http://localhost:8080)

---

## Scaling the Deployment

### 8. Scale Up/Down
```sh
kubectl scale deployment nginx-deployment --replicas=5
kubectl get pods
kubectl get deployments
```

---

## Monitoring and Troubleshooting

### 9. Check Pod Status and Logs
```sh
kubectl get pods
kubectl describe pods
kubectl logs <pod-name>
```

### 10. Common Issues
- **ImagePullBackOff**: If pods are stuck pulling the image:
  - Ensure your internet connection is active.
  - Try pulling the image manually:
    ```sh
    docker pull nginx:latest
    ```
  - If using kind, load the image:
    ```sh
    kind load docker-image nginx:latest
    ```
  - Try a specific image tag (e.g., `nginx:1.25`) in your YAML.
- **Pods Pending**: Check events:
  ```sh
  kubectl describe pod <pod-name>
  kubectl get events
  ```
- **Service Not Accessible**: Use port-forwarding as shown above.

---

## Clean Up
```sh
kubectl delete -f service.yaml
kubectl delete -f deployment.yaml
```

---

## Deliverables
- `deployment.yaml` and `service.yaml` files (provided in this repository)
- Screenshots of:
  - `kubectl get pods`
  - `kubectl get services`
  - `kubectl get deployments`
  - Application running in browser

---

## References
- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Docker Desktop Kubernetes](https://docs.docker.com/desktop/kubernetes/)
- [kind Documentation](https://kind.sigs.k8s.io/)
- [Your GitHub Repo](https://github.com/Renuu007/Kubernetes-app)

---

## License
This project is for educational purposes.

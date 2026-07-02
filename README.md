# k3s SRE Challenge

## Project Overview

This project demonstrates the automated installation of a single-node k3s Kubernetes cluster using Ansible and the deployment of a "Hello World" Nginx application. The application is deployed using Kubernetes manifests, and a GitHub Actions workflow is configured to validate the deployment pipeline.

---

## Technologies Used

- Ubuntu (WSL)
- Ansible
- k3s (Lightweight Kubernetes)
- Kubernetes
- Nginx
- Git
- GitHub
- GitHub Actions

---

## Project Structure

```
k3s-sre-challenge/
├── ansible/
│   └── install-k3s.yml
├── k8s/
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── configmap.yaml
│   └── index.html
├── .github/
│   └── workflows/
│       └── deploy.yml
└── README.md
```

---

## Part 1 - Install k3s

The k3s installation is automated using an Ansible playbook.

### Features

- Installs the latest stable version of k3s
- Creates a single-node Kubernetes cluster
- Installs required dependencies
- Starts and enables the k3s service
- Verifies the cluster installation

Run the playbook:

```bash
sudo ansible-playbook ansible/install-k3s.yml
```

Verify:

```bash
sudo k3s kubectl get nodes
```

---

## Part 2 - Deploy Hello World Application

The application is deployed using Kubernetes resources.

Resources used:

- Deployment
- Service
- ConfigMap

Deploy the application:

```bash
sudo k3s kubectl apply -f k8s/configmap.yaml
sudo k3s kubectl apply -f k8s/deployment.yaml
sudo k3s kubectl apply -f k8s/service.yaml
```

Verify:

```bash
sudo k3s kubectl get deployments
sudo k3s kubectl get pods
sudo k3s kubectl get svc
```

Access the application:

```
http://<Node-IP>:30080
```

Example:

```
http://172.29.239.192:30080
```

---

## Part 3 - GitHub Actions

GitHub Actions is configured to run automatically whenever code is pushed to the **main** branch.

Pipeline steps:

- Checkout repository
- Install kubectl
- Validate Kubernetes manifest files
- Complete CI pipeline successfully

> **Note:** The k3s cluster for this assignment runs locally in WSL. GitHub-hosted runners cannot directly access a local Kubernetes cluster. In a production environment, a self-hosted GitHub Actions runner or a cloud-hosted Kubernetes cluster would be used for deployment.

---

## Verification

Cluster Status

```bash
sudo k3s kubectl get nodes
```

Pods

```bash
sudo k3s kubectl get pods -A
```

Services

```bash
sudo k3s kubectl get svc
```

---

## Application Output

The deployed application displays:

```
Hello World

Kubernetes Assignment Completed Successfully

Deployed using Kubernetes (k3s)

Automated using Ansible

CI/CD using GitHub Actions
```

---

## Author

**Pravin Kumar**

GitHub: https://github.com/Pravin-coder23
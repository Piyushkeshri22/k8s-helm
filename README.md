# Kubernetes Helm Lab

Hands-on Kubernetes Helm project for learning package management, Helm repositories, Helm charts, values.yaml customization, release management, upgrades, rollbacks, and chart deployment using Minikube.

----

# Objective

Learn how Helm simplifies Kubernetes application deployment by understanding:

* Helm Architecture
* Helm Components
* Helm Repositories
* Helm Charts
* Chart Structure
* values.yaml
* Templates
* Release Management
* Install, Upgrade, and Rollback
* Real-world use cases

---

# What is Helm?

Helm is the package manager for Kubernetes.

It simplifies the deployment and management of Kubernetes applications by packaging Kubernetes manifests into reusable Helm Charts.

Instead of manually creating multiple YAML files, Helm deploys an entire application using a single command.

---

# What Problem Helm Solves

Deploying applications manually often requires multiple Kubernetes manifests such as:

* Deployment
* Service
* ConfigMap
* Secret
* Ingress
* PersistentVolumeClaim
* ServiceAccount

Managing these YAML files becomes difficult as applications grow.

Helm solves this problem by packaging all Kubernetes resources into reusable Helm Charts.

---

# Why Helm is Needed

Without Helm:

* Multiple YAML files
* Manual updates
* Difficult version management
* No rollback capability
* Repetitive deployments

With Helm:

* One command deployment
* Versioned releases
* Easy upgrades
* Easy rollbacks
* Reusable templates
* Environment-specific configurations

---

# Helm Architecture

```text
                Developer
                     │
                     ▼
              Helm CLI (Client)
                     │
                     ▼
          Helm Repository (Charts)
                     │
                     ▼
             Download Helm Chart
                     │
                     ▼
          Render Templates using values.yaml
                     │
                     ▼
           Kubernetes API Server
                     │
                     ▼
        Pods, Services, ConfigMaps,
      Secrets, Deployments, PVCs...
```

---

# Helm Components

## Helm CLI

Used to install, upgrade, rollback, and manage Helm releases.

Examples:

```bash
helm install

helm upgrade

helm rollback

helm uninstall
```

---

## Helm Repository

A Helm Repository stores Helm Charts.

Popular repositories:

* Bitnami
* Prometheus Community
* Grafana
* Jetstack
* NGINX

Example:

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```

---

## Helm Chart

A Helm Chart is a package containing Kubernetes resource templates and configuration.

A chart includes:

* Chart.yaml
* values.yaml
* templates/
* charts/

---

## Helm Release

A Release is a running instance of a Helm Chart inside a Kubernetes cluster.

Example:

```bash
helm install my-nginx bitnami/nginx
```

* Chart: bitnami/nginx
* Release: my-nginx

---

# Helm Chart Structure

```text
my-chart/
│
├── Chart.yaml
├── values.yaml
├── charts/
└── templates/
    ├── deployment.yaml
    ├── service.yaml
    ├── ingress.yaml
    ├── _helpers.tpl
    └── NOTES.txt
```

---

# Chart.yaml

Contains chart metadata.

Example:

```yaml
apiVersion: v2
name: nginx
description: NGINX Helm Chart
version: 1.0.0
appVersion: "1.31.2"
```

---

# values.yaml

Contains default configuration values used by Helm templates.

Example:

```yaml
replicaCount: 3

service:
  type: NodePort

image:
  debug: true
```

---

# Templates

Templates generate Kubernetes manifests dynamically.

Examples:

* Deployment
* Service
* ConfigMap
* Secret
* Ingress

Helm replaces template variables using values from `values.yaml`.

---

# Prerequisites

* Docker Desktop
* Minikube
* kubectl
* Helm

Verify installation:

```bash
kubectl get nodes

helm version
```

---

# Repository Structure

```text
k8s-helm/
├── README.md
├── values.yaml
└── .gitignore
```

---

# Install Helm Repository

Add Bitnami repository:

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```

Verify:

```bash
helm repo list
```

Update repository:

```bash
helm repo update
```

---

# Search Helm Charts

Search available charts:

```bash
helm search repo
```

Search NGINX:

```bash
helm search repo nginx
```

---

# View Chart Information

```bash
helm show chart bitnami/nginx
```

View default values:

```bash
helm show values bitnami/nginx
```

---

# Install Helm Chart

```bash
helm install my-nginx bitnami/nginx
```

Verify:

```bash
helm list

kubectl get all
```

---

# Check Helm Release

```bash
helm status my-nginx

helm history my-nginx

helm get values my-nginx

helm get manifest my-nginx
```

---

# Upgrade Release

Create a custom values file.

Example:

```yaml
replicaCount: 3

service:
  type: NodePort

image:
  debug: true
```

Upgrade:

```bash
helm upgrade my-nginx bitnami/nginx -f values.yaml
```

Verify:

```bash
helm history my-nginx

kubectl get deployment

kubectl get pods

kubectl get svc
```

---

# Rollback Release

View history:

```bash
helm history my-nginx
```

Rollback:

```bash
helm rollback my-nginx 1
```

Verify:

```bash
helm history my-nginx

kubectl get deployment

kubectl get svc
```

---

# Common Helm Commands

```bash
helm version

helm repo list

helm repo update

helm search repo nginx

helm show chart bitnami/nginx

helm show values bitnami/nginx

helm install

helm list

helm status

helm history

helm get values

helm get manifest

helm upgrade

helm rollback

helm uninstall
```

---

# Real-World Use Cases

Helm is commonly used to deploy:

* NGINX
* Prometheus
* Grafana
* Jenkins
* MySQL
* PostgreSQL
* MongoDB
* Redis
* Kafka
* Elasticsearch
* RabbitMQ
* Argo CD
* Cert-Manager

---

# Interview Questions

1. What is Helm?
2. Why is Helm called the package manager for Kubernetes?
3. What problem does Helm solve?
4. What is a Helm Chart?
5. What is a Helm Repository?
6. What is a Helm Release?
7. Difference between Chart and Release?
8. What is values.yaml?
9. What are Helm templates?
10. Explain the Helm upgrade process.
11. Explain Helm rollback.
12. Difference between `helm install` and `helm upgrade`.
13. What is `helm history`?
14. What is `helm get manifest`?
15. Name some popular Helm repositories.

---

# Helm Workflow

```text
Developer
      │
      ▼
Helm CLI
      │
      ▼
Helm Repository
      │
      ▼
Download Chart
      │
      ▼
Apply values.yaml
      │
      ▼
Render Templates
      │
      ▼
Generate Kubernetes Manifests
      │
      ▼
Deploy Resources to Kubernetes
```

---

# Key Takeaways

* Helm is the package manager for Kubernetes.
* Helm uses Charts to package Kubernetes applications.
* Helm Repositories store Helm Charts.
* values.yaml customizes deployments.
* Helm Releases manage deployed applications.
* Helm supports upgrades and rollbacks.
* Helm simplifies Kubernetes application lifecycle management.

---

# Cleanup

Uninstall the release:

```bash
helm uninstall my-nginx
```

Verify:

```bash
helm list

kubectl get all
```

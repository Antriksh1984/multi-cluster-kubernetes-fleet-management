# Multi-Cluster Kubernetes Fleet Management

## Overview

This project demonstrates a production-style multi-cluster Kubernetes architecture on Microsoft Azure using GitOps principles. It includes multiple Azure Kubernetes Service (AKS) clusters deployed across regions, centralized application management using Argo CD, and observability through Prometheus and Grafana.

The system enables consistent application deployment across clusters, centralized control, and real-time monitoring.

---

## Architecture

The architecture consists of the following layers:

* User Layer: Clients accessing the application via public endpoints
* Networking Layer: Azure Load Balancer exposing services
* Compute Layer: Multiple AKS clusters across regions
* GitOps Layer: Argo CD connected to a GitHub repository
* Container Registry: Azure Container Registry (ACR)
* Observability Layer: Prometheus and Grafana

### High-Level Flow

* Users access applications through Azure Load Balancer
* Applications are deployed on multiple AKS clusters
* Argo CD pulls manifests from GitHub and deploys to clusters
* AKS clusters pull container images from ACR
* Prometheus collects metrics from clusters
* Grafana visualizes metrics via dashboards

---

## Technologies Used

### Azure Services

* Azure Kubernetes Service (AKS)
* Azure Container Registry (ACR)
* Azure Load Balancer
* Azure Fleet (optional for cluster grouping)

### Kubernetes Components

* Deployments
* Services (ClusterIP and LoadBalancer)
* Namespaces
* Secrets

### GitOps

* Argo CD

### Observability

* Prometheus
* Grafana

---

## Cluster Setup

Two AKS clusters were created in different regions:

* AKS Cluster 1: East US
* AKS Cluster 2: West US (Control Plane Cluster)

Argo CD is installed on the control plane cluster and manages deployments across both clusters.

---

## Application

The application used is a sample voting app consisting of:

* Frontend (web UI)
* Backend (API)
* Redis (data store)

It is deployed across both clusters.

---

## GitOps Workflow

The system follows a GitOps model:

1. Application manifests are stored in a GitHub repository
2. Argo CD monitors the repository
3. Changes in Git trigger automatic deployments
4. Applications are synchronized across clusters

---

## Observability

Prometheus and Grafana are used to monitor cluster and application health.

### Prometheus

* Collects metrics from nodes, pods, and Kubernetes components

### Grafana

* Provides dashboards for:

  * Cluster performance
  * Pod resource usage
  * Application health

---

## Key Features

* Multi-region Kubernetes deployment
* Centralized GitOps-based management
* Automated synchronization of applications
* Real-time monitoring and visualization
* Scalable and production-oriented architecture

---

## Project Structure

```
.
├── k8s/
│   └── azure-vote/
├── manifests/
├── monitoring/
├── argocd/
└── README.md
```

---

## Setup Steps (Summary)

1. Create AKS clusters in multiple regions
2. Attach Azure Container Registry
3. Deploy sample application manually (initial step)
4. Install Argo CD on control cluster
5. Expose Argo CD via LoadBalancer
6. Connect Argo CD to GitHub repository
7. Register additional clusters with Argo CD
8. Deploy applications using GitOps
9. Install Prometheus and Grafana using Helm

---

## Future Improvements

* Automate deployments using CI/CD pipelines
* Enable auto-sync and rollback in Argo CD
* Implement centralized multi-cluster monitoring
* Add alerting using Alertmanager
* Secure access using RBAC and Azure AD

---

## Credits

This project was inspired by and built with reference to the following resources:

* https://github.com/mzazon/cloud-projects/blob/main/azure/multi-cluster-kubernetes-fleet-management-gitops/multi-cluster-kubernetes-fleet-management-gitops.md
* https://github.com/Azure-Samples/azure-voting-app-redis

---

## License

This project is for educational and demonstration purposes.

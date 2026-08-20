# E-Commerce GitOps Repository

This repository contains the Kubernetes manifests and Argo CD configuration used to deploy the E-Commerce application to Amazon EKS using a GitOps-based continuous delivery approach.

## Architecture

Developer
   |
   v
Application Git Repository
   |
   v
Jenkins CI
   |
   +--> Build
   +--> Unit Tests
   +--> SonarQube
   +--> Trivy Security Scan
   +--> Docker Image Build
   |
   v
Amazon ECR
   |
   v
GitOps Repository
   |
   v
Argo CD
   |
   v
Amazon EKS
   |
   +--> Frontend
   |
   +--> Backend
   |
   +--> Services

## GitOps Workflow

1. Developer pushes application code to GitHub.
2. Jenkins automatically triggers the CI pipeline.
3. Jenkins builds and tests the frontend and backend.
4. SonarQube performs code-quality analysis.
5. Trivy scans the application and container images for vulnerabilities.
6. Jenkins builds Docker images.
7. Docker images are pushed to Amazon ECR.
8. Jenkins updates the image tag in this GitOps repository.
9. The Git change becomes the desired state of the Kubernetes environment.
10. Argo CD detects the Git change.
11. Argo CD synchronizes the changes to Amazon EKS.
12. Kubernetes deploys the new application version.

## Repository Structure

```text
ecommerce-gitops/
│
├── README.md
├── namespace.yaml
│
├── backend/
│   ├── backend-deployment.yaml
│   └── backend-service.yaml
│
├── frontend/
│   ├── frontend-deployment.yaml
│   └── frontend-service.yaml
│
└── argocd/
    └── ecommerce-app.yaml

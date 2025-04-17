# Home Lab Kubernetes Cluster - GitOps with K3s

## Objective
Create a GitOps-managed home lab Kubernetes cluster using K3s on a 3-node Proxmox setup. Leverage ArgoCD for GitOps automation, with a clear separation of responsibilities across master, worker, and storage nodes. 

## Scope
- Provision and configure a multi-node K3s cluster using Terraform
- Automate all provisioning and deployment using ArgoCD and Git
- Use an existing admin VM as the orchestrator for Terraform, kubectl, and ArgoCD
- Implement core services like Traefik and Longhorn through GitOps
- Maintain full Git-backed infrastructure and Kubernetes state

## Architecture Overview

### Proxmox Environment
- 3-node physical Proxmox cluster
- Existing admin Ubuntu VM for provisioning and cluster administration

### Kubernetes Cluster (K3s)
- **3 Control Plane (Master) VMs** – High availability setup
- **3 General Worker VMs** – For apps, ingress, monitoring, etc.
- **3 Storage Worker VMs** – Dedicated to Longhorn volumes

### Tooling
- **Infrastructure as Code**: Terraform (with Proxmox provider)
- **GitOps**: ArgoCD (deployed post-cluster setup)
- **Ingress**: Traefik (deployed via ArgoCD)
- **Storage**: Longhorn (deployed via ArgoCD)
- **Secrets**: TBD (SOPS + Age recommended)

## Guiding Principles
- Everything as Code (infra + app + config)
- Fully automated provisioning
- Git is the single source of truth
- Admin tasks initiated from the designated admin VM

## Out of Scope (initial phase)
- Multi-cluster federation
- On-cluster CI/CD systems (e.g., Jenkins, Tekton)
- External secret management (e.g., HashiCorp Vault)

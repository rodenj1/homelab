# Initial Tasks - K3s GitOps Cluster on Proxmox

## 🧰 Admin VM Setup (Pre-Provisioned)
- [ ] Install and configure `kubectl`
- [ ] Install Terraform
- [ ] Install ArgoCD CLI
- [ ] Configure SSH access to Proxmox and VM templates
- [ ] Ensure access to Git repo for bootstrap

---

## 📦 Terraform - VM Provisioning
- [ ] Create Terraform config for:
  - 3 master (control plane) VMs
  - 3 general-purpose worker VMs
  - 3 Longhorn-dedicated storage VMs
- [ ] Distribute VMs evenly across 3 Proxmox physical hosts
- [ ] Assign static IPs and hostnames
- [ ] Use cloud-init-compatible Ubuntu image
- [ ] Test successful boot and SSH access per VM

---

## ⚙️ K3s Cluster Setup
- [ ] Generate cloud-init or provisioning script to install K3s
  - Master 1: `--cluster-init`
  - Masters 2 & 3: join using cluster token
  - Workers: join with `--server` and token
- [ ] Label nodes appropriately (e.g. `node-role.kubernetes.io/storage=true`)
- [ ] Configure kubeconfig on the admin VM for cluster access
- [ ] Validate control plane HA and node join success

---

## 🚀 ArgoCD Bootstrapping
- [ ] Deploy ArgoCD via manifests or Helm
- [ ] Create ArgoCD `IngressRoute` for web access via Traefik
- [ ] Login and change default password
- [ ] Bootstrap ArgoCD with Git repo:
  - Set up `Application` and `AppProject` for the home-lab cluster
  - Point to `clusters/home-lab/` in Git

---

## 🌐 Core Infrastructure via ArgoCD
- [ ] Deploy Traefik ingress controller
- [ ] Deploy MetalLB with static IP pool
- [ ] Deploy Longhorn:
  - Assign `longhorn` label to storage nodes
  - Taint non-storage nodes (optional) to exclude from storage scheduling
- [ ] Deploy cert-manager for TLS support

---

## 📁 Git Repository Setup
- [ ] Create initial Git structure:

```txt
.
├── bootstrap/
│   └── terraform/
├── clusters/
│   └── home-lab/
│       ├── argocd/
│       ├── infra/
│       └── apps/
└── docs/
    ├── PLANNING.md
    └── TASK.md
```

---

## 🔍 Verification
- [ ] Verify `kubectl get nodes` and cluster status from admin VM
- [ ] Confirm ArgoCD UI is accessible and syncing apps
- [ ] Ensure Traefik ingress works with a test app
- [ ] Confirm Longhorn UI is available and volumes can be created


[![Japanese](https://img.shields.io/badge/Language-Japanese-blue)](README_ja.md)

# Home Lab Kubernetes Manifests (GitOps)

![ArgoCD](https://img.shields.io/badge/GitOps-ArgoCD-orange)
![Kubernetes](https://img.shields.io/badge/Kubernetes-Manifests-blue)
![Helm](https://img.shields.io/badge/Helm-Values-0F1689)

This repository contains the **Kubernetes manifests and Helm values** for applications running on my home lab cluster.
It serves as the **Single Source of Truth (SSOT)** for GitOps workflows managed by **ArgoCD**.

Infrastructure provisioning code (Terraform/Ansible) is located in the [homelab-kubernetes-iac](https://github.com/t0m0h1des-homelab/homelab-kubernetes-iac) repository.

## 📂 Directory Structure

The repository adopts the **App of Apps** pattern to manage multiple applications efficiently.

```text
.
├── apps/                          # Application Configuration (Helm Values)
│   ├── kubernetes-dashboard/      # Dashboard settings
│   │   └── values.yaml
│   ├── cloudflared/               # Cloudflare Tunnel settings
│   └── ...
│
└── argocd/                        # ArgoCD Application Definitions
    ├── bootstrap.yaml             # The Entry Point (App of Apps)
    └── applications/              # Individual Application CRs
        ├── kubernetes-dashboard.yaml
        ├── cloudflared.yaml
        └── ...
````

## 🚀 GitOps Workflow

1.  **Modify:** Update `values.yaml` in the `apps/` directory or add a new Application CR in `argocd/applications/`.
2.  **Commit & Push:** Push changes to the `main` branch.
3.  **Sync:** ArgoCD detects the changes and automatically syncs the cluster state.

## 🛠️ Managed Applications

| Application | Description | Type |
| :--- | :--- | :--- |
| **Kubernetes Dashboard** | Web-based Kubernetes user interface. | Helm (Official) |
| **Cloudflared** | Secure remote access tunnel via Cloudflare. | Helm |
| *(More to come)* | ... | ... |

## 🔗 Related Projects

  * **Infrastructure (IaC):** [homelab-kubernetes-iac](https://www.google.com/url?sa=E&source=gmail&q=https://github.com/t0m0h1des-homelab/homelab-kubernetes-iac)

## 📝 License

This project is licensed under the MIT License.

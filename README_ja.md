[![English](https://img.shields.io/badge/Language-English-blue)](README.md)

# Home Lab Kubernetes Manifests (GitOps)

![ArgoCD](https://img.shields.io/badge/GitOps-ArgoCD-orange)
![Kubernetes](https://img.shields.io/badge/Kubernetes-Manifests-blue)
![Helm](https://img.shields.io/badge/Helm-Values-0F1689)

自宅ラボKubernetesクラスタ上で稼働するアプリケーションの **マニフェストおよびHelm設定値（Values）** を管理するリポジトリ。
**ArgoCD** によるGitOpsワークフローにおける **Single Source of Truth (SSOT)** として機能する。

インフラ構築コード（Terraform/Ansible）は [homelab-kubernetes-iac](https://github.com/t0m0h1des-homelab/homelab-kubernetes-iac) リポジトリにて管理。

## 📂 ディレクトリ構成

**App of Apps** パターンを採用し、アプリケーション設定とArgoCDへの登録定義を分離して管理。

```text
.
├── apps/                          # アプリケーション設定の実体 (Helm Values等)
│   ├── kubernetes-dashboard/      # Dashboard用設定
│   │   └── values.yaml            # 公式チャートへのOverride値
│   ├── cloudflared/               # Cloudflare Tunnel設定
│   └── ...
│
└── argocd/                        # ArgoCDへの登録定義 (Application CR)
    ├── bootstrap.yaml             # エントリーポイント (App of Apps親アプリ)
    └── applications/              # 各アプリケーションの登録マニフェスト
        ├── kubernetes-dashboard.yaml
        ├── cloudflared.yaml
        └── ...
````

## 🚀 GitOps ワークフロー

1.  **変更:** `apps/` ディレクトリ内の `values.yaml` を修正、または `argocd/applications/` に新規アプリ定義を追加。
2.  **プッシュ:** `main` ブランチへコミット＆プッシュ。
3.  **同期:** ArgoCDが変更を検知し、クラスタの状態を自動的に同期（Sync）。

## 🛠️ 管理対象アプリケーション

| アプリケーション | 概要 | 管理形式 |
| :--- | :--- | :--- |
| **Kubernetes Dashboard** | Kubernetesクラスタ管理用Web UI | Helm (Official) |
| **Cloudflared** | Cloudflare Tunnelによるセキュアなリモートアクセス | Helm |
| *(順次追加予定)* | ... | ... |

## 🔗 関連プロジェクト

  * **Infrastructure (IaC):** [homelab-kubernetes-iac](https://www.google.com/url?sa=E&source=gmail&q=https://github.com/t0m0h1des-homelab/homelab-kubernetes-iac)

## 📝 ライセンス

This project is licensed under the MIT License.

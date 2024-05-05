# ArgoCD and Crossplane
Practical implementation of ArgoCD and Crossplane


## Prepare a **Managment Cluster**
- Bootstrap a cluster of your choice, here I'm deploying on a VM on Virtual Box, using Kubeadm
- Install helm, azure-cli and argocd

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh

curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash

helm repo add argo https://argoproj.github.io/argo-helm
helm repo update

helm install argocd argo/argo-cd -n argocd --create-namespace --set configs.params."server.insecure"=true

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
rm argocd-linux-amd64
```

## Deploy Crossplane, AKS and EKS

Checkout the following README.md files: \
[Crossplane](./crossplane/README.md) \
[AKS](./azure/README.md) \
[EKS](./aws/README.md)

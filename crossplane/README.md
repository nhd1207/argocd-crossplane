## Deploy Crossplane

Run the following command to deploy an ArgoCD application 
```bash
cat << EOF | kubectl apply -f - 
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: main
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://github.com/nhd1207/argocd-crossplane.git
    targetRevision: HEAD
    path: crossplane
    directory:
      recurse: false
      include: '*.yaml'
  destination:
    server: "https://kubernetes.default.svc"
    namespace: argocd
  syncPolicy:
    automated: {}
EOF
```

## Result:

![ArgoCD application](./asset/image.png)
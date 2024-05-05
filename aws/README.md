
```bash
kubectl create secret generic aws-secret -n crossplane-system \
    --from-file=creds=./credentials.txt
```


Create an Application
```bash
cat << EOF | kubectl apply -f - 
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: awsresources
  namespace: argocd
spec:
  project: crossplane
  source:
    repoURL: https://github.com/nhd1207/argocd-crossplane.git
    targetRevision: HEAD
    path: aws
    directory:
      recurse: false
      include: '*.yaml'
  destination:
    server: "https://kubernetes.default.svc"
    namespace: crossplane-system
  syncPolicy:
    automated: {}
EOF
```
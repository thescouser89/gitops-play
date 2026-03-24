# Bootstrap
Install argocd
```
kubectl create namespace argocd
kubectl apply -n argocd \
    --server-side \
    --force-conflicts \
    -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Install root argocd-application, which will load the other applications
```
kubectl apply -f argocd-root.yaml
```

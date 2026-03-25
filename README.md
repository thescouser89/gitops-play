# Bootstrap for community
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

# Bootstrap for Openshift
For Openshift, you can install it by running:
```
oc apply -f argocd-openshift-operator.yaml
```

Install root argocd-application, which will load the other applications
```
kubectl apply -f argocd-openshift-root.yaml
```

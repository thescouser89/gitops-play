# Installing argocd first
Install argocd
```
kubectl create namespace argocd
kubectl apply -n argocd \
    --server-side \
    --force-conflicts \
    -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

## Argocd and private git repos
```
argocd repo add https://github.com/your-org/your-repo.git --username <git-username> --password <personal-access-token>

# or

argocd repo add git@github.com:your-org/your-repo.git --ssh-private-key-path ~/.ssh/id_rsa_argocd
```

The same would apply for any 'Application' yaml referring to a private Git helm chart repository

# Bootstrap for community
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
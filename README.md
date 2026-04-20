# Installing argocd first
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

Note that the 'Application' yamls are installed inside the **argocd** namespace.

# Bootstrap for Openshift
Installing argocd on Openshift requires a different instruction to the community.
```
oc apply -f argocd-openshift-operator.yaml
```

Install root argocd-application, which will load the other applications
```
kubectl apply -f argocd-openshift-root.yaml
```
Note that the 'Application' yamls are installed inside the **openshift-gitops** namespace.

## Argocd and private git repos
```
argocd repo add https://github.com/your-org/your-repo.git --username <git-username> --password <personal-access-token>

# or

argocd repo add git@github.com:your-org/your-repo.git --ssh-private-key-path ~/.ssh/id_rsa_argocd
```

The same would apply for any 'Application' yaml referring to a private Git helm chart repository

# Secrets
At some point, in between the creation of Openshift namespaces + operators, and deploying Helm charts, we need
to deploy some secrets for the successful deployment of the Helm Charts.

The secrets (perhaps loaded from external-secrets) are:
- external-secrets 'secret-store' link to the actual external secret server
- quay.io secret to pull images

The service account of the helm application should add the quay.io secret to
itself to give it enough permission to pull the image.

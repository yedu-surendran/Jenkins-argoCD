## Using a Manifest File

You can also create an ArgoCD application by defining it in a manifest file and applying it with kubectl.

Create the Manifest: Save the following content to a file named argocd-demo-app.yaml:

```
vi argocd-demo-app.yaml
```


```
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: first-argocd-demo-app
  namespace: argocd
spec:
  project: default

  source:
    repoURL: https://github.com/NinjaCloud/argoCD.git
    targetRevision: HEAD
    path: development

  destination: 
    server: https://kubernetes.default.svc
    namespace: argocd-demo

  syncPolicy:
    syncOptions:
    - CreateNamespace=true

    automated:
      selfHeal: true
      prune: true
```

Apply the Manifest:

```
kubectl apply -f argocd-demo-app.yaml
```

This command creates an ArgoCD application named first-argocd-demo-app in the argocd namespace, which will sync your Kubernetes manifests from the specified Git repository.


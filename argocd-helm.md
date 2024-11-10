# Lab to deploy applications using helm charts

### create a file test-helm.yaml

```
vi test-helm
```

```
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: wordpress
  namespace: argocd
spec:
  project: default
  source:
    chart: wordpress
    repoURL: https://charts.bitnami.com/bitnami
    targetRevision: 23.1.28
    helm:
      releaseName: wordpress
  destination:
    server: "https://kubernetes.default.svc"
    namespace: default
```

### Apply the file using kubectl

```
kubectl apply -f test-helm.yaml
```

# Cheatsheet

## Kubernetes

### Help

```zsh
kubectl {command} help
```

### API Resources

```zsh
kubectl api-resources -o wide
```

### Show Current Kube Config

```zsh
kubectl config view
```

### Switch Clusters/Context

```zsh
kubectl config use-context {cluster-name}
```

### Namespaces

```zsh
kubectl get ns
kubectl delete ns {ns-name}
```

### Metrics Server

```zsh
kubectl top po
kubectl top po --containers
```

### Logs

```zsh
kubectl logs {pod-name} -c {container-name}
```

### Describe API Object

```zsh
kubectl describe {api-resource} {object-id} -n {namespace}
```

### Pods

```zsh
kubectl get po -n {namespace}
kubectl delete po {pod-name} -n {namespace}
```

### Deployments

```zsh
kubectl get deploy -n {namespace}
kubectl delete deploy {deployment-name} -n {namespace}
```

### ConfigMaps

```zsh
kubectl get cm -n {namespace}
kubectl edit cm {cm-name} -n {namespace}
kubectl delete cm {cm-name} -n {namespace}
```

### Secrets

```zsh
kubectl get secret -n {namespace}
kubectl edit secret {secret-name} -n {namespace}
kubectl delete secret {secret-name} -n {namespace}
```

### Services

```zsh
kubectl get svc -n {namespace}
kubectl delete svc {svc-name} -n {namspace}
```

### Ingresses

```zsh
kubectl get ingress -A
kubectl delete ingress {ingress-name} -n {namespace}
```

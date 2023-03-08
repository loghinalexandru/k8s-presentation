# Kubernetes

## Useful arguments. Applies to all commands

- ```-n or --namespace``` specify a different namespace other than the default one
- ```-A or --all-namespaces``` runs the command on all namespaces

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

### Shell Into Container

```zsh
 kubectl exec -it {pod-name} -c {container-name} -- /bin/sh
```

### Copy From Container

```zsh
kubectl cp {pod-name}:{path-origin} {path-dest} -c {container-name}
```

### Pods

```zsh
kubectl get po
kubectl delete po {pod-name}
```

### Deployments

```zsh
kubectl get deploy
kubectl delete deploy {deployment-name}
```

### ConfigMaps

```zsh
kubectl get cm
kubectl edit cm {cm-name}
kubectl delete cm {cm-name}
```

### Secrets

```zsh
kubectl get secret
kubectl edit secret {secret-name}
kubectl delete secret {secret-name}
```

### Services

```zsh
kubectl get svc
kubectl delete svc {svc-name}
```

### Ingresses

```zsh
kubectl get ingress -A
kubectl delete ingress {ingress-name}
```

### Scale Manually

```zsh
kubectl scale --replicas={pods-number} deploy {deployment-name}
```

<div style="page-break-after: always;"></div>

# Helm

## Show Releases

```zsh
helm list
```

### Create Chart

```zsh
helm create {chart-name}
```

### Install/DryRun

```zsh
helm upgrade --install -f {custom-values.yaml} {release-name} {chart}
helm install {release-name} --set {custom-inline} --dry-run {chart}
```

### Show Default Values

```zsh
helm show values {chart}
```

### Show Release Values

```zsh
helm get values {release-name}
```

### Delete Release

```zsh
helm delete {release-name}
```

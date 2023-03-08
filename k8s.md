---
theme: gaia
marp: true
size: 16:9
paginate: true
backgroundColor: #ffff
color: #000
backgroundImage: 
  - url(bg.svg)
_class: 
  - lead
title: K8s + Helm
author: Loghin Alexandru
style: |
  .columns {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1rem;
    }
---
![bg vertical left:40% 80%](https://upload.wikimedia.org/wikipedia/commons/6/67/Kubernetes_logo.svg)
![bg vertical left:40% 30%](https://upload.wikimedia.org/wikipedia/commons/9/9e/Plus_symbol.svg)
![bg vertical left:40% 30%](https://cncf-branding.netlify.app/img/projects/helm/horizontal/color/helm-horizontal-color.svg)

# Introduction

**Quick overview of k8s and the CLI**
**&**
**Why should you use Helm**

---
# Quick Disclaimer

This is a very short introduction into the kubernetes and helm ecosystem since the topic is very complex.

I highly encourage to dig deeper after this presentation by checking the official [documentation](https://kubernetes.io/docs/home/).

**Also if you have any questions just feel free to interrupt me.**

---
<!-- _class: lead -->
![bg vertical left:40% 80%](https://upload.wikimedia.org/wikipedia/commons/6/67/Kubernetes_logo.svg)

> **Kubernetes is an open-source system for automating deployment, scaling, and management of containerized applications.**

---
# What is kubernetes?

##### Keywords:

- **Automating deployments**
- **Scaling**
- **Containerized applications**

---
# Glossary
<div class="columns">
<div>

#### High Level:

- Control Plane
- Node/Agent
- Controllers
- Operator Pattern

</div>
<div>

#### Low Level:

- Orchestration(API,Manager...)
- Kubelet
- Kube Proxy
- Container Runtime

</div>
</div>

---
## Automating deployments
This can be easiley done via the Kubernetes Objects.

Options:

- Pod
- Deployment
- Daemon Set
- Stateful Set

---

### Scaling

What do you do when you need to handle load?

#### Option 1

Scale vertically. This means adding more available RAM/CPU to the pod.

#### Option 2

Scale horizontally. This means adding more instances of the same service and load balancing between them.

---

### Solution

In Kubernetes we can do both.

#### Vertically

- Requests & Limits

#### Horizontally

- Replicas & Services

---

### Containerized applications

I hope you are familiar with Docker or better said containerd.

Why you ask?

Each pod in kubernetes runs one or more **container images**.

The underling container engine can be of any kind as long as it implements the **Container Runtime Interface** (CRI).

---

### DNS

Every cluster needs one.

- Pods & Services have DNS entries
- It is scoped per namespace
- Queries are usually expanded via ```/etc/resolv.conf```
- Can be changed in any shape or form you imagine
eg. {service-name}.{namespace}.{svc|pod}.{cluster-domain}

---

#### Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
...
spec:
  replicas: 3
  ...
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

---

#### Service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: ClusterIP # Other options NodePort/LoadBalancer
  # clusterIP: None for Headless Service
  selector:
    app.kubernetes.io/name: MyApp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 9376
```

---

#### Ingress

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
...
spec:
  rules:
  - host: "*.foo.com"
    http:
      paths:
      - pathType: Prefix
        path: "/"
        backend:
          service:
            name: my-service
            port:
              number: 80
```

---

#### Kubeconfig

- Manages access to kubernetes clusters (plural)
- Usually you can find it in ~/.kube/config
- One file by default

#### Azure

```bash
$ az aks get-credentials --resource-group myResourceGroup --name myAKSCluste
```

##### K3s

```bash
$ export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
```

---

### Example

```yaml
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://192.168.1.12:6443
  name: homestack
contexts:
- context:
    cluster: homestack
    namespace: default
    user: default
  name: homestack
current-context: homestack
kind: Config
preferences: {}
users:
- name: default
  user:
    client-certificate-data: DATA+OMITTED
    client-key-data: DATA+OMITTED
```

---
<!-- _class: lead -->
![bg vertical left:40% 30%](https://cncf-branding.netlify.app/img/projects/helm/horizontal/color/helm-horizontal-color.svg)

> ### The package manager for Kubernetes.

---

### Package Manager?

- More like a templating engine with added stuff
- Very useful if you want to add versioning
- Adds an easy way to deploy/teardown a complex service
- Interacts with kubernetes
- Provides a ".Values" variable
- Hub for sharing charts [artifacthub.io](https://artifacthub.io/)
- CLI tool, nothing more nothing less

---

### More Details

- A deployable unit in helm is called a "Chart"
- Written in GO with the ```text/template``` package
- A release is a deployed chart on k8s
- Can upgrade/install/rollback releases
- It supports also repositories

```bash
NAME         	NAMESPACE	REVISION	UPDATED                                	STATUS  	CHART           	APP VERSION
homestack-dns	default  	1       	2023-02-16 17:11:27.513353937 +0000 UTC	deployed	coredns-0.1.0   	1.0.0      
kleilobby    	default  	2       	2023-02-14 15:23:26.310650121 +0000 UTC	deployed	klei-lobby-0.1.0	1.0.0 
```

---

### Links

- [Helm Docs](https://helm.sh/docs/helm/)
- [Kubernetes Docs](https://kubernetes.io/docs/home/)
- [Kubectl Docs](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)
- [Go template package](https://pkg.go.dev/text/template)
- [Recommended labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/common-labels/)
- [Well-Known Labels, Annotations and Taints](https://kubernetes.io/docs/reference/labels-annotations-taints/)
- [QoS for Pods](https://kubernetes.io/docs/tasks/configure-pod-container/quality-service-pod/#create-a-pod-that-gets-assigned-a-qos-class-of-burstable)

---

<!-- _class: lead -->

## DEMO

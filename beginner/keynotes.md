# Quick Context

- Lens is not OpenSource anymore so we need an alternative
- Kubectl is easy to use, all the commands have a logic behind them so they are easy to remember (CRUD)

# K8s

- Memebr of CNCF (Cloud Native Computing     Foundation)
- Open Source
- Written entirely in Go
- Usually hard to mantain locally on bare metal, that's why it is easier to use a mantained version (Azure, AWS, GCP)
- Container Runtime Interface (CRI) & Container Storage Interface (CSI)
- Usually targets stateless apps. Can work with state but it is difficult
- Mention (but don't go into detail) about PV, PVC, Job, CronJobs, RBAC, CRD etc.

# Helm

- Uses the default Go templates with some more helper functions
- Can hold subcharts
- Really useful to create dynamic charts. If you have something simple just write one deployment yaml with each resource separated by ```---```

# DEMO

- Get kubectl & helm binary in C:\Windows\System32
- Setup kubeconfig via az
- Config context & default namespace
- Show full API resources & Helm releases
- Load Balancer & random kubectl commands
- DNS expand via resolv.conf
- Metrics
- Generate helm chart & values override
- akv2k8s inject study case

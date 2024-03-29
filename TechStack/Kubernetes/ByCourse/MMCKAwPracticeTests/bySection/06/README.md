## Section 06 Cluster Maintenance

### Cluster Maintenance - Section Introduction

### OS Upgrades

```
> kubectl drain node-1
> kubectl drain node01 --ignore-daemonsets

> kubectl cordon node-2

> kubectl uncordon node-1


> kubectl get pods -o wide
```

### Kubernetes Software Versions

Reference:
[The Kubernetes API](https://kubernetes.io/docs/concepts/overview/kubernetes-api/)

API Conventions - [Github](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md)

API Changes - [Github](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api_changes.md)

### Cluster Upgrade Process

```
> kubeadm upgrade plan

> kubeadmin upgrade apply

> kubectl drain controlplane --ignore-daemonsets

> kubectl version --short

// Linux Commands
> apt install kubeadm=1.20.0-00
> apt install kubelet=1.20.0-00
> systemctl restart kubelet
```

### Backup and Restore Methods

```
// ETCD Cluster
> etcdctl snapshot save snapshot.db

> etcdctl snapshot status snapshot.db

> etcdctl snapshot restore snapshot.db --data-dir /var/lib/etcd-from-backup

> etcdctl snapshot save snapshot.db \
  --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/etcd/ca.crt \
  --cert=/etc/etcd/etcd-server.crt \
  --key=/etc/etcd/etcd-server.key

// Linux Commands
> systemctl daemon-reload

> service etcd restart
```

```
// etcd.service
ExecStart=/usr/local/bin/etcd \\
// to be continued
...
```

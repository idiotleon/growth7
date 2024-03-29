## Section 07 Security

### Security - Security Introduction

### Kubernetes Security Primitives

### Authentication

### Article on Setting up Basic Authentication

### TLS Introduction

### TLS Basics

### TLS in Kubernetes - Certificate Creation

1

```
// OpenSSL Commands
// to generate keys
> openssl genrsa -out ca.key 2048
// certificate signing request
> openssl req -new -key ca.key -subj "/CN=KUBERNETES-CA" -out ca.csr
// sign certificates
> openssl x509 -req -in ca.csr -signkey ca.key -out ca.crt
```

Kube API Server

- kubernetes 10.96.0.1
- kubernetes.default 172.17.0.87
- kubernetes.default.svc
- kubernetes.default.svc.cluster.local

### View Certificate Details

```
> journalctl -u etcd.service -l

> kubectl logs etcd-master
```

Reference:

- kubernetes-the-hard-way - [github](https://github.com/mmumshad/kubernetes-the-hard-way/tree/master/tools)

### Certificates API

```
> kubectl get csr

> kubectl certificate approve jane

> kubectl get csr jane -o yaml

> kubectl get csr agent-smith -o yaml

> kubectl certificate deny agent-smith

> kubectl delete csr agent-smith

// Linux Commands
> echo "LS0..Qo=" | base64 --decode
```

### KubeConfig

```
> kubectl get pods --kubeconfig config

> kubectl config view
> kubectl config view --kubeconfig=my-custom-config

> kubectl config use-context prod-user@production
```

### API Groups

### Authorization

#### Authorization Mode

- Node
- ABAC
- RBAC
- WebHook
- Always Allow
- Always Deny

### RBAC

```
> kubectl get roles

> kubectl get rolebindings

> kubectl describe role developer

> kubectl describe rolebinding devuser-developer-binding

// to check accesses
> kubectl auth can-i create deployments
> kubectl auth can-i delete nodes
> kubectl auth can-i create deployments --as dev-user
> kubectl auth can-i create pods --as dev-user
> kubectl auth can-i create pods --as dev-user --namespace test
```

### Cluster Roles and Role Bindings

```
> kubectl get clusterroles --no-headers | wc -l
> kubectl get clusterroles --no-headers -o json | jq '.items | length'

> kubectl get clusterrolebindings --no-headers | wc -l
> kubectl get clusterrolebindings --no-headers -o json | jq '.items | length'

// namespaced
> kubectl api-resources --namespaced=true

// cluster scoped
> kubectl api-resources --na

> kubectl create -f cluster-admin-role.yaml
> kubectl create -f cluster-admin-role-binding.yaml
```

### Service Account

```
> kubectl create serviceacount dashboard-sa

> kubectl get serviceaccount

> kubectl describe serviceaccount dashboard-sa

> kubectl describe secrete dashboard-sa-token-kbbdm

> kubectl get serviceaccount

> kubectl exec -it my-kubernetes-dashboard ls /var/run/secretes/kubernetes.io/serviceaccount

> kubectl exec -it my-kubernetes-dashboard cat /var/run/secrets/kubernetes.io/serviceaccount/token
```

### Image Security

```
// to work in pair with the YAML file
> kubecl create secret docker-register regcred \
    --docker-server= \
    --docker-username= \
    --docker-password= \
    --docker-email =

> kubectl create secret docker-registry private-reg-cred --docker-username=docker_user --docker-password=dock_password --docker-server=myprivateregistry.com:5000 --docker-email=docker_user@myprivateregistry.com

> kubectl create secret --help

// docker commands
> docker login private-registry.io
> docker run private-registry.io/apps/internal-app
```

### Security Contexts

```
> kubectl exec ubuntu-sleeper -- whoami
```

### Network Policy

| Solutions that support Network Policies | Solutions that do not support Network Policies |
| --------------------------------------- | ---------------------------------------------- |
| Kube-router, Calico, Romana, Weave-net  | Flannel                                        |

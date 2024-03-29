## Section 03 Scheduling

### Manual Scheduling

```
kubectl -n kube-system get pods
```

### Labels and Selectors

```
> kubectl get pods --selector env=dev

> kubectl get pods -l env=dev
> kubectl get pods -l env=dev --no-headers | ws -l

> kubectl get pods --selector bu=finance
> kubectl get all --selector env=prod
> kubectl get all --selector env=prod,bu=finance,tier=frontend
> kubectl get pods --show-labels

> kubectl create -f replicaset-definition-1.yaml
```

### Taints and Tolerations

```
> kubectl taint nodes node-name key=value:taint-effect

> kubectl taint nodes node1 app=blue:NodeSchedule

> kubectl taint nodes node1

> kubectl describe node kubemaster | grep Taint

> kubectl taint nodes node01 spray=mortein:NoSchedule

> kubectl taint nodes controlplane node-role.kubernetes.io/master:NoSchedule

> kubectl describe node node01 | grep -i taint

> kubectl run bee --image=nginx --restart=Never --dry-run -o yaml > bee.yaml

> kubectl explain pod --recursive | less

> kubectl explain pod --recursive | grep -A5 tolerations

```

### Node Selector

```
// kubectl label nodes <node-name> <label-key>=<label-value>
> kubectl label nodes node-1 size=Large
```

### Node Affinity

```
> kubectl get pods -o wide
```

### Resource Requirements and Limits

```
> kubectl replace -f elephant.yaml --force
```

### DaemonSets

```
> kubectl get daemonsets --all-namespaces

> kubectl -n kube-system describe ds weave-net | grep -i image

> kubectl create deployment elasticsearch --image=k8s.gcr.io/fluentd-elasticsearch:1.20 -n kube-system --dry-run=client -o yaml > fluentd.yaml
```

### Static Pods

<table>
    <thead>
        <tr>
            <th>Static PODs</th>
            <th>DaemonSets</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Created by tde Kubelet</td>
            <td>Created by Kube-API server (DaemonSet Controller)</td>
        </tr>
        <tr>
            <td>Depoy Control Plane components as Static Pods</td>
            <td>Deploy Monitoring Agents, Logging Agents on nodes</td>
        </tr>
        <tr>
            <td colspan=2>Ignored by the Kube-Scheduler</td>
        </tr>
    </tbody>
</table>

```
> kubectl run --restart=Never --image=busybox static-busybox --dry-run=client -o yaml --command -- sleep 1000 > /etc/kubernetes/manifests/static-busybox.yaml
```

### Multiple Schedulers

```
> kubectl get pods --namespace=kube-system

> kubectl logs my-custom-scheduler --name-space=kube-system

> kubectl -n kube-system describe pod kube-scheduler-master | grep Image
```

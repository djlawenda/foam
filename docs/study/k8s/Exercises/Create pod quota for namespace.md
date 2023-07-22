---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create pod quota for namespace.md'
---
# Create pod quota for namespace
Note Created: 2023-02-25

## Lab 
 how to set quotas for the total amount memory and CPU that can be used by **all Pods running** in a namespace

## Solution

Create a namespace
`kubectl create namespace quota-mem-cpu-example`

Create a [[ResourceQuota]]
```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: mem-cpu-demo
spec:
  hard:
    requests.cpu: "1"
    requests.memory: 1Gi
    limits.cpu: "2"
    limits.memory: 2Gi
```
`kubectl apply -f quota-mem-cpu.yaml --namespace=quota-mem-cpu-example`

Create a Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: quota-mem-cpu-demo
spec:
  containers:
  - name: quota-mem-cpu-demo-ctr
    image: nginx
    resources:
      limits:
        memory: "800Mi"
        cpu: "800m"
      requests:
        memory: "600Mi"
        cpu: "400m
```
`kubectl apply -f quota-mem-cpu-pod.yaml --namespace=quota-mem-cpu-example`

View detailed information about the ResourceQuota
`kubectl get resourcequota mem-cpu-demo --namespace=quota-mem-cpu-example --output=yaml`

```yaml
status:
  hard:
    limits.cpu: "2"
    limits.memory: 2Gi
    requests.cpu: "1"
    requests.memory: 1Gi
  used:
    limits.cpu: 800m
    limits.memory: 800Mi
    requests.cpu: 400m
    requests.memory: 600Mi
```

Attempt to create a second Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: quota-mem-cpu-demo-2
spec:
  containers:
  - name: quota-mem-cpu-demo-2-ctr
    image: redis
    resources:
      limits:
        memory: "1Gi"
        cpu: "800m"
      requests:
        memory: "700Mi"
        cpu: "400m"
```
Second Pod has a memory request of 700 MiB. Notice that the sum of the used memory request and this new memory request exceeds the memory request quota: 600 MiB + 700 MiB > 1 GiB
`kubectl apply -f quota-mem-cpu-pod-2.yaml --namespace=quota-mem-cpu-example`

```console
Error from server (Forbidden): error when creating "examples/admin/resource/quota-mem-cpu-pod-2.yaml":
pods "quota-mem-cpu-demo-2" is forbidden: exceeded quota: mem-cpu-demo,
requested: requests.memory=700Mi,used: requests.memory=600Mi, limited: requests.memory=1Gi
```

## Materials
* https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/quota-memory-cpu-namespace/
* https://kubernetes.io/docs/reference/kubernetes-api/policy-resources/resource-quota-v1/
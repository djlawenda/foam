---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create cpu resource limits in namespace.md'
---
# Create cpu resource limits in namespace
Note Created: 2023-02-25

## Lab 
 If you create a Pod within a namespace that has a default CPU limit, and any container in that Pod does not specify its own CPU limit, then the control plane assigns the default CPU limit to that container.

## Solution

Create namespace
`kubectl create namespace default-cpu-example`

Create LimitRange
```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: cpu-limit-range
spec:
  limits:
  - default:
      cpu: 1
    defaultRequest:
      cpu: 0.5
    type: Container
```
`kubectl apply -f cpu-defaults.yaml --namespace=default-cpu-example`

Create pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: default-cpu-demo
spec:
  containers:
  - name: default-cpu-demo-ctr
    image: nginx
```
`kubectl apply -f cpu-defaults-pod.yaml --namespace=default-cpu-example`

Get pod
`kubectl get pod default-cpu-demo --output=yaml --namespace=default-cpu-example`

Pod has assigned default resources from namespace
```yaml
containers:
- image: nginx
  imagePullPolicy: Always
  name: default-cpu-demo-ctr
  resources:
    limits:
      cpu: "1"
    requests:
      cpu: 500m
```


## Materials
https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/cpu-default-namespace/
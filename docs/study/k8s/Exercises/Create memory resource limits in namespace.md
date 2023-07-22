---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create resource limits in namespace.md'
---
# Create resource limits in namespace
Note Created: 2023-02-25

## Lab 

Once you have a namespace that has a default memory limit, and you then try to create a Pod with a container that does not specify its own memory limit, then the control plane assigns the default memory limit to that container.

## Solution

Create namespace

`kubectl create namespace default-mem-example`

Create a [[LimitRange]]

```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: mem-limit-range
spec:
  limits:
  - default:
      memory: 512Mi
    defaultRequest:
      memory: 256Mi
    type: Container
```

`kubectl apply -f memory-defaults.yaml --namespace=default-mem-example`

Create Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: default-mem-demo
spec:
  containers:
  - name: default-mem-demo-ctr
    image: nginx
```
`kubectl apply -f memory-defaults-pod.yaml --namespace=default-mem-example`

Get Pod
`kubectl get pod default-mem-demo --output=yaml --namespace=default-mem-example`

```yaml
containers:
- image: nginx
  imagePullPolicy: Always
  name: default-mem-demo-ctr
  resources:
    limits:
      memory: 512Mi
    requests:
      memory: 256Mi
```

## Materials
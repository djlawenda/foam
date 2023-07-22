---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create memory min max constrains in namespace.md'
---
# Create memory min max constrains in namespace
Note Created: 2023-02-25

## Lab 
How to set minimum and maximum values for memory used by containers running in a namespace. You specify minimum and maximum memory values in a LimitRange object.

## Solution

Create namespace
`kubectl create namespace constraints-mem-example`

Create a LimitRange
```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: mem-min-max-demo-lr
spec:
  limits:
  - max:
      memory: 1Gi
    min:
      memory: 500Mi
    type: Container
```
`kubectl apply -f memory-constraints.yaml --namespace=constraints-mem-example`

Get LimitRange
`kubectl get limitrange mem-min-max-demo-lr --namespace=constraints-mem-example --output=yaml`

```yaml
  limits:
  - default:
      memory: 1Gi
    defaultRequest:
      memory: 1Gi
    max:
      memory: 1Gi
    min:
      memory: 500Mi
    type: Container
```
> Min and max is used also as a default

Create Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: constraints-mem-demo
spec:
  containers:
  - name: constraints-mem-demo-ctr
    image: nginx
    resources:
      limits:
        memory: "800Mi"
      requests:
        memory: "600Mi"
```
`kubectl apply -f memory-constraints-pod.yaml --namespace=constraints-mem-example`

Get Pod
`kubectl get pod constraints-mem-demo --output=yaml --namespace=constraints-mem-example`

```yaml
resources:
  limits:
     memory: 800Mi
  requests:
    memory: 600Mi
```

## Materials
---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create cpu min max constrains in namespace.md'
---
# Create cpu min max constrains in namespace
Note Created: 2023-02-25

## Lab 

How to set minimum and maximum values for the CPU resources used by containers and Pods in a namespace.

## Solution

Create a namespace
`kubectl create namespace constraints-cpu-example`

Create a LimitRange
```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: cpu-min-max-demo-lr
spec:
  limits:
  - max:
      cpu: "800m"
    min:
      cpu: "200m"
    type: Container
```
`kubectl apply -f cpu-constraints.yaml --namespace=constraints-cpu-example`

`kubectl get limitrange cpu-min-max-demo-lr --output=yaml --namespace=constraints-cpu-example`

```yaml
limits:
- default:
    cpu: 800m
  defaultRequest:
    cpu: 800m
  max:
    cpu: 800m
  min:
    cpu: 200m
  type: Container
```
Default is copied from max

Create Pod
The container manifest specifies a CPU request of 500 millicpu and a CPU limit of 800 millicpu. These satisfy the minimum and maximum CPU constraints imposed by the LimitRange for this namespace.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: constraints-cpu-demo
spec:
  containers:
  - name: constraints-cpu-demo-ctr
    image: nginx
    resources:
      limits:
        cpu: "800m"
      requests:
        cpu: "500m"
```
`kubectl apply -f cpu-constraints-pod.yaml --namespace=constraints-cpu-example`

Get Pod
`kubectl get pod constraints-cpu-demo --output=yaml --namespace=constraints-cpu-example`
```yaml
resources:
  limits:
    cpu: 800m
  requests:
    cpu: 500m
```


## Materials
https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/cpu-constraint-namespace/
---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Attempt to create pod that exceeds the max cpu constrain in namespace.md'
---
# Attempt to create pod that exceeds the max cpu constrain in namespace
Note Created: 2023-02-25

## Lab 
Continuation of [[Create cpu min max constrains in namespace]]
The container specifies a CPU request of 500 millicpu and a cpu limit of 1.5 cpu.

## Solution

Create Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: constraints-cpu-demo-2
spec:
  containers:
  - name: constraints-cpu-demo-2-ctr
    image: nginx
    resources:
      limits:
        cpu: "1.5"
      requests:
        cpu: "500m"
```
`kubectl apply -f cpu-constraints-pod-2.yaml --namespace=constraints-cpu-example`

Error:
```console
Error from server (Forbidden): error when creating "examples/admin/resource/cpu-constraints-pod-2.yaml":
pods "constraints-cpu-demo-2" is forbidden: maximum cpu usage per Container is 800m, but limit is 1500m.
```

## Materials
https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/cpu-constraint-namespace/
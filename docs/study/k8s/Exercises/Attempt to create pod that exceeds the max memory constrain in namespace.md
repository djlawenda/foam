---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Attempt to create pod that exceeds the max memory constrain in namespace.md'
---
# Attempt to create pod that exceeds the max memory constrain in namespace
Note Created: 2023-02-25

## Lab 

Coninuation of [[Create memory min max constrains in namespace]]

## Solution

Create Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: constraints-mem-demo-2
spec:
  containers:
  - name: constraints-mem-demo-2-ctr
    image: nginx
    resources:
      limits:
        memory: "1.5Gi"
      requests:
        memory: "800Mi"
```

`kubectl apply -f memory-constraints-pod-2.yaml --namespace=constraints-mem-example`

```console
Error from server (Forbidden): error when creating "examples/admin/resource/memory-constraints-pod-2.yaml":
pods "constraints-mem-demo-2" is forbidden: maximum memory usage per Container is 1Gi, but limit is 1536Mi.
```

## Materials
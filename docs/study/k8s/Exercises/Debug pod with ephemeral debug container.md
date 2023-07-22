---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Debug pod with ephemeral debug container.md'
---
# Debug pod with ephemeral debug container
Note Created: 2023-02-25

## Lab 

Use the kubectl debug command to add ephemeral containers to a running Pod

## Solution

Create a pod
```console
kubectl run ephemeral-demo --image=registry.k8s.io/pause:3.1 --restart=Never
```
Pause container doesn't contain debugging utilities if you try `kubectl exec` it return error.
```console
kubectl exec -it ephemeral-demo -- sh
```
ERROR: OCI runtime exec failed: exec failed: container_linux.go:346: starting container process caused "exec: \"sh\": executable file not found in $PATH": unknown

### Add a new busybox container and attaches to it
```console
kubectl debug -it ephemeral-demo --image=busybox:1.28 --target=ephemeral-demo
```

## Materials
https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/
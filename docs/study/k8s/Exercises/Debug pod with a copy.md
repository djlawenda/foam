---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Debug pod with a copy.md'
---
# Debug pod with a copy
Note Created: 2023-02-25

## Lab 

Application's container images are built on busybox but you need debugging utilities not included in busybox

## Solution

Create Pod
```console
kubectl run myapp --image=busybox:1.28 --restart=Never -- sleep 1d
```

Create a copy of myapp named myapp-debug that adds a new Ubuntu container for debugging
```console
kubectl debug myapp -it --image=ubuntu --share-processes --copy-to=myapp-debug
```

## Materials
https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/
---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Debug pod with exec.md'
---
# Debug pod with exec
Note Created: 2023-02-25

## Lab 

Debugging with container exec

## Solution

If the container image includes debugging utilities, as is the case with images built from Linux and Windows OS base images, you can run commands inside a specific container with kubectl exec

### Look at the logs from a running Cassandra pod
```console
kubectl exec cassandra -- cat /var/log/cassandra/system.log
```

### Run a shell that's connected to your terminal using the -i and -t arguments
```console
kubectl exec -it cassandra -- sh
```
```console
kubectl exec --stdin --tty cassandra -- /bin/bash
```
> The double dash (--) separates the arguments you want to pass to the command from the kubectl arguments.

## Materials
https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/
https://kubernetes.io/docs/tasks/debug/debug-application/get-shell-running-container/
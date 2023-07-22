---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Exceed a container memory limit.md'
---
# Exceed a container memory limit
Note Created: 2023-02-22

## Lab 

A Container can exceed its memory request if the Node has memory available. But a Container is not allowed to use more than its memory limit. If a Container allocates more memory than its limit, the Container becomes a candidate for termination.

In this exercise, you create a Pod that attempts to allocate more memory than its limit.

## Solution

configuration file for a Pod that has one Container with a memory request of 50 MiB and a memory limit of 100 MiB

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: memory-demo-2
  namespace: mem-example
spec:
  containers:
  - name: memory-demo-2-ctr
    image: polinux/stress
    resources:
      requests:
        memory: "50Mi"
      limits:
        memory: "100Mi"
    command: ["stress"]
    args: ["--vm", "1", "--vm-bytes", "250M", "--vm-hang", "1"]
```
In the args section of the configuration file, you can see that the Container will attempt to allocate 250 MiB of memory, which is well above the 100 MiB limit.

Create Pod
Check Pod status
NAME            READY     STATUS      RESTARTS   AGE
memory-demo-2   0/1       OOMKilled   1          24s

OOM -- out of memory OOM

Delete Pod

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/assign-memory-resource/
---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create liveness probes with command.md'
---
# Create liveness probes with command
Note Created: 2023-02-25

## Lab 

Create a Pod that runs a container based on the registry.k8s.io/busybox image.

## Solution

Create Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    test: liveness
  name: liveness-exec
spec:
  containers:
  - name: liveness
    image: registry.k8s.io/busybox
    args:
    - /bin/sh
    - -c
    - touch /tmp/healthy; sleep 30; rm -f /tmp/healthy; sleep 600
    livenessProbe:
      exec:
        command:
        - cat
        - /tmp/healthy
      initialDelaySeconds: 5
      periodSeconds: 5
```
> `periodSeconds` field specifies that the kubelet should perform a liveness probe every 5 seconds
> `initialDelaySeconds` field tells the kubelet that it should wait 5 seconds before performing the first probe

 kubelet executes the command cat /tmp/healthy in the target container

 If the command succeeds, it returns 0, and the kubelet considers the container to be alive and healthy

 ```console
 kubectl apply -f exec-liveness.yaml
 kubectl describe pod liveness-exec
 ```
 At the bottom of the output, there are messages indicating that the liveness probes have failed, and the failed containers have been killed and recreated.
  ```console
Normal   Killing    10s                kubelet, node01    Container liveness failed liveness probe, will be restarted
 ```

 Wait another 30 seconds, and verify that the container has been restarted
```console
 $kubectl describe pod liveness-exec
 liveness-exec   1/1       Running   1          1m
 ```

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/
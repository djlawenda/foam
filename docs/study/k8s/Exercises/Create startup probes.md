---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create startup probes.md'
---
# Create startup probes
Note Created: 2023-02-25

## Lab 

Applications that might require an additional startup time on their first initialization. The trick is to set up a startup probe with the same command, HTTP or TCP check, with a failureThreshold * periodSeconds long enough to cover the worse case startup time.

## Solution

Create Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    test: liveness
  name: liveness-http
spec:
  containers:
  - name: liveness
    image: registry.k8s.io/liveness
    args:
    - /server
    ports:
    - name: liveness-port
      containerPort: 8080
      hostPort: 8080

    livenessProbe:
      httpGet:
        path: /healthz
        port: liveness-port
      failureThreshold: 1
      periodSeconds: 10

    startupProbe:
      httpGet:
        path: /healthz
        port: liveness-port
      failureThreshold: 30
      periodSeconds: 10
```

Thanks to the startup probe, the application will have a maximum of 5 minutes (30 * 10 = 300s) to finish its startup.

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/
[[Probe configuration]]
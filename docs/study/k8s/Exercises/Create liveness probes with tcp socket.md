---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create liveness probes with tcp socket.md'
---
# Create liveness probes with tcp socket
Note Created: 2023-02-25

## Lab 

Liveness probe uses a TCP socket. kubelet will attempt to open a socket to your container on the specified port. If it can establish a connection, the container is considered healthy

## Solution

Create Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: goproxy
  labels:
    app: goproxy
spec:
  containers:
  - name: goproxy
    image: registry.k8s.io/goproxy:0.1
    ports:
    - containerPort: 8080
    livenessProbe:
      tcpSocket:
        port: 8080
      initialDelaySeconds: 15
      periodSeconds: 20
```
kubelet will run the first liveness probe 15 seconds after the container starts. This will attempt to connect to the goproxy container on port 8080. If the liveness probe fails, the container will be restarted.

```console
kubectl apply -f tcp-liveness-readiness.yaml
kubectl describe pod goprox
```

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/
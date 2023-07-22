---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create liveness probes with gRPC.md'
---
# Create liveness probes with gRPC
Note Created: 2023-02-25

## Lab 

If your application implements gRPC Health Checking Protocol, kubelet can be configured to use it for application liveness checks. You must enable the GRPCContainerProbe feature gate in order to configure checks that rely on gRPC.

## Solution

Create Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: etcd-with-grpc
spec:
  containers:
  - name: etcd
    image: registry.k8s.io/etcd:3.5.1-0
    command: [ "/usr/local/bin/etcd", "--data-dir",  "/var/lib/etcd", "--listen-client-urls", "http://0.0.0.0:2379", "--advertise-client-urls", "http://127.0.0.1:2379", "--log-level", "debug"]
    ports:
    - containerPort: 2379
    livenessProbe:
      grpc:
        port: 2379
      initialDelaySeconds: 10
```
To use a gRPC probe, port must be configured.
```console
kubectl apply -f grpc-liveness.yaml
kubectl describe pod etcd-with-grpc
```

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/
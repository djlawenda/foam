---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create liveness probes with http request.md'
---
# Create liveness probes with http request
Note Created: 2023-02-25

## Lab 

Liveness probe uses an HTTP GET request

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
    livenessProbe:
      httpGet:
        path: /healthz
        port: 8080
        httpHeaders:
        - name: Custom-Header
          value: Awesome
      initialDelaySeconds: 3
      periodSeconds: 3
```
> `periodSeconds` field specifies that the kubelet should perform a liveness probe every 3 seconds
> `initialDelaySeconds` field tells the kubelet that it should wait 3 seconds before performing the first probe
kubelet sends an HTTP GET request to the server that is running in the container and listening on port 8080
If the handler for the server's /healthz path returns a success code, the kubelet considers the container to be alive and healthy. Any code greater than or equal to 200 and less than 400 indicates success. Any other code indicates failure.

```console
kubectl apply -f http-liveness.yaml
kubectl describe pod liveness-http
```

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/
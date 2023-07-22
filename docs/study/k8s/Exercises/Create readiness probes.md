---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create readiness probes.md'
---
# Create readiness probes
Note Created: 2023-02-25

## Lab 

 A pod with containers reporting that they are not ready does not receive traffic through Kubernetes Services.

 > Readiness probes runs on the container during its whole lifecycle.

## Solution

Readiness probes are configured similarly to liveness probes. The only difference is that you use the readinessProbe field instead of the livenessProbe field.

Create Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    test: readiness
  name: readiness-http
spec:
  containers:
  - name: readiness
    image: registry.k8s.io/liveness
    args:
    - /server
    readinessProbe:
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


## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-readiness-probes
[[Probe configuration]]
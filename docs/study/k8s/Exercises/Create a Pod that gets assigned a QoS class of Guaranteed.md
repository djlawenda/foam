---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create a Pod that gets assigned a QoS class of Guaranteed.md'
---
# Create a Pod that gets assigned a QoS class of Guaranteed
Note Created: 2023-02-25

## Lab 

How to configure Pods so that they will be assigned particular Quality of Service (QoS) classes. Kubernetes uses QoS classes to make decisions about evicting Pods when Node resources are exceeded.

For a Pod to be given a QoS class of Guaranteed:

- Every Container in the Pod must have a memory limit and a memory request.
- For every Container in the Pod, the memory limit must equal the memory request.
- Every Container in the Pod must have a CPU limit and a CPU request.
- For every Container in the Pod, the CPU limit must equal the CPU request.

## Solution

manifest for a Pod that has one Container

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: qos-demo
  namespace: qos-example
spec:
  containers:
  - name: qos-demo-ctr
    image: nginx
    resources:
      limits:
        memory: "200Mi"
        cpu: "700m"
      requests:
        memory: "200Mi"
        cpu: "700m"
```
`kubectl apply -f qos-pod.yaml --namespace=qos-example`

Get pod status.qosClass
`kubectl get pod qos-demo --namespace=qos-example --output=yaml`

```yaml
spec:
  containers:
    ...
    resources:
      limits:
        cpu: 700m
        memory: 200Mi
      requests:
        cpu: 700m
        memory: 200Mi
    ...
status:
  qosClass: Guaranteed
```

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/quality-service-pod/
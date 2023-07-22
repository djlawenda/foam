---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create a Pod that gets assigned a QoS class of BestEffort.md'
---
# Create a Pod that gets assigned a QoS class of BestEffort
Note Created: 2023-02-25

## Lab 

How to configure Pods so that they will be assigned particular Quality of Service (QoS) classes. Kubernetes uses QoS classes to make decisions about evicting Pods when Node resources are exceeded.

For a Pod to be given a QoS class of BestEffort, the Containers in the Pod must not have any memory or CPU limits or requests

## Solution

Manifest for a Pod that has one Container. The Container has no memory or CPU limits or requests

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: qos-demo-3
  namespace: qos-example
spec:
  containers:
  - name: qos-demo-3-ctr
    image: nginx
```
```console
kubectl apply -f qos-pod-3.yaml --namespace=qos-example
kubectl get pod qos-demo-3 --namespace=qos-example --output=yaml
```
```yaml
spec:
  containers:
    ...
    resources: {}
  ...
status:
  qosClass: BestEffort
```

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/quality-service-pod/
---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Assign Pods to Nodes.md'
---
# Assign Pods to Nodes
Note Created: 2023-02-25

## Lab
how to assign a Kubernetes Pod to a particular node 

1. schedule with nodeSelector
2. schedule with nodeName

## Solution

1. schedule with nodeSelector

Add a label to a node
```console
kubectl get nodes --show-labels
kubectl label nodes <your-node-name> disktype=ssd
kubectl get nodes --show-labels
```

Create a pod that gets scheduled to your chosen node
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    env: test
spec:
  containers:
  - name: nginx
    image: nginx
    imagePullPolicy: IfNotPresent
  nodeSelector: # schedule on node with matching label
    disktype: ssd
```
```console
kubectl apply -f pod-nginx.yaml
kubectl get pods --output=wide
```
NAME     READY     STATUS    RESTARTS   AGE    IP           NODE
nginx    1/1       Running   0          13s    10.200.0.4   worker0


2. schedule with nodeName
Create a pod that gets scheduled to specific node
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  nodeName: foo-node # schedule pod to specific node
  containers:
  - name: nginx
    image: nginx
    imagePullPolicy: IfNotPresent
```   

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/assign-pods-nodes/
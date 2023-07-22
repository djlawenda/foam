---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Assign Pods to Nodes using Node Affinity.md'
---
# Assign Pods to Nodes using Node Affinity
Note Created: 2023-02-25

## Lab 
how to assign a Kubernetes Pod to a particular node using Node Affinity

1. requiredDuringSchedulingIgnoredDuringExecution
2. preferredDuringSchedulingIgnoredDuringExecution

## Solution

Add a label to a node
```console
kubectl get nodes --show-labels
kubectl label nodes <your-node-name> disktype=ss
kubectl get nodes --show-labels
```

1. Schedule a Pod using required node affinity

Create Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: disktype
            operator: In
            values:
            - ssd            
  containers:
  - name: nginx
    image: nginx
    imagePullPolicy: IfNotPresent
```
This means that the pod will get scheduled only on a node that has a disktype=ssd label.

```console
kubectl apply -f pod-nginx-required-affinity.yaml
kubectl get pods --output=wide
```

2. Schedule a Pod using preferred node affinity
   
   Create Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  affinity:
    nodeAffinity:
      preferredDuringSchedulingIgnoredDuringExecution:
      - weight: 1
        preference:
          matchExpressions:
          - key: disktype
            operator: In
            values:
            - ssd          
  containers:
  - name: nginx
    image: nginx
    imagePullPolicy: IfNotPresent
```

```console
kubectl apply -f pod-nginx-required-affinity.yaml
kubectl get pods --output=wide
```
This means that the pod will prefer a node that has a disktype=ssd label.

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/assign-pods-nodes-using-node-affinity/
---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create serviceAccount.md'
---
# Create serviceAccount
Note Created: 2023-02-25

## Lab 

Create a new ServiceAccount which will have access to API server.

## Solution

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: secret-access-sa
```
```console
kubectl create -f serviceaccount.yaml
```

## Materials
LFD259  exercise 6.3
https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Get Secret.md'
---
# Get Secret
Note Created: 2023-02-25

## Lab 

## Solution

```console
kubectl get secrets
```

```console
kubectl describe secret db-user-pass
```

```yaml
Name:            db-user-pass
Namespace:       default
Labels:          <none>
Annotations:     <none>

Type:            Opaque

Data
====
password:    12 bytes
username:    5 bytes
```

Decode Secret
```console
kubectl get secret db-user-pass -o jsonpath='{.data.password}' | base64 --decode
```

## Materials
https://kubernetes.io/docs/tasks/configmap-secret/managing-secret-using-kubectl/
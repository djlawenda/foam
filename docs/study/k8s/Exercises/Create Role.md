---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create Role.md'
---
# Create Role
Note Created: 2023-02-26

## Lab 

A Role always sets permissions within a particular namespace; when you create a Role, you have to specify the namespace it belongs in.

## Solution

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""] # "" indicates the core API group
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
```

This Role ca get, watch and list pods in default namespace.

## Materials
https://kubernetes.io/docs/reference/access-authn-authz/rbac/
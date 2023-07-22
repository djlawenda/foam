---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create ClusterRole.md'
---
# Create ClusterRole
Note Created: 2023-02-26

## Lab 

ClusterRole is a non-namespaced resource. A ClusterRole can be used to grant the same permissions as a Role.
Create a ClusterRole which will list the actual actions allowed cluster-wide

[[Create serviceAccount]]
[[Create Role]]

## Solution

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: secret-access-cr
rules:
  - apiGroups:
    - "" # "" indicates the core API group
    resources:
    - secrets
    verbs:
    - get
    - list
```

This ClusterRole can get and list secrets across cluster.

## Materials
LFD259  exercise 6.3
https://kubernetes.io/docs/reference/access-authn-authz/rbac/
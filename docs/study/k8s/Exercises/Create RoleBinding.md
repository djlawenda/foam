---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create RoleBinding.md'
---
# Create RoleBinding
Note Created: 2023-02-26

## Lab 

Bind the Role to serviceAccount.

- [[Create serviceAccount]]
- [[Create Role]]
- [[Create ClusterRole]

## Solution

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: secret-rb
subjects:
  - kind: ServiceAccount
    name: secret-access-sa
roleRef:
  kind: ClusterRole
  name: secret-access-cr
  apiGroup: rbac.authorization.k8s.io
```
```console
kubectl create -f rolebinding.yaml
```
This binding assigns ClusterRole `secret-access-cr` to serviceAccount `secret-access-sa`.

## Materials
LFD259 exercise 6.3
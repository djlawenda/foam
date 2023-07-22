---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create config map from plain text.md'
---
# Create config map from plain text
Note Created: 2023-02-25

## Lab 

Use kubectl create configmap with the --from-literal argument to define a literal value from the command line

## Solution

### Create config map from literal --from-literal=VAR=VAL

```console
kubectl create configmap special-config --from-literal=special.how=very --from-literal=special.type=charm
kubectl get configmaps special-config -o yaml
```
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  creationTimestamp: 2022-02-18T19:14:38Z
  name: special-config
  namespace: default
  resourceVersion: "651"
  uid: dadce046-d673-11e5-8cd0-68f728db1985
data:
  special.how: very
  special.type: charm
```

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/
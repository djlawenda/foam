---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/View CRDs.md'
---
# View CRDs
Note Created: 2023-02-26

## Lab 

View CRDs currently in the cluster

## Solution

- View
```console
kubectl get crd
```

- Check YAML
```console
kubectl get crd <NAME> -o yaml
```

## Materials
LFD259 exercise 4.7.1
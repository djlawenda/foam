---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create YAML from existing object.md'
---
# Create YAML from existing object
Note Created: 2023-02-26

## Lab 

Create YAML from exsiting object in cluster

## Solution

- Pod
```console
k get po firstpod -o yaml > firstpod.yam
```

- Deployment
```console
k get deploy deploy-firstpod -o yaml > deploy-firstpod.yaml
```

## Materials
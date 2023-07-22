---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Use labels in selector.md'
---
# Use labels in selector
Note Created: 2023-02-25

## Lab 

Labels are key/value pairs that are attached to objects, such as pods. Labels are intended to be used to specify identifying attributes of objects that are meaningful and relevant to users, but do not directly imply semantics to the core system. Labels can be used to organize and to select subsets of objects.

Example labels:

"release" : "stable", "release" : "canary"
"environment" : "dev", "environment" : "qa", "environment" : "production"
"tier" : "frontend", "tier" : "backend", "tier" : "cache"
"partition" : "customerA", "partition" : "customerB"
"track" : "daily", "track" : "weekly"

The API currently supports two types of selectors: 
- equality-based 
- set-based.

## Solution

### Equality-based requirement
Three kinds of operators are admitted =,==,!=. The first two represent equality (and are synonyms), while the latter represents inequality.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: cuda-test
spec:
  containers:
    - name: cuda-test
      image: "registry.k8s.io/cuda-vector-add:v0.1"
      resources:
        limits:
          nvidia.com/gpu: 1
  nodeSelector:
    accelerator: nvidia-tesla-p100
```
### sample commands
```console
kubectl get --selector app=design2 pod -o yaml
kubectl get --selector app!=design2 pod -o yaml
```

### Set-based requirement
Three kinds of operators are supported: in,notin and exists (only the key identifier).

Examples:
- `environment in (production, qa)` all resources with key equal to environment and value equal to production or qa
- `tier notin (frontend, backend)` all resources with key equal to tier and values other than frontend and backend, and all resources with no labels with the tier key
- `partition` all resources including a label with key partition; no values are checked.
- `!partition `all resources without a label with key partition; no values are checked.

### sample commands
```console
kubectl get --selector app in (design1, design2) pod -o yaml
kubectl get --selector app notin (design1, design2) pod -o yaml
```

## Materials
https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/
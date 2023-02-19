---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/View objects.md'
---
# View objects
Note Created: 2023-02-19

## Lab 

1. List all services in the namespace
2. List all pods in all namespaces
3. List all pods in the current namespace, with more details
4. List a particular deployment
5. List all pods in the namespace
6. Get a pod's YAML

## Solution

1. kubectl get services 
2. kubectl get pods --all-namespaces
3. kubectl get pods -o wide
4. kubectl get deployment my-dep
5. kubectl get pods
6. kubectl get pod my-pod -o yaml

## Materials
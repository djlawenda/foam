---
type: exercise-note
tags: exercise, logs
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Interacting with running Pods.md'
---
# Interacting with running Pods
Note Created: 2023-02-19

## Lab 

1. dump pod logs
2. dump pod container logs
3. stream pod logs
4. stream pod container logs
5. Run pod as interactive shell
6. Listen on port 5000 on the local machine and forward to port 6000 on my-pod

## Solution

1. kubectl logs my-pod  
2. kubectl logs my-pod -c my-container
3. kubectl logs -f my-pod
4. kubectl logs -f my-pod -c my-container 
5. kubectl run -i --tty busybox --image=busybox:1.28 -- sh
6. kubectl port-forward my-pod 5000:6000

## Materials
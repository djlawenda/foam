---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/SecurtyContext runAsUser, runAsGroup.md'
---
# SecurtyContext runAsUser, runAsGroup
Note Created: 2023-02-25

## Lab 

- [[Add securityContext to pod]] 
- [[Add securityContext to container]]

## Solution

- `runAsUser` field specifies that for any Containers in the Pod, all processes run with user ID 1000
- `runAsGroup` field specifies the primary group ID of 3000 for all processes within any containers of the Pod

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/security-context/
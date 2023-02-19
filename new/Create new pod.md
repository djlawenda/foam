---
type: exercise-note
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create new pod.md'
---
# Create new pod
2023-02-19
Note Created: 2023-02-19

## Lab 

1. Start a single instance of nginx pod in the namespace of mynamespace
2. Generate spec for running pod nginx and write it into a file called pod.yaml

## Solution

1. kubectl run nginx --image=nginx -n mynamespace
2. kubectl run nginx --image=nginx --dry-run=client -o yaml > pod.yaml

## Materials
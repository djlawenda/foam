---
type: exercise-note
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create object from manifest.md'
---
# Create object from manifest
2023-02-19
Note Created: 2023-02-19

## Lab 

1. create resource(s)
2. create resource(s) from multiple files
3. create resource(s) from directory
4. create resource(s) from url

## Solution

1. kubectl apply -f ./my-manifest.yaml
2. kubectl apply -f ./my1.yaml -f ./my2.yaml
3. kubectl apply -f ./dir 
4. kubectl apply -f https://git.io/vPieo 

## Materials
https://kubernetes.io/docs/reference/kubectl/cheatsheet/
---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Get object and sort.md'
---
# Get object and sort
Note Created: 2023-02-19

## Lab 

1. List Services Sorted by Name
2. List PersistentVolumes sorted by capacity

## Solution

1. kubectl get services --sort-by=.metadata.name
2. kubectl get pv --sort-by=.spec.capacity.storage

## Materials
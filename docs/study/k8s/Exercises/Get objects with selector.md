---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Get objects with selector.md'
---
# Get objects with selector
Note Created: 2023-02-19

## Lab 

1. Get the all pods with label app=cassandra
2. Get all running pods in the namespace

## Solution

1. kubectl get pods --selector=app=cassandra -o
2. kubectl get pods --field-selector=status.phase=Running

## Materials
---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/List events.md'
---
# List events
Note Created: 2023-02-19

## Lab 

1. List Events sorted by timestamp
2. List all warning events

## Solution

1. kubectl get events --sort-by=.metadata.creationTimestamp
2. kubectl events --types=Warning

## Materials
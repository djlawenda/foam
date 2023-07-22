---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Sort by metadata.md'
---
# Sort by metadata
Note Created: 2023-03-04

## Lab

Display all pods and sort by creationTimestamp.

## Solution

```console
k get po -A --sort-by metadata.creationTimestamp
```

## Materials
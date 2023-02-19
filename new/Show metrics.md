---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Show metrics.md'
---
# Show metrics
Note Created: 2023-02-19

## Lab 

1. Show [[metrics]] for a given pod and its containers
2. Show [[metrics]] for a given pod and sort it by 'cpu'

## Solution

1. kubectl top pod POD_NAME --containers
2. kubectl top pod POD_NAME --sort-by=cpu

## Materials
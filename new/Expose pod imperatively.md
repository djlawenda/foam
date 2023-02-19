---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Expose pod imperatively.md'
---
# Expose pod imperatively
Note Created: 2023-02-19

## Lab 

1. expose pod at port 80

## Solution

1 kubectl expose po nginx-6db489d4b7-9wgn9 --port=80 --target-port=8000

## Materials
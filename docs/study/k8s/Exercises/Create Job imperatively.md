---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create Job imperatively.md'
---
# Create Job imperatively
Note Created: 2023-02-19

## Lab 

1. create a Job which prints "Hello World"

## Solution

1. kubectl create job hello --image=busybox:1.28 -- echo "Hello World"

## Materials
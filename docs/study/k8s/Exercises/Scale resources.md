---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Scale resources.md'
---
# Scale resources
Note Created: 2023-02-19

## Lab 

1. Scale a replicaset named 'foo' to 3
2. If the deployment named mysql's current size is 2, scale mysql to 3
3. Scale multiple replication controllers

## Solution

1. kubectl scale --replicas=3 rs/foo  
2. kubectl scale --current-replicas=2 --replicas=3 deployment/mysql
3. kubectl scale --replicas=5 rc/foo rc/bar rc/baz  

## Materials
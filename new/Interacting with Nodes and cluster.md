---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Interacting with Nodes and cluster.md'
---
# Interacting with Nodes and cluster
Note Created: 2023-02-19

## Lab 

1. Mark my-node as unschedulable
2. Drain my-node in preparation for maintenance
3. Mark my-node as schedulable
4. Display addresses of the master and services
5. Dump current cluster state to stdout

## Solution

1. kubectl cordon my-node
2. kubectl drain my-node
3. kubectl uncordon my-node
4. kubectl cluster-info 
5. kubectl cluster-info dump

## Materials
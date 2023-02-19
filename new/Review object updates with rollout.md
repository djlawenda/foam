---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Review object updates with rollout.md'
---
# Review object updates with rollout
Note Created: 2023-02-19

## Lab 

1. Check the history of deployments including the revision
2. Rollback to the previous deployment
3. Rollback to a specific revision
4. Watch rolling update status of "frontend" deployment until completion
5. Rolling restart of the "frontend" deployment

## Solution

1. kubectl rollout history deployment/frontend
2. kubectl rollout undo deployment/frontend
3. kubectl rollout undo deployment/frontend --to-revision=2
4. kubectl rollout status -w deployment/frontend
5. kubectl rollout restart deployment/frontend

## Materials
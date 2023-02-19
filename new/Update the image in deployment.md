---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Update the image in deployment.md'
---
# Update the image in deployment
Note Created: 2023-02-19

## Lab 

1. Rolling update "www" containers of "frontend" deployment, updating the image

## Solution

1. kubectl set image deployment/frontend www=image:v2

## Materials
---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Save pod logs to file.md'
---
# Save pod logs to file
Note Created: 2023-02-26

## Lab 

Save logs of pod alpha to file alpha.logs in ~/opt/answer/

## Solution

```console
kubectl logs alpha | sudo tee ~/opt/answer/alpha.logs
```

## Materials
https://www.youtube.com/watch?v=5cgpFWVD8ds 10:36
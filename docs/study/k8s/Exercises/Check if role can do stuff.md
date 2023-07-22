---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Check if role can do stuff.md'
---
# Check if role can do stuff
Note Created: 2023-03-04

## Lab 

Check if User john and paul with Role my-role can create Pod.

## Solution

```console
kubectl auth can-i create pod --as=john
```
yes
```console
kubectl auth can-i create pod --as=paul
```
no

## Materials
https://www.youtube.com/watch?v=YMxHK7FRlV0&t=1391s
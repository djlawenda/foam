---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/LFD259 domian review solution ch8.md'
---
# LFD259 domian review solution ch8
Note Created: 2023-03-04

## Lab 

> Find and use the `troubleshoot-review1.yaml` file to create a deployment. The create command will fail. Edit the file
to fix issues such that a single pod runs for at least a minute without issue. There are several things to fix.

```console
student@cp:˜$ kubectl create -f troubleshoot-review1.yaml
```
<Fix any errors found here>
When fixed it should look like this:

```console
student@cp:˜$ kubectl get deploy igottrouble
NAME READY UP-TO-DATE AVAILABLE AGE
igottrouble 1/1 1 1 5m13s
```


> Remove any resources created during this review.

## Solution

## Materials
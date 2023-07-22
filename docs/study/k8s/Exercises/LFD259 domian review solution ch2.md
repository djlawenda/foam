---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/LFD259 domian review solution ch2.md'
---
# LFD259 domian review solution ch2
Note Created: 2023-02-26

## Lab 

1. A new pod with the nginx image. Showing all containers running and a Ready status.
```console
k run new --image=nginx
```
2. A new service exposing the pod as a nodePort, which presents a working webserver configured in the previous step.
```console
k expose pod new --port=80
k edit svc new
```
replace type: ConfigIP with type:NodePort

3. Update the pod to run the nginx:1.11-alpine image and re-verify you can view the webserver via a NodePort.
```console
k edit po new
```
replace image:nginx with image:nginx:1.11-alpine
```console
# check on which node po is running
k get po new -o wide
# check the IP of node01
k describe node node01
# check port assigned to svc NodePort
k get svc
# check nginx
curl nodeIP:NodePort
```
4. Delete any resources created during this review.

## Solution

## Materials
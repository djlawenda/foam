---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Debug misbehaving pods (k get, k describe, k logs, k exec).md'
---
# Debug misbehaving pods (k get, k describe, k logs, k exec)
Note Created: 2023-02-25

## Lab 

## Solution

1. The first step in debugging a Pod is taking a look at it. Check the current state of the Pod and recent events with the following command:
```console
kubectl describe pods ${POD_NAME}
```

2. My pod stays pending
   
If a Pod is stuck in Pending it means that **it can not be scheduled onto a node**. Generally this is because there are insufficient resources of one type or another that prevent scheduling. Look at the output of the kubectl describe ... command above. There should be messages from the scheduler about why it can not schedule your pod.

- **You don't have enough resources**: You may have exhausted the supply of CPU or Memory in your cluster
- **You are using hostPort**: When you bind a Pod to a hostPort there are a limited number of places that pod can be scheduled

3. My pod stays waiting
   
If a Pod is stuck in the Waiting state, then it has been scheduled to a worker node, but it can't run on that machine. **The most common cause of Waiting pods is a failure to pull the image.**
- Make sure that you have the name of the image correct.
- Have you pushed the image to the registry?
- Try to manually pull the image to see if the image can be pulled.

4. My pod is running but not doing what I told it to do
   
The first thing to do is to delete your pod and try creating it again with the --validate option. For example, run kubectl apply --validate -f mypod.yaml
The next thing to check is whether the pod on the apiserver matches the pod you meant to create (e.g. in a yaml file on your local machine). For example, run kubectl get pods/mypod -o yaml > mypod-on-apiserver.yaml and then manually compare the original pod description, mypod.yaml with the one you got back from apiserver, mypod-on-apiserver.yaml


## Materials
https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/
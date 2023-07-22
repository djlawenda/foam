---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Add custom commands to pod.md'
---
# Add custom commands to pod
Note Created: 2023-02-25

## Lab 

When you create a Pod, you can define a command and arguments for the containers that run in the Pod.

- To define a command, include the `command` field in the configuration file.
- To define arguments for the command, include the `args` field in the configuration file.

## Solution

Create Pod

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: command-demo
  labels:
    purpose: demonstrate-command
spec:
  containers:
  - name: command-demo-container
    image: debian
    command: ["printenv"] # add command
    args: ["HOSTNAME", "KUBERNETES_PORT"] # add argument
  restartPolicy: OnFailure
```

Run a command in a shell if there are several commands piped together, or it might be a shell script

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: command-demo
  labels:
    purpose: demonstrate-command
spec:
  containers:
  - name: command-demo-container
    image: debian
    command: ["/bin/sh"] # run shell
    args: ["-c", "while true; do echo hello; sleep 10;done"] # run commands as args
  restartPolicy: OnFailure
```

## Materials
https://kubernetes.io/docs/tasks/inject-data-application/define-command-argument-container/
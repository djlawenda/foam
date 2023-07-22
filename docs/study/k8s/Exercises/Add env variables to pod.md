---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Add env variables to pod.md'
---
# Add env variables to pod
Note Created: 2023-02-25

## Lab 

Use environment variables to define arguments

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
    env:
    - name: MESSAGE # add env var
      value: "hello world"
    command: ["/bin/echo"]
    args: ["$(MESSAGE)"] # use env var as an arg
  restartPolicy: OnFailure
```

## Materials
https://kubernetes.io/docs/tasks/inject-data-application/define-command-argument-container/

## Lab 

Define an environment dependent variable for a container
To set dependent environment variables, you can use $(VAR_NAME) in the value of env in the configuration file.

## Solution

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: dependent-envars-demo
spec:
  containers:
    - name: dependent-envars-demo
      args:
        - while true; do echo -en '\n'; printf UNCHANGED_REFERENCE=$UNCHANGED_REFERENCE'\n'; printf SERVICE_ADDRESS=$SERVICE_ADDRESS'\n';printf ESCAPED_REFERENCE=$ESCAPED_REFERENCE'\n'; sleep 30; done;
      command:
        - sh
        - -c
      image: busybox:1.28
      env:
        - name: SERVICE_PORT
          value: "80"
        - name: SERVICE_IP
          value: "172.17.0.1"
        - name: UNCHANGED_REFERENCE
          value: "$(PROTOCOL)://$(SERVICE_IP):$(SERVICE_PORT)"
        - name: PROTOCOL
          value: "https"
        - name: SERVICE_ADDRESS
          value: "$(PROTOCOL)://$(SERVICE_IP):$(SERVICE_PORT)"
        - name: ESCAPED_REFERENCE
          value: "$$(PROTOCOL)://$(SERVICE_IP):$(SERVICE_PORT)"
```

## Materials
https://kubernetes.io/docs/tasks/inject-data-application/define-interdependent-environment-variables/
---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/LFD259 domian review solution ch4.md'
---
# LFD259 domian review solution ch4
Note Created: 2023-02-26

## Lab 

> Find and use the `design-review1.yaml` file to create a pod.
```console
k create -f design-review1.yaml
```
> Determine the CPU and memory resource requirements of design-pod1.
pod asks for 1 CPU and 1036Mi mem, resource request 0.3 cpu/456Mi mem with limits 2.22 cpu/567Mi
   Edit the pod resource requirements such that the CPU limit is exactly twice the amount requested by the container. (Hint: subtract .22)
changed
```yaml
    resources:
      limits:
        cpu: "2.22"
        memory: "567Mi"
      requests:
        cpu: "0.3"
        memory: "456Mi"
```
to
```yaml
    resources:
      limits:
        cpu: "2"
        memory: "567Mi"
      requests:
        cpu: "0.3"
        memory: "456Mi"
```
> Increase the memory resource limit of the pod until the pod shows a Running status. This may require multiple edits and attempts. Determine the minimum amount necessary for the Running status to persist at least a minute.
```yaml
    resources:
      limits:
        cpu: "2"
        memory: "1050Mi"
      requests:
        cpu: "0.3"
        memory: "456Mi"
```

> Use the `design-review2.yaml` file to create several pods with various labels.
```console
k create -f design-review2.yaml
```

> Using only the –selector value tux to delete only those pods. This should be half of the pods. Hint, you will need to view pod settings to determine the key value as well.
```console
# check labels of all pod
kubectl get pods --show-labels
# delete all pods where review=tux
k delete po --selector review=tux
```

> Create a new cronjob which runs busybox and the sleep 30 command. Have the cronjob run every three minutes. View the job status to check your work. Change the settings so the pod runs 10 minutes from the current time, every week. For example, if the current time was 2:14PM, I would configure the job to run at 2:24PM, every Monday.
```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: hello
spec:
  schedule: "*/3 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: hello
            image: busybox:1.28
            imagePullPolicy: IfNotPresent
            command:
            - /bin/sh
            - -c
            - sleep 30
          restartPolicy: OnFailure
```

> Delete any resources created during this review.

## Solution

## Materials
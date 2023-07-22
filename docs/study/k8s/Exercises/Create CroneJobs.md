---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create CroneJobs.md'
---
# Create CroneJobs
Note Created: 2023-02-25

## Lab 

Create CronJob that runs "Hello from the Kubernetes cluster" each minute on busybox.
CronJob is wrapper for Job [[Create Jobs]]

## Solution

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: hello
spec: # spec of CronJob
  schedule: "* * * * *" # schedule
  jobTemplate: 
    spec: # spec of Job in CronJob
      template: 
        spec: # spec of Pod in Job
          containers:
          - name: hello
            image: busybox:1.28
            imagePullPolicy: IfNotPresent
            command:
            - /bin/sh
            - -c
            - date; echo Hello from the Kubernetes cluster
          restartPolicy: OnFailure
```

Watch for the job to be created
```console
kubectl get jobs --watch
```

Show the pod log
```console
kubectl logs $pods
```

## Materials
https://kubernetes.io/docs/tasks/job/automated-tasks-with-cron-jobs/ 
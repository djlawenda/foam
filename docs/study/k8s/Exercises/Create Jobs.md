---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create Jobs.md'
---
# Create Jobs
Note Created: 2023-02-26

## Lab 

Create a job which will run a container which sleeps for three seconds then stops.
Run Jobs at a schedule [[Create CroneJobs]]

## Solution

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: sleepy
spec:
  compleions: 3 # how many times to run the job
  parallelism: 1 # how many pods to run at a time
  activeDeadlineSeconds: 15 # all pods and job end after N seconds  
  template:
    spec:
      containers:
      - name: resting
       image: busybox
       command: ["/bin/sleep"]
       args: ["3"]
      restartPolicy: Never
```
```console
kubectl create -f job.yaml
```


## Materials
LFD259 exercise 4.2.1
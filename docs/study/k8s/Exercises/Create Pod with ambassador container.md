---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create Pod with ambassador container.md'
---
# Create Pod with ambassador container
Note Created: 2023-02-25

## Lab 

Ambassador containers proxy a local connection to the world.  As an example, consider a Redis cluster with read-replicas and a single write master.  You can create a Pod that groups your main application with a Redis ambassador container.  The ambassador is a proxy is responsible for splitting reads and writes and sending them on to the appropriate servers. 

## Solution

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: curl-with-ambassador
spec:
  containers:
  - name: main
    image: tutum/curl
    command: ["sleep", "9999999"]
  - name: ambassador
    image: omrizzy/ambassador:1.0
```

* [ ] Read more stuff from https://dev.bitolog.com/ambassador-container/

## Materials
https://kubernetes.io/blog/2015/06/the-distributed-system-toolkit-patterns/
https://dev.bitolog.com/ambassador-container/
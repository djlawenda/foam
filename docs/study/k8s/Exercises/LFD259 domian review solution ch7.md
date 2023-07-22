---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/LFD259 domian review solution ch7.md'
---
# LFD259 domian review solution ch7
Note Created: 2023-03-04

## Lab 

>  Create a new pod called webone, running the nginx service. Expose port 80.
```console
k run webone --image=nginx
kubectl expose pod webone --port=80
```

>  Create a new service named webone-svc. The service should be accessible from outside the cluster.
```console
kubectl expose pod webone --port=80 --name=webone-svc --type=NodePort 
```

> Update both the pod and the service with selectors so that traffic for to the service IP shows the web server content.
??

> Change the type of the service such that it is only accessible from within the cluster. Test that exterior access no longer
works, but access from within the node works.
??

> Deploy another pod, called webtwo, this time running the wlniao/website image. Create another service, called
webtwo-svc such that only requests from within the cluster work. Note the default page for each server is distinct.
```console
k run webtwo --image=wlniao/website
kubectl expose pod webtwo --port=80
```

> Install and configure an ingress controller such that requests for webone.com see the nginx default page, and requests
for webtwo.org see the wlniao/website default page.
??

> Remove any resources created in this review.

## Solution

## Materials
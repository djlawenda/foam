---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create Network policy.md'
---
# Create Network policy
Note Created: 2023-02-25

## Lab 

Make sure you've configured a network provider with network policy support.
Antrea
Calico
Cilium
Kube-router
Romana
Weave Net

> Declare network policies that govern how pods communicate with each other

## Solution

Create an nginx deployment
```console
kubectl create deployment nginx --image=nginx
```

Expose the Deployment through a Service called nginx
```console
kubectl expose deployment nginx --port=80
```

Test the service by accessing it from another Pod
```console
$kubectl run busybox --rm -ti --image=busybox:1.28 -- /bin/sh
$wget --spider --timeout=1 nginx
Connecting to nginx (10.100.0.16:80)
remote file exists
```

Create a NetworkPolicy
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: access-nginx
spec:
  podSelector:
    matchLabels:
      app: nginx
  ingress:
  - from:
    - podSelector:
        matchLabels:
          access: "true"
```
NetworkPolicy includes a podSelector which selects the grouping of Pods to which the policy applies.

Assign the policy to the service
```console
kubectl apply -f nginx-policy.yaml
```

Attempt to connect from a Pod without the correct labels: FAIL
```console
$kubectl run busybox --rm -ti --image=busybox:1.28 -- /bin/sh
$wget --spider --timeout=1 nginx
Connecting to nginx (10.100.0.16:80)
wget: download timed out
```

Attempt to connect from a Pod without the correct labels: SUCCESS
```console
$kubectl run busybox --rm -ti --labels="access=true" --image=busybox:1.28 -- /bin/sh
$wget --spider --timeout=1 nginx
Connecting to nginx (10.100.0.16:80)
remote file exists
```

## Materials
https://kubernetes.io/docs/tasks/administer-cluster/declare-network-policy/

## Lab 

Create a default policy which denies all traffic

## Solution

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-default
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  - Egress
```

## Lab 

Create a policy which allows traffic from ipBlock on port 80

## Solution

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-default
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  ingress:
  - from:
    - ipBlock:
        cidr: 192.168.0.0/16
    ports:
    - port: 80
```

## Materials
LFD259 exercise 6.4
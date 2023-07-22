---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Modify container capabilites.md'
---
# Modify container capabilites
Note Created: 2023-02-26

## Lab 

Add new capabilites to container.
A capability allows granting of specific, elevated privileges without granting full root access. We will be setting NET ADMIN to allow interface, routing, and other network configuration. We’ll also set SYS TIME, which allows system clock configuration.

## Solution

Create Pod with container without additional capabilties
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secondapp
spec:
  securityContext:
    runAsUser: 1000
  containers:
  - name: busy
    image: busybox
    command:
      - sleep
      - "3600"
    securityContext:
      runAsUser: 2000
      allowPrivilegeEscalation: false
```
```console
kubectl create -f second.yaml
```

- check capabilites
```console
kubectl exec -it secondapp -- sh
$ ps aux
$ grep Cap /proc/1/status
```
CapInh: 00000000000005fb
CapPrm: 0000000000000000
CapEff: 0000000000000000
CapBnd: 00000000000005fb
CapAmb: 0000000000000000
```console
$ exit
capsh --decode=00000000000005fb
```
0x00000000000005fb=cap_chown,cap_dac_override,cap_fowner,cap_fsetid,cap_kill,
cap_setgid,cap_setuid,cap_setpcap,cap_net_bind_service

- add capabilties
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secondapp
spec:
  securityContext:
    runAsUser: 1000
  containers:
  - name: busy
    image: busybox
    command:
      - sleep
      - "3600"
    securityContext:
      runAsUser: 2000
      allowPrivilegeEscalation: false
      capabilties:
        add: ["NET_ADMIN", "SYS_TIME"]
```
```console
kubectl apply -f second.yaml
```
- check capabilites
```console
kubectl exec -it secondapp -- sh
$ ps aux
$ grep Cap /proc/1/status
```
CapInh: 00000000020015fb
CapPrm: 0000000000000000
CapEff: 0000000000000000
CapBnd: 00000000020015fb
CapAmb: 0000000000000000
```console
$ exit
capsh --decode=00000000020015fb
```
0x00000000020015fb=cap_chown,cap_dac_override,cap_fowner,cap_fsetid,cap_kill,
cap_setgid,cap_setuid,cap_setpcap,cap_net_bind_service,cap_net_admin,cap_sys_time

## Materials
LFD259 exercise 6.1
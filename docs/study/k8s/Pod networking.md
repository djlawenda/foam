---
type: basic-note
foam_template:
    name: basic-note
    description: Basic note
    filepath: 'new/Pod networking.md'
---
# Pod networking
2023-02-19
Note Created: 2023-02-19

## Note

There is only one IP address per [[Pod]]. If there is more than one
[[container]] in a pod, they must share the IP. To communicate with each
other, they can either use IPC, the loopback interface, or a shared file
system.

All [[container]]s in a pod share the same network [[namespace]].

[[Pod to Pod]]
---
type: definition-note
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/kube-proxy.md'
---
# kube-proxy
2023-02-19
Note Created: 2023-02-19

## Definition

The kube-proxy creates and manages networking rules to expose the
container on the network to other containers or the outside world.

It does so through the use of iptables entries. It also has the
userspace mode, in which it monitors Services and Endpoints using a
random port to proxy traffic via ipvs. A network plugin pod, such as
calico-node, may be found depending on the plugin in use.
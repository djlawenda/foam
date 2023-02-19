---
type: definition-note
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/kubelet.md'
---
# kubelet
2023-02-19
Note Created: 2023-02-19

## Definition

Each node in the cluster runs two processes: a [[kubelet]], which is often a
systemd process, not a container, and kube-proxy.

The kubelet receives requests to run the containers, manages any
resources necessary and works with the container engine to manage them
on the local node. The local container engine could be Docker, cri-o,
containerd, or some other.

Intakes API call from api-server with PodSpec (JSON). It will work to
configure the local node until the specification has been met. The heavy
lifter for changes and configuration on worker nodes.

Should a Pod require access to storage, Secrets or ConfigMaps, the
kubelet will ensure access or creation. It also sends back status to the
kube-apiserver for eventual persistence.
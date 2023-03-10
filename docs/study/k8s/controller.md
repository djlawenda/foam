---
type: definition-note
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/controller.md'
---
# controller
2023-02-19
Note Created: 2023-02-19

## Definition

Orchestration is managed through a series of watch-loops, also called
[[controller]] or operators. Each controller interrogates the
kube-apiserver for a particular object state, then modifies the object
until the declared state matches the current state. These controllers
are compiled into the kube-controller-manager

The kube-controller-manager is a core control loop daemon which
interacts with the kube-apiserver to determine the state of the cluster.
If the state does not match, the manager will contact the necessary
controller to match the desired state. There are several operators in
use, such as endpoints, namespace, and replication.

They query the current state, compare it against the spec, and execute
code based on how they differ. Various operators ship with Kubernetes,
and you can create your own, as well. A simplified view of an operator
is an agent, or Informer, and a downstream store. Using a DeltaFIFO
queue, the source and downstream are compared.
---
type: basic-note
foam_template:
    name: basic-note
    description: Basic note
    filepath: 'new/Pod to Pod.md'
---
# Pod to Pod
2023-02-19
Note Created: 2023-02-19

## Note

[[Pod]] to Pod

[[Service]] identifies the pods to transfer traffic by selectors

When service identifies and matches pods labels it register them as its
[[Endpoints]]

Service picks one of its Endpoints randomly and sends the traffic to Pod
at targetPort

K8s creates Endpoints as the objects

If service has multiple ports then they need to have name

Headless services are useful for stateful app like DBs bc their pods are
not identical
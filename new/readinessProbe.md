---
type: definition-note
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/readinessProbe.md'
---
# readinessProbe
2023-02-19
Note Created: 2023-02-19

## Definition

Sometimes, applications are temporarily unable to serve traffic.
Kubernetes provides readiness probes to detect and mitigate these
situations. A pod with containers reporting that they are not ready does
not receive traffic through Kubernetes Services.
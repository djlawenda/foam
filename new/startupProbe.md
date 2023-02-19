---
type: definition-note
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/startupProbe.md'
---
# startupProbe
2023-02-19
Note Created: 2023-02-19

## Definition

If [[kubelet]] uses a startupProbe, it will disable liveness and readiness
checks until the application passes the test. The duration until the
container is considered failed is failureThreshold times periodSeconds.
For example, if your periodSeconds was set to five seconds, and your
failureThreshold was set to ten, kubelet would check the application
every five seconds until it succeeds, or is considered failed after a
total of 50 seconds.
---
type: definition-note
tags: definition
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/Probe configuration.md'
---
# Probe configuration
Note Created: 2023-02-25

## Definition

`initialDelaySeconds`: Number of seconds after the container has started before startup, liveness or readiness probes are initiated. Defaults to 0 seconds. Minimum value is 0.

`periodSeconds`: How often (in seconds) to perform the probe. Default to 10 seconds. Minimum value is 1.

`timeoutSeconds`: Number of seconds after which the probe times out. Defaults to 1 second. Minimum value is 1.
`successThreshold`: Minimum consecutive successes for the probe to be considered successful after having failed. Defaults to 1. Must be 1 for liveness and startup Probes. Minimum value is 1.

`failureThreshold`: After a probe fails failureThreshold times in a row, Kubernetes considers that the overall check has failed:

`terminationGracePeriodSeconds`: configure a grace period for the kubelet to wait between triggering a shut down of the failed container, and then forcing the container runtime to stop that container.

https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-readiness-probes
---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Change probes type (http, custom command, socket).md'
---
# Change probes type (http, custom command, socket)
Note Created: 2023-02-25

## Lab 

  - [[Create liveness probes with command]]
  - [[Create liveness probes with http request]]
  - [[Create liveness probes with tcp socket]]
  - [[Create liveness probes with gRPC]]

## Solution

### HTTP probes
HTTP probes have additional fields that can be set on httpGet:

`host`: Host name to connect to, defaults to the pod IP. You probably want to set "Host" in httpHeaders instead.

`scheme`: Scheme to use for connecting to the host (HTTP or HTTPS). Defaults to HTTP.

`path`: Path to access on the HTTP server. Defaults to /.

`httpHeaders`: Custom headers to set in the request. HTTP allows repeated headers.

`port`: Name or number of the port to access on the container. Number must be in the range 1 to 65535.

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-readiness-probes
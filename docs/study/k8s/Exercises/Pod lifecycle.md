---
type: basic-note
foam_template:
    name: basic-note
    description: Basic note
    filepath: 'new/Pod lifecycle.md'
---
# Pod lifecycle
Note Created: 2023-02-25

## Note

###  [[Pod]] phases
Phase is the field if PodStatus object.

> `Pending`	The Pod has been accepted by the Kubernetes cluster, but one or more of the **containers has not been set up** and made ready to run. This includes time a Pod spends waiting to be scheduled as well as the time spent downloading container images over the network.
> `Running`	The Pod has been bound to a node, and **all of the containers have been created**. At least one container is still running, or is in the process of starting or restarting.
> `Succeeded`	All containers in the Pod have terminated in success, and will not be restarted.
> `Failed`	All containers in the Pod have terminated, and at least one container has terminated in failure. That is, the container either exited with non-zero status or was terminated by the system.
> `Unknown`	For some reason the state of the Pod could not be obtained. This phase typically occurs due to an error in communicating with the node where the Pod should be running.
> This `Terminating` status is not one of the Pod phases. A Pod is granted a term to terminate gracefully, which defaults to 30 seconds. You can use the flag --force.

###  [[Container]] states
> `Waiting` A container in the Waiting state is still running the operations it requires in order to complete start up
> `Running` a container is executing without issues
> `Terminated` a container began execution and then either ran to completion or failed for some reason

### Pod conditions
PodStatus has an array of PodConditions through which the Pod has or has not passed.

> `PodScheduled` the Pod has been scheduled to a node. [Pod Scheduling Readiness]([https://](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-scheduling-readiness/))
> `PodHasNetwork`: (alpha feature; must be enabled explicitly) the Pod sandbox has been successfully created and networking configured. [Pod network readiness]([https://](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#pod-has-network))
> `ContainersReady`: all containers in the Pod are ready.
> `Initialized`: all init containers have completed successfully.
Ready: the Pod is able to serve requests and should be added to the load balancing pools of all matching Services.

### Container probes
There are four different ways to check a container using a probe.

> `exec` Executes a specified command inside the container. The diagnostic is considered successful if the command exits with a status code of 0.
> `grpc` Performs a remote procedure call using gRPC. The diagnostic is considered successful if the status of the response is SERVING.
> `httpGet` Performs an HTTP GET request against the Pod's IP address on a specified port and path. The diagnostic is considered successful if the response has a status code greater than or equal to 200 and less than 400.
> `tcpSocket` Performs a TCP check against the Pod's IP address on a specified port. The diagnostic is considered successful if the port is open.

[[Create readiness probes]]
[[Create liveness probes]]
[[Create startup probes]] Startup probes are useful for Pods that have containers that take a long time to come into service.

### Termination of Pods
Typically, the container runtime sends a [[TERM signal]] to the main process in each container. Many container runtimes respect the [[STOPSIGNAL]] value defined in the container image and send this instead of TERM. Once the grace period has expired, the [[KILL signal]] is sent to any remaining processes, and the Pod is then deleted from the API Server.

At the same time as the kubelet is starting graceful shutdown, the control plane removes that shutting-down Pod from EndpointSlice (and Endpoints) objects where these represent a Service with a configured selector.

> Immediate deletion of Pod use flag --force along with --grace-period=0

### Garbage collection of Pods
The Pod garbage collector (PodGC), which is a controller in the control plane, cleans up terminated Pods (with a phase of Succeeded or Failed), when the number of Pods exceeds the configured threshold

## Materials
https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/




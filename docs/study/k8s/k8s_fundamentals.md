---
generator: Aspose.Words for Java 21.4.0;
---

Manage containerized application

Docker Swarm is the solution provided by Docker Inc. It has been
re-architected recently and is based on SwarmKit. It is embedded with
the Docker Engine

Apache Mesos is a data center scheduler, which can run containers
through the use of frameworks. Marathon is the framework that lets you
orchestrate containers.

Nomad from HashiCorp, solution for managing containerized applications.
Nomad schedules tasks defined in Jobs. It has a Docker driver which lets
you define a running container as a task.

Rancher is a container orchestrator-agnostic system, which provides a
single pane of glass interface to manage applications. It supports
Mesos, Swarm, Kubernetes.

The Cloud Foundry Foundation embraces the 12 factor application
principles.

Kubernetes Architecture

[[Control plane node]]

Kubernetes exposes an API via the API server.

The kube-apiserver is central to the operation of the Kubernetes
cluster. [All calls]{.underline}, both internal and external traffic,
[are handled via this agen]{.underline}t. All actions are accepted and
validated by this agent, and it is the [only connection to the etcd
database]{.underline}. It validates and configures data for API objects,
and services REST operations. As a result, it acts as a cp process for
the entire cluster, and acts as a frontend of the cluster\'s shared
state.

Starting as a beta feature in v1.18, the Connectivity service provides
the ability to separate user-initiated traffic from server-initiated
traffic. Until these features are developed, most network plugins
commingle the traffic, which has performance, capacity, and security
ramifications.

Client

You can communicate with the API using a local client called kubectl or
you can write your own client and use curl commands.

The [[kube-scheduler]] is forwarded the pod spec for running containers
coming to the API and finds a suitable node to run those containers.

The kube-scheduler uses an algorithm to determine which node will host a
Pod of containers. The scheduler will try to view available resources
(such as volumes) to bind, and then try and retry to deploy the Pod
based on availability and success. There are several ways you can affect
the algorithm, or a custom scheduler could be used instead. You can also
bind a Pod to a particular node, though the Pod may remain in a pending
state due to other settings

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

[[CoreDNS server]] to handle DNS queries, Kubernetes service discovery, and
other functions

The state of the cluster, networking, and other persistent information
is kept in an [[etcd database]], or, more accurately, a b+tree key-value
store. Rather than finding and changing an entry, values are always
appended to the end. Previous copies of the data are then marked for
future removal by a compaction process.

There is a Leader database along with possible followers, or non-voting
Learners who are in the process of joining the cluster. They communicate
with each other on an ongoing basis to determine which will be the
Leader, and determine another in the event of failure

While most Kubernetes objects are designed to be decoupled, a transient
microservice which can be terminated without much concern etcd is the
exception. As it is, the persistent state of the entire cluster must be
protected and secured. Before upgrades or maintenance, you should plan
on backing up etcd.

All nodes

Each node in the cluster runs two processes: a [[kubelet]], which is often a
systemd process, not a container, and [[kube-proxy]].

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

The kube-proxy creates and manages networking rules to expose the
container on the network to other containers or the outside world.

It does so through the use of iptables entries. It also has the
userspace mode, in which it monitors Services and Endpoints using a
random port to proxy traffic via ipvs. A network plugin pod, such as
calico-node, may be found depending on the plugin in use.

The [[container runtime]] is the software that is responsible for running
containers.

Kubernetes supports container runtimes such as , , and any other
implementation of the .

Buldiah

Podman

Containerd

Github containers https://github.com/containers

[[Primitives]]

A [[Pod]] consists of one or more containers which share an IP address,
access to storage and namespace. Typically, one container in a Pod runs
an application, while other containers support the primary application.

Containers in a Pod are started in parallel. As a result, there is no
way to determine which container becomes available first inside a pod.
The use of InitContainers can order startup, to some extent.

[[Init container]], which must complete before app containers will be
started. Should the init container fail, it will be restarted until
completion, without the app container running.

The code below will run the init container until the ls command
succeeds; then the database container will start.

+----------------------------------------------------------------------+
| **spec:**\                                                           |
| ** containers:**\                                                    |
| ** - name: main-app**\                                               |
| ** image: databaseD **\                                              |
| ** initContainers:**\                                                |
| ** - name: wait-database**\                                          |
| ** image: busybox**\                                                 |
| ** command: \[\'sh\', \'-c\', \'until ls /db/dir ; do sleep 5; done; |
| \'\] **                                                              |
+----------------------------------------------------------------------+
|                                                                      |
+----------------------------------------------------------------------+

There is only one IP address per Pod. If there is more than one
container in a pod, they must share the IP. To communicate with each
other, they can either use IPC, the loopback interface, or a shared file
system.

All containers in a pod share the same network namespace.

TO DO: Concept of InitContianers

[[Namespace]]

A segregation of resources, upon which resource quotas and permissions
can be applied. Kubernetes objects may be created in a namespace or
cluster-scoped.

[[How to check what object is namespaced]]

A [[node]] may be a virtual or physical machine, depending on the cluster.
Each node is managed by the and contains the services necessary to run .

To[[ mark a node unschedulable]], run:

  ---------------------------
  kubectl cordon \$NODENAME
  ---------------------------

[[context]]

A combination of user, cluster name and namespace. A convenient way to
switch between combinations of permissions and restrictions. For example
you may have a development cluster and a production cluster, or may be
part of both the operations and architecture namespaces. This
information is referenced from \~/.kube/config.

Controller/operator

They query the current state, compare it against the spec, and execute
code based on how they differ. Various operators ship with Kubernetes,
and you can create your own, as well. A simplified view of an operator
is an agent, or Informer, and a downstream store. Using a DeltaFIFO
queue, the source and downstream are compared.

[[Deployment]]

The default and feature-filled operator for containers is a Deployment.
A Deployment does not directly work with pods. Instead it manages
ReplicaSets. The ReplicaSet is an operator which will create or
terminate pods according to a podSpec. The podSpec is sent to the
kubelet, which then interacts with the container engine to download and
make available the required resources, then spawn or terminate
containers until the status matches the spec.

-   Operator Deployment \>\> manages \>\> operator ReplicaSet

-   Operator ReplicaSet \>\> acts according to \>\> podSpec

-   podSpec \>\> goes to \>\> kubelet

-   kubelet \>\> tells what to do \>\> container engine

-   Container engine \>\> creates, terminates, updates \>\> containers

The [[service]] operator requests existing IP addresses and information from
the endpoint operator, and will manage the network connectivity based on
labels. A service is used to communicate between pods, namespaces, and
outside the cluster

[[[Labels]]]{.underline}

Arbitrary strings which become part of the object metadata

[[[Annotations]]]{.underline}

remain with the object but is not used as a selector

Container engine

Each node could run in a different engine.

Process monitoring

Supervisord is a lightweight process monitor

Kubernetes does not have cluster-wide logging - it uses i.e. Fluentd

TO DO:

TO DO : borg paper

TO DO: check slack

Installation

[[kubeadmin]]

kubeadm, the community-suggested tool from the Kubernetes project, that
makes installing Kubernetes easy and avoids vendor-specific installers.
Getting a cluster running involves two commands: kubeadm init, that you
run on a cp node, and then, kubeadm join, that you run on your worker

Main steps:

-   Run kubeadm init on the control plane node.

-   Create a network for IP-per-Pod criteria.

-   Run kubeadm join on workers or secondary cp nodes.

Kubectl

Alternatives: You can use RESTful calls or the Go language, as well.

configuration file: \$HOME/.kube/config

Includes:

Endpoints

Credentials

Context = combination of a cluster and user credentials

[[Switch between context]]

  -----------------------------------
  kubectl config use-context foobar
  -----------------------------------

[Tools that help in installation]{.underline}

kubespray

In the Kubernetes incubator. It is an advanced Ansible playbook which
allows you to set up a Kubernetes cluster on various operating systems
and use different network providers

Kops

kops (Kubernetes Operations) lets you create a Kubernetes cluster on AWS
via a single command line

Kube-aws

kube-aws is a command line tool that makes use of the AWS Cloud
Formation to provision a Kubernetes cluster on AWS.

Kind

Kind is one of a few methods to run Kubernetes locally. It is currently
written to work with Docker.

Generate yaml from running deployment

  ----------------------------------------------------
  kubectl get deployment nginx -o yaml \> first.yaml
  ----------------------------------------------------

Change cluster (context + user)

  -----------------------------------
  kubectl config use-context foobar
  -----------------------------------

Remember to remove the creationTimestamp ,

resourceVersion , and uid lines. Also remove all the lines including and
after status:

+----------------------------------------------------------------------+
| kubectl -n kube-system exec -it etcd-ip-172-31-62-196 \-- sh -c \\\  |
| \"ETCDCTL_API=3 \--cert=/etc/kubernetes/pki/etcd/peer.crt            |
| \--key=/etc/kubernetes/pki/etcd/peer.key                             |
| \--cacert=/etc/kubernetes/pki/etcd/ca.crt \\\                        |
| etcdctl \--endpoints=https://127.0.0.1:2379 member list\"            |
+----------------------------------------------------------------------+
|                                                                      |
+----------------------------------------------------------------------+

Checking access

+----------------------------------------------------------------------+
| **\$ kubectl auth can-i create deployments**\                        |
| **yes **\                                                            |
| **\$ kubectl auth can-i create deployments \--as bob**\              |
| **no **\                                                             |
| **\$ kubectl auth can-i create deployments \--as bob \--namespace    |
| developer**\                                                         |
| **yes**                                                              |
+----------------------------------------------------------------------+
|                                                                      |
+----------------------------------------------------------------------+

Workload

[[readinessProbe]]

Sometimes, applications are temporarily unable to serve traffic.
Kubernetes provides readiness probes to detect and mitigate these
situations. A pod with containers reporting that they are not ready does
not receive traffic through Kubernetes Services.

[[livenessProbe]]

We also want to make sure it stays in a healthy state. Some applications
may not have built-in checking, so we can use livenessProbes to
continually check the health of a container.

[[startupProbe]]

If kubelet uses a startupProbe, it will disable liveness and readiness
checks until the application passes the test. The duration until the
container is considered failed is failureThreshold times periodSeconds.
For example, if your periodSeconds was set to five seconds, and your
failureThreshold was set to ten, kubelet would check the application
every five seconds until it succeeds, or is considered failed after a
total of 50 seconds.

Networking

Container to container in Pod

Pod networking

There can be[ only one pod network per cluster]{.underline}, although
the CNI-Genie project is trying to

change this. The network must allow container-to-container, pod-to-pod,
pod-to-service, and external-to-service communications.

Prior to initializing the Kubernetes cluster, the network must be
considered and IP conflicts avoided. There are several Pod networking
choices:

[Calico]{.underline}

A flat Layer 3 network which communicates without IP encapsulation, used
in production with software such as Kubernetes, OpenShift, Docker, Mesos
and OpenStack. Viewed as a simple and flexible networking model.

Felix, which is the primary Calico agent on each machine. This agent, or
daemon, is responsible for interface monitoring and management, route
programming, ACL configuration and state reporting.

BIRD is a dynamic IP routing daemon used by Felix to read routing state
and distribute that information to other nodes in the cluster.

[Flannel]{.underline}

A Layer 3 IPv4 network between the nodes of a cluster. Developed by
CoreOS. A flanneld agent on each node allocates subnet leases for the
host.

WeaveNet

It is typically used as an add-on for a CNI-enabled Kubernetes cluster.

Services - [[Pod to Pod]]

Service identifies the pods to transfer traffic by selectors

When service identifies and matches pods labels it register them as its
Endpoints

Service picks one of its Endpoints randomly and sends the traffic to Pod
at targetPort

K8s creates Endpoints as the objects

If service has multiple ports then they need to have name

Headless services are useful for stateful app like DBs bc their pods are
not identical

CocroachDB is good for k8s

[[ClusterIP service]] is accessible within cluster only

[[NodePort service]] is accessible from outside

nodePort must be in range 30000 to 32767

NodePort svc is accessible at IP of node and port of nodePort

NodePort and static port (i.e.30008) is not secure bc it gives the
access to cluster from external app better option is to use Load
Balancer

When [[LoadBalancer service]] is created it automatically creates ClusterIP svc
and NodePort svc

In production it's either Ingress or LoadBalancer service

[[Service operator]]

operator which listens to the endpoint operator to provide a persistent
IP for Pods. Pods have ephemeral IP addresses chosen from a pool. Then
the service operator sends messages via the kube-apiserver which
forwards settings to kube-proxy on every node, as well as the network
plugin.

There are two containers, they share the same namespace and the same IP
address. The IP address is assigned before the containers are started,
and will be inserted into the containers. This IP is set for the life of
the pod.

[[Endpoints]]

The endpoint is created at the same time as the service. Note that it
uses the pod IP address, but also includes a port. The service connects
network traffic from a node high-number port to the endpoint using
iptables with ipvs on the way. The kube-controller-manager handles the
watch loops to monitor the need for endpoints and services, as well as
any updates or deletions.

Service

ClusterIP

ClusterIP which is used to connect inside the cluster, not the IP of the
cluster. As the graphic shows, this can be used to connect to a NodePort
for outside the cluster, an IngressController or proxy, or another
"backend"pod or pods.

TO DO:

The three main networking challenges to solve in a container
orchestration system are:

-   Coupled container-to-container communication (solved by the pod
    concept).

-   Pod-to-pod communication.

-   External-to-pod communication (solved by the services concept, which
    we will discuss later).

Kubernetes expects the network configuration to enable pod-to-pod
communication to be available

TO DO:

TO DO:

TO DO:

TO DO:

While a CNI plugin can be used to configure the network of a pod and
provide a single IP per pod, CNI does not help you with pod-to-pod
communication across nodes.

The requirement from Kubernetes is the following:

-   All pods can communicate with each other across nodes.

-   All nodes can communicate with all pods.

-   No Network Address Translation (NAT).

Basically, all IPs involved (nodes and pods) are routable without NAT.
This can be achieved at the physical network infrastructure if you have
access to it (e.g. GKE). Or, this can be achieved with a software
defined overlay with solutions like:

-   Weave

-   Flannel

-   Calico

Ingress

External service thru NodePort

Create internal svc which is default - ClusterIP

Host is the address (domain name or IP) that is the entry point to the
cluster. It can be the node in the cluster or it can be outside the
cluster that routes to cluster.

Ingress is the set of rules. To implement Ingress we need Ingress
Controller.

In cloud:

In bare metal:

Kubectl cheat sheet

Namespaces

[[Change namespace]]

+----------------------------------------------------------------------+
| kubectl config set-context \--current                                |
| \--namespace=\<insert-namespace-name-here\>\                         |
| \# Validate it\                                                      |
| kubectl config view \--minify \| grep namespace:                     |
+----------------------------------------------------------------------+
|                                                                      |
+----------------------------------------------------------------------+

Check object in and outside namespace

+-----------------------------------------------+
| \# In a namespace\                            |
| kubectl api-resources \--namespaced=**true**\ |
| \# Not in a namespace\                        |
| kubectl api-resources \--namespaced=**false** |
+-----------------------------------------------+
|                                               |
+-----------------------------------------------+

Pod

[[Create new pod]]

  -----------------------------------------------------------
  kubectl run newpod \--image=nginx \--generator=run-pod/v1
  -----------------------------------------------------------

[[Add annotation]]

+----------------------------------------------------------------------+
| **\$ kubectl annotate pods \--all description=\'Production Pods\' -n |
| prod **\                                                             |
| **\$ kubectl annotate \--overwrite pod webpod description=\"Old      |
| Production Pods\" -n prod **\                                        |
| **\$ kubectl -n prod annotate pod webpod description-**              |
+----------------------------------------------------------------------+
|                                                                      |
+----------------------------------------------------------------------+

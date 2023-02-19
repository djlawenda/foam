---
type: definition-note
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/etcd database.md'
---
# etcd database
2023-02-19
Note Created: 2023-02-19

## Definition

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
---
type: definition-note
tags: definition
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/busbox.md'
---
# busbox
Note Created: 2023-03-11

## Definition

### Run command in busybox YAML

Option 1
```yaml
containers:
  - args:
    - /bin/sh
    - -c
    - wget -O /work-dir/index.html http://neverssl.com/online
    image: busybox
```

```yaml
Option 2
containers:
  - image: busybox
    command: ["sh","-c","wget -O /work-dir/index.html http://neverssl.com/online"]
```

### Run command in busybox kubectl
```console
kubectl run box-test --image=busybox --restart=Never -it --rm -- /bin/sh -c "wget -O- IP"
```
-i Keep stdin open on the container in the pod
-t Allocate a TTY for the container in the pod
--rm If true, delete the pod after it exits

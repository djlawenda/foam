---
type: definition-note
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/Init container.md'
---
# Init container
2023-02-19
Note Created: 2023-02-19

## Definition

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
| \'\] **     
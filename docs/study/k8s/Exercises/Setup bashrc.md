---
type: basic-note
foam_template:
    name: basic-note
    description: Basic note
    filepath: 'new/Setup bashrc.md'
---
# Setup bashrc
Note Created: 2023-03-04

## Note

```console
vim ~/.bashrc
```

```yaml
alias k=kubectl
alias v=vim
alias kx= 'kubectl explain'

export drc='--dry-run=client -o yaml'

# goes to the begning of the file
function ns () { kubectl config set-context --current --namespace=$1 }
```


```console
source ~/.bashrc
```
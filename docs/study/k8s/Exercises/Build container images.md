---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Build container images.md'
---
# Build container images
Note Created: 2023-02-26

## Lab 

Build container with podman

## Solution

- Create image file
[[Define container images]]

- Build image
```console
sudo podman build -t simpleapp .
```

- View images
```console
sudo podman images
```

- Run new image from local cashe
```console
sudo podman run localhost/simpleapp
```

- Stop the container
```console
podman stop --latest
```

- Remove container
```console
podman rm --latest
```

## Materials
LFD259 exercise 3.1.7
https://docs.podman.io/en/latest/Introduction.html
https://github.com/containers/podman/blob/main/docs/tutorials/podman_tutorial.md
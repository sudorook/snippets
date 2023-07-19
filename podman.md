# Podman

## Command Tables

### `podman`

Usage: `podman <command>` or `podman container <command>`

Note that `podman list` is not correct. Use `podman ps` or `podman container
list`, instead.

Man page: `man podman-container-<command>`

| Command      | Description                                            |
| :--          | :--                                                    |
| `attach`     | Attach to a running container.                         |
| `checkpoint` | Checkpoint a container.                                |
| `cleanup`    | Clean up network and mount points of a container.      |
| `commit`     | Commit a container into an image.                      |
| `cp`         | Copy files or folders into and out of containers.      |
| `create`     | Create a new container.                                |
| `diff`       | Inspect changes in a container’s filesystem.           |
| `exec`       | Run a process in a container.                          |
| `exists`     | Check if a container exists.                           |
| `export`     | Export a container's filesystem as a TAR archive.      |
| `init`       | Init a container.                                      |
| `inspect`    | Display detailed information on a container.           |
| `kill`       | Send a signal to the primary process in the container. |
| `ps`/`list`  | List all of the containers.                            |
| `logs`       | Fetch logs for a container.                            |
| `mount`      | Mount a container's root filesystem.                   |
| `pause`      | Pause container.                                       |
| `port`       | List port mappings for a container.                    |
| `prune`      | Remove all non-running containers.                     |
| `rename`     | Rename an existing container.                          |
| `restart`    | Restart a container.                                   |
| `restore`    | Restore a checkpointed container.                      |
| `rm`         | Remove a container.                                    |
| `run`        | Run a command in a new container.                      |
| `runlabel`   | Execute the command described by an image label.       |
| `start`      | Start a container.                                     |
| `stats`      | Display statistics for a container.                    |
| `stop`       | Stop a container.                                      |
| `top`        | Display running process in a container.                |
| `unmount`    | Unmount a container's root filesystem.                 |
| `unpause`    | Unpause all the containers in a pod.                   |
| `wait`       | Wait for a container to exit.                          |

### `podman image`

Usage: `podman image <command>`

Man page: `man podman-image-<command>`

| Command   | Description                                             |
| :--       | :--                                                     |
| `build`   | Builds an image using instructions from Containerfiles  |
| `diff`    | Inspects changes in image’s filesystem                  |
| `exists`  | Checks whether an image exists                          |
| `history` | Shows a history of a specified image                    |
| `import`  | Imports a tarball to create a filesystem image          |
| `inspect` | Displays the configuration of an image                  |
| `list`    | Lists all of the images                                 |
| `load`    | Loads image(s) from a tarball                           |
| `mount`   | Mounts an image’s root filesystem                       |
| `prune`   | Removes unused images                                   |
| `pull`    | Pulls an image from a registry                          |
| `push`    | Pushes an image to a registry                           |
| `rm`      | Removes an image                                        |
| `save`    | Saves image(s) to an archive                            |
| `scp`     | Securely copies images to other containers/storage      |
| `search`  | Searches the registry for an image                      |
| `sign`    | Signs an image                                          |
| `tag`     | Adds an additional name to a local image                |
| `tree`    | Prints the layer hierarchy of an image in a tree format |
| `trust`   | Manages container image trust policy                    |
| `unmount` | Unmounts an image’s root filesystem                     |
| `untag`   | Removes a name from a local image                       |

### `podman volume`

Usage: `podman volume <command>`

Man page: `man podman-volume-<command>`

| Command   | Description                                      |
| :--       | :--                                              |
| `create`  | Create a new volume.                             |
| `exists`  | Check if a volume exists.                        |
| `export`  | Export the contents of a volume into a tar ball. |
| `import`  | Untar a tarball into a volume.                   |
| `inspect` | Display detailed information on a volume.        |
| `list`    | List all of the volumes.                         |
| `prune`   | Remove all unused volumes.                       |
| `rm`      | Remove one or more volumes.                      |

### `podman-pod`

Usage: `podman pod <command>`

Man page: `man podman-pod-<command>`

| Command   | Description                                                          |
| :--       | :--                                                                  |
| `create`  | Create a new pod.                                                    |
| `exists`  | Check if a pod exists.                                               |
| `inspect` | Display detailed information on a pod.                               |
| `kill`    | Send a signal to the primary processes of the containers in the pod. |
| `list`    | List all of the pods.                                                |
| `logs`    | Fetch logs for the pod with one or more containers.                  |
| `pause`   | Pause all the containers in a pod.                                   |
| `prune`   | Remove all stopped pods and their containers.                        |
| `restart` | Restart a pod.                                                       |
| `rm`      | Remove one or more pods.                                             |
| `stats`   | Display statistics for the containers in a pod.                      |
| `start`   | Start a pod.                                                         |
| `stop`    | Stop a pod.                                                          |
| `top`     | Display running process in the pod.                                  |
| `unpause` | Unpause all the containers in a pod.                                 |

### `podman-secret`

Usage: `podman secret <command>`

Man page: `man podman-secret-<command>`

| Command   | Description                                          |
| :--       | :--                                                  |
| `create`  | Create a new secret.                                 |
| `inspect` | Display detailed information on one or more secrets. |
| `ls`      | List all available secrets.                          |
| `rm`      | Remove one or more secrets.                          |

## List current host-container port mappings

```sh
podman port -l
```

## Show UID mapping

```sh
podman unshare cat /prof/self/uid_map
```

## Inspect contents of downloaded images

To view the rootfs manifest, run:
```sh
podman inspect <ID>
```

Use tab-completion to get the `<ID>` value reliably.

For lower-level output, such as the container image format, use `skopeo`
instead:
```sh
skopeo inspect --raw <ID>
```

## List containers

To list running containers, run:
```sh
podman ps
```

To include all containers, including those not currently running, try:
```sh
podman ps --all
```

## Remove untagged images

```sh
podman image prune --all
```

Use `--force` as well to remove untagged images that are currently running.
Otherwise, be sure to stop them first.

## Mount and enter images

It is possible to mount container images in a read-only filesystem. Run:
```sh
podman unhare
podman image mount <image>
```

The `unshare` command drops the terminal into a user namespace. This is
required because mounting is not possible in rootless (i.e. user) mode.

When done, unmount as follows:
```sh
podman image unmount <image>
exit
```

The above commands are to be run in the same TTY where `podman unshare` was
run.

## Run containers with non-overlapping user namespaces

Use the `--userns=auto` flag. Doing so will allocate 1024 total UIDs for the
namespace. To override this, run `--userns=auto:size=<SIZE>` where `<SIZE>` is
the number of UIDs (min=1024, max=65536).

Default settings can also be overridden in `/etc/containers/storage.conf`.

```sh
podman run --userns=auto
```

## Pass secrets to containers

To pass a file, for example one containing a password, run:
```sh
podman secret create <name> <path/to/secret>
podman run --secret <name> ...
```

The file will be available within the container at `/run/secrets/<name>`.

To copy the secret to the container environment instead, run `--secret
<name>,type=env` instead.

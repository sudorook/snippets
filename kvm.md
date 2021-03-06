# KVM/libvirt

## Shrink qcow2 files

1. Delete any extraneous files, like package archives, cache, etc.
2. Zero out the virtual disk. You can use bleachbit for this or just pipe
   /dev/zero to a file. (Be sure to delete it after!)
3. Shut down the VM and pass the qcow2 file to the `shrink-vm` script.


## Enable virgl 3d rendering in Virtual Machine Manager

1. Switch the Video mode from QXL to Virtio, and check the 3D acceleration
   option.
2. Switch the SPICE display server listen type to None, and check the OpenGL
   box.
3. Enable `cgroup_device_acl` in /etc/livbirt/qemu.conf and add
   "/dev/dri/renderD128" to the list. Restart the libvirtd.service afterwards.


## Delete image snapshots

To view available snapshots for a particular domain, run:
```
virsh -c qemu:///system snapshot-list --domain <DOMAIN_ID>
```

Delete any of the listed images by:
```
virsh -c qemu:///system snapshot-delete --domain <DOMAIN_ID> <SNAPSHOT_ID>
```


## Delete domains

```
virsh -c qemu:///system undefine <DOMAIN_ID>
```

In the event that non-stock emulation of NVRAM, pass the `--nvram` flag, too.
This is relevant for [OSX-KVM](https://github.com/kholia/OSX-KVM).

```
virsh -c qemu:///system undefine --nvram <DOMAIN_ID>
```

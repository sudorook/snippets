# KVM/libvirt

## Shrink qcow2 files

1. Delete any extraneous files, like package archives, cache, etc.
2. Zero out the virtual disk:
   - Use BleachBit with the 'Free disk space' option checked, or
   - Pipe from /dev/zero to a file. (Be sure to delete it after!)
3. Shut down the VM and pass the qcow2 file to the `shrink-vm` script.

## Enable virgl 3D rendering in Virtual Machine Manager

1. Switch the Video mode from 'QXL' to 'Virtio,' and be sure to check the 3D
   acceleration option.
2. Switch the SPICE display server listen type to 'None', and check the OpenGL
   box.
3. Enable `cgroup_device_acl` in /etc/livbirt/qemu.conf and add
   '/dev/dri/renderD128' to the list. Restart `libvirtd.service` afterwards.

## Delete image snapshots

To view available snapshots for a particular domain, run:

```sh
virsh -c qemu:///system snapshot-list --domain <DOMAIN_ID>
```

Delete any of the listed images by:

```sh
virsh -c qemu:///system snapshot-delete --domain <DOMAIN_ID> <SNAPSHOT_ID>
```

## Delete domains

```sh
virsh -c qemu:///system undefine <DOMAIN_ID>
```

In the event that non-stock emulation of NVRAM, pass the `--nvram` flag, too.
This is relevant for [OSX-KVM](https://github.com/kholia/OSX-KVM).

```sh
virsh -c qemu:///system undefine --nvram <DOMAIN_ID>
```

# Convert OVA file to QCOW2

To convert a VirtualBox image in OVA format to a QCOW2 image compatible with
QEMU, run:

```sh
tar xf <input>
qemu-img convert -O qcow2 <input> <output>
```

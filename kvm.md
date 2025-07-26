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

## Convert OVA file to QCOW2

To convert a VirtualBox image in OVA format to a QCOW2 image compatible with
QEMU, run:

```sh
tar xf <input>
qemu-img convert -O qcow2 <input> <output>
```

## Share a directory between host and guest with `virtiofs`

To share the host directory `<hostdir>` and mount it within a VM at the
directory `<guestdir>`, do the following:

1. From the Virt-Manager GUI, select the 'Show virtual hardware details' icon.
2. In the 'Memory' section, check the 'Enable shared memory' box.
3. Select 'Add Hardware' at the bottom of the UI.
4. In the pop-up, select 'Filesystem.'
5. Select the 'virtiofs' driver (the default).
6. Enter the absolute path of `<hostdir>` in the 'Source path' text box.
7. Enter the target string (e.g. `share`) in 'Target path.' This value **is
   not** the `<guestdir>` path.
8. Confirm the changes (i.e. click 'Finish') and boot the VM.
9. From within the guest, run:

   ```sh
   sudo mount -t virtiofs <share> <guestdir>
   ```

   For clarity, `<share>` is the target string, and `<guestdir>` is the absolute
   path for the mountpoint of the shared directory in the guest.

Additionally, create mount rules in `/etc/fstab` to avoid having to manually
mount the shared filesystem at each boot. Add a rule as follows:

```txt
<share> <guestdir> virtiofs defaults 0 0
```

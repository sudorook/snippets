# KVM/libvirt

## Shrink qcow2 files

1. Delete any extraneous files, like package archives, cache, etc.
2. Zero out the virtual disk. You can use bleachbit for this or just pipe
   /dev/zero to a file. (Be sure to delete it after!)
3. Shut down the VM and pass the qcow2 file to the shrink-vm script.

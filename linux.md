# Linux

## Get UUID for devices

```
lsblk --fs
```

## Get PCI bus for NVME devices

```
sudo dmesg | grep nvme
```

The above command works as long as the dmesg logs have not rolled over, so it
may fail for systems with long uptime.

## No sound over HDMI (Intel CPU)

If audio playback over HDMI does not work (e.g. playback halts or speeds
through files), add `intel_iommu=on,igfx_off` to the `GRUB_CMDLINE_LINUX`
variable in `/etc/default/grub`. Be sure to rebuild the GRUB configuration file
afterwards.

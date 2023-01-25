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

## Get architecture and supported instruction sets

To get the architecture and other information, run:
```
/lib/ld-linux-x86-64.so.2 --help
```

In Debian, run instead:
```
/lib64/ld-linux-x86-64.so.2 --help
```

The `/lib/ld-linux.so.2` symlinked to `/lib32/ld-linux.so.2` will not produce
the same results.

## Monitor directory for modified files

To monitor `MODIFY` events for inodes in a directory `<dir>`, run:
```
inotifywait -m -e modify -r <dir>
```

Omit the `-e modify` flag to monitor all events (`READ`, etc.) instead.

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

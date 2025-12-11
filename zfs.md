# ZFS

## Get the compression ratio of a zpool

Use the `zfs` command-line tool to query the zpool compression ratio:

```bash
zfs get compressratio <zpool>
```

To query a specific dataset instead, run:

```bash
zfs get compressratio <zpool>/<dataset>
```

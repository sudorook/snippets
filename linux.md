# Linux

## Get UUID for devices

```sh
lsblk --fs
```

## Get PCI bus for NVME devices

```sh
sudo dmesg | grep nvme
```

The above command works as long as the dmesg logs have not rolled over, so it
may fail for systems with long uptime.

## No sound over HDMI (Intel CPU)

If audio playback over HDMI does not work (e.g. playback halts or speeds through
files), add `intel_iommu=on,igfx_off` to the `GRUB_CMDLINE_LINUX` variable in
`/etc/default/grub`. Be sure to rebuild the GRUB configuration file afterwards.

## Disable modules at boot

To disable modules, one normally adds a blacklist entry in
`/etc/modprobe.d/<file>`. To disable during boot, though, edit the GRUB command
line and add:

```txt
modprobe.blacklist=<module>
```

## Get architecture and supported instruction sets

To get the architecture and other information, run:

```sh
/lib/ld-linux-x86-64.so.2 --help
```

In Debian, run instead:

```sh
/lib64/ld-linux-x86-64.so.2 --help
```

The `/lib/ld-linux.so.2` symlinked to `/lib32/ld-linux.so.2` will not produce
the same results.

## Monitor directory for modified files

To monitor `MODIFY` events for inodes in a directory `<dir>`, run:

```sh
inotifywait -m -e modify -r <dir>
```

Omit the `-e modify` flag to monitor all events (`READ`, etc.) instead.

## Create on-demand swapfile

To manually add more swap space, do as follows:

```sh
dd if=/dev/zero of=/swapfile bs=1M count=1024 status=progress
chmod 0600 /swapfile
mkswap -U clear /swapfile
swapon /swapfile
```

The above creates 1 GiB of swap space. To create more, increase the value of
`count=#`.

To remove the file, run:

```sh
swapoff /swapfile
rm -f /swapfile
```

## Log all event associated with a device in real time

Install `evtest` and run:

```sh
sudo evtest
```

The program will prompt for a device to watch and will print all events as they
occur.

## Malfunctioning tablet mode detection (Intel)

Check if the system is correctly detecting the device type by running:

```sh
cat /sys/class/dmi/id/chassis_type
```

If the output is **not** 31 or 32 (i.e. laptop), then the `vbtn` kernel module
is malfunctioning. Disable it by adding to a modprobe blacklist
`blacklist intel_vbtn`.

## Reset the TTY

If character rendering is botch by, for example, printing a binary file to
stdout, reset the terminal by running:

```sh
reset
```

## Pass environmental variables to sudo

By default, invoking `sudo` will not copy environment variables to the superuser
shell. To pass specific variables, open the `/etc/sudoers` file (preferably with
`visudo`, and use the `env_keep` flag as follows:

```txt
Defaults env_keep += "EDITOR"
```

The above will pass the `EDITOR` environment variable. Additional ones can be
passed by extending the string, e.g. `"EDITOR DIFFPROG"`.

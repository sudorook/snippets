# dd

## Track transfer progress

### Option 1: dd status=progress

```sh
sudo dd if=source of=dest status=progress
```

### Option 2: kill

#### One-shot

```sh
sudo kill -USR1 $(pgrep ^dd)
```

#### Repeat on 5 second interval

```sh
watch -n5 'sudo kill -USR1 $(pgrap ^dd)'
```

## Backup and compress (in parallel) a disk image

Requires pzstd, pixz, or pigz, depending of the type of compression used.

```sh
sudo dd if=/dev/DEVICE bs=1M status=progress | pzstd > IMAGE.img.zst
```

DEVICE represents the device name, e.g. sda or mmcblk0, and IMAGE is the desired
name to call the compressed image.

## Write (in parallel) compressed backup image to disk

Requires pzstd, pixz or pigz, depending of the type of compression used.

```sh
sudo sh -c "pzstd -d < IMAGE.img.zst > /dev/DEVICE" && sync
```

DEVICE represents the device name, e.g. sda or mmcblk0, and IMAGE is the desired
name to call the compressed image.

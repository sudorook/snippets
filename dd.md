# dd

## Track transfer progress

### Option 1: dd status=progress

```
sudo dd if=source of=dest status=progress
```


### Option 2: kill

One-shot
```
sudo kill -USR1 $(pgrep ^dd)
```

Repeat on 5 second interval
```
watch -n5 'sudo kill -USR1 $(pgrap ^dd)'
```


## Backup and compress (in parallel) a disk image

Requires pixz or pigz, depending of the type of compression used.

```
sudo dd if=/dev/DEVICE bs=1M status=progress | pixz > IMAGE.img.xz
```

DEVICE represents the device name, e.g. sda or mmcblk0, and IMAGE is the
desired name to call the compressed image.


## Write (in parallel) compressed backup image to disk

Requires pixz or pigz, depending of the type of compression used.
```
sudo sh -c "pixz -d < IMAGE.img.xz > /dev/DEVICE" && sync
```

DEVICE represents the device name, e.g. sda or mmcblk0, and IMAGE is the
desired name to call the compressed image.

# SystemD

## Unset the default boot entry

```sh
sudo bootctl set-default ""
sudo bootctl set-timeout ""
```

Alternatively, in the EFI boot menu, press `d` on the default option to unset
it. (`d` toggles the default kernel.)

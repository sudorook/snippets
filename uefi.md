# UEFI

## View existing EFI boot images

```
efibootmgr -v
```

## Delete EFI boot entries

Use `efibootmgr` to view the list of images along with 4-digit list numbers. To
delete entry XXXX:

```
efibootmgr -b XXXX -B
```

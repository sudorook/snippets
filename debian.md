# Debian

## Reinstall GRUB with EFI firmware (from legacy BIOS installation)

From the Debian [GRUBEFIReinstall](https://wiki.debian.org/GrubEFIReinstall)
pages:

1. Boot using UEFI into a live environment.
2. If `/sys/firmware/efi/efivars` is empty, reboot into the rescue system with
   the `efi=runtime` kernel parameter set. Then, mount the EFI variables in the
   live environment by running:

   ```sh
   mount -t efivarfs none /sys/firmware/efi/efivars
   ```

3. Mount the system in the live environment, particularly the root and /boot/efi
   partitions.
4. Bind-mount virtual filesystems:

   ```sh
   for i in /dev /dev/pts /proc /sys /sys/firmware/efi/efivars /run; do
    sudo mount -B "$i" /mnt"$i"
   done
   ```

5. Chroot into the system.
6. Install `grub-efi` (and make sure that `grub-pc-bin` remains installed).
7. Re-install GRUB:

   ```sh
   grub-install --target-i386-pc /dev/<DEVICE> --recheck
   grub-install /dev/<DEVICE> --bootloader-id=<ID> --recheck
   ```

   Check that the EFI directory (`/boot/efi`) is not populated.

8. Update the GRUB config file by running `update-grub`.
9. Exit the chroot, unmount, and reboot.

**Note:** If the base system is LUKS-encrypted, make sure the device name used
when unlocking is _the same_ as the one used when unlocking during the normal
boot sequence.

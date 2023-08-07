# AUR

## Update `sha256sums` automatically

After updating the version numbers and/or URLs, run:

```sh
updpkgsums
```

This will download the source file, compute the SHA256 checksum, and update the
array in the PKGBUILD file.

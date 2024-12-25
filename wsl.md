# Windows Subsystem for Linux

## Set available RAM

From the host, edit the file `c:\Users\<user>\.wslconfig` and append:

```conf
[wsl2]
memory=<size>
```

## Export WSL image as backups

To create backups of existing WSL images, first ensure that WSL is not running
(`wsl --shutdown`).

Then, run:

```ps1
wsl --export <NAME> "$env:userprofile\WSL\Images\<NAME>_$(date -f yyyyMMdd_HHmmss).tar"
```

## Enable `interop` in WSL for file-sharing between host and guest

To make files in the host and guest accessible from within and outside the
virtualised environment, respectively, set the following in `/etc/wsl.conf`:

```txt
[interop]
enabled=True
```

Note that this will reduce performance within the image.

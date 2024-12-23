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

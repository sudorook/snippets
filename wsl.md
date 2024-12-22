# Windows Subsystem for Linux

## Export WSL image as backups

To create backups of existing WSL images, first ensure that WSL is not running
(`wsl --shutdown`).

Then, run:

```ps1
wsl --export <NAME> "$env:userprofile\WSL\Images\<NAME>_$(date -f yyyyMMdd_HHmmss).tar"
```

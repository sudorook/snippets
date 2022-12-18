# Windows

## Zero out free space

First, download SDelete. Then, unzip the archive and open the containing folder
in the command prompt (enter `cmd` in the file manager toolbar).

From the prompt, run:
```
sdelete.exe -z <DRIVE>
```

`<DRIVE>` corresponds to the drive to wipe, which in most cases for one's
system drive is `C:`. Be sure to use `-z` and *not* `-c`, as the former simply
zeros out the drive and the latter writes random data and then zeros it out.

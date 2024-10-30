# Windows

## Zero out free space

First, download [SDelete](https://download.sysinternals.com/files/SDelete.zip).
Then, unzip the archive and open the containing folder in the command prompt
(enter `cmd` in the file manager toolbar).

Alternatively, use WinGet:

```ps1
winget install Microsoft.Sysinternals.SDelete
```

From the prompt, run:

```ps1
sdelete.exe -z <DRIVE>
```

`<DRIVE>` corresponds to the drive to wipe, which in most cases for one's system
drive is `C:`. Be sure to use `-z` and _not_ `-c`, as the former simply zeros
out the drive and the latter writes random data and then zeros it out.

## Convert MBR partition to GPT

Open the command prompt as administrator and go to the `Windows/System32`
directory:

```ps1
cd \Windows\System32
```

Run `mbr2gpt.exe`, first to check whether the conversion is possible and again
to actually perform it:

```ps1
mbr2gpt /validate /AllowFullOS
mbr2gpt /convert /AllowFullOS
```

Should there be an error message toward the end of the program stating
`Failed to update ReAgent.xml, please try to manually disable and enable WinRE`,
disable and enable by running:

```ps1
reagentc /disable
reagentc /enable
```

This only applies if a Windows recovery environment exists. If not, ignore the
error.

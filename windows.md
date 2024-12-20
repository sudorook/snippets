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

## Add a `Ctrl+Alt+t` shortcut for opening Windows Terminal

1. Locate a Windows Terminal .exe file on the system. It will be named 'wt.exe.'
   One place to look is
   `c:\Users\<username>\AllData\Local\Microsoft\WindowsApps\wt.exe`.
2. Open the directory containing wt.exe in File Explorer. Right-click the wt.exe
   file and select 'Create shortcut' in the 'Show more options' sub-menu.
3. Move the new `wt - Shorcut.exe` file to the Desktop folder.
4. Right-click the Desktop shortcut and enter the 'Properties' menu.
5. In the 'Shortcut key' field, enter `Ctrl+Alt+t`.

## Access WSL files from Git Bash on the host

A WSL file's path for Git Bash is `//wsl.localhost/<name>/home/....`, where
`<name>` is the name of the Linux distribution (e.g. `Ubuntu`). See`wsl --list`
for the names currently available.

## Windows terminal

### Default shortcuts

- Open a new vertical pane: `Ctrl+Alt++`
- Open an new horizontal pane: `Ctrl+Alt+-`
- Switch pane focus: `Alt+<arrow>`
- Resize a pane: `Alt+Shift+<arrow>`
- Close a pane: `Ctrl+Shift+w`
- Open command palette: `Ctrl+Shift+p`
- Duplicate a pane: `Alt+Shift+d`
- Zoom a pane: selection 'Toggle pane zoom` from the command palette.

## Find license key

To obtain the license key for a registered installation of Windows, run the
following int he command prompt (as administrator):

```ps1
wmic path softwarelicensingservice get OA3xOriginalProductKey
```

Alternatively, run in Powershell as administrator:

```powershell
$(Get-WmiObject -query 'select * from SoftwareLicensingService').OA3xOriginalProductKey
```

The above commands only work for OEM keys. Otherwise, it returns empty. For
other cases, download and run Magical Jellybean KeyFinder. The activation key is
the string in the 'CD Key' field.

## Unregister a license key

To, uninstall the current product key from Windows and put it into an unlicensed
state, run:

```ps1
slmgr /upk
```

Then, ensure that the product key is removed from the registry:

```ps1
slmgr /cpky
```

Lastly, reset the Windows activation timers so that new users are prompted to
activate Windows:

```ps1
slmgr /rearm
```

## Extract product keys (from Linux)

For OEM keys, use the `chntpw` tool:

```ps1
sudo chntpw -e </path/to/windows>/Windows/System32/config/SOFTWARE
```

Replace `<path/to/windows>` with the absolute path to where the drive is
mounted. The `SOFTWARE` file may be lower case.

```ps1
dpi \Microsoft\Windows NT\CurrentVersion\DigitalProductId
```

Note that for the product key must be deactivated on the original device for the
key to used on another.

## Reset Windows 10 without login

1. From the login screen, navigate to the reset option on the bottom-right menu.
2. Press and hold `Shift`.
3. Select `Restart`.
4. Release `Shift` once the 'Please wait...' message is displayed.

This will open up a restart menu. From here, select the 'Troubleshooting'
option, which will reveal a menu where the device may be factory reset.

## View battery charge/discharge status

```ps1
gwmi -Class batterystatus -Namespace root\wmi
```

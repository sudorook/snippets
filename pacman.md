# Pacman (Arch Linux)

## List the files installed by a package

```
pacman -Ql <package>
```

Alternatively, for a package archive that is not yet installed (e.g. `pacman
-Sw ...`), run:

```
pacman -Qlp <file>
```

## Find out what program implements a command

```
pacman -Qo <command>
```

Note that this only applies to *available* commands from installed packages.
Pacman won't search all the available packages.

`pacman -Qo` can also be used on file paths to reveal which package installed
it.

## Overwrite package files

If a package is installed incorrectly or the installation is broken, overwrite
existing files from the repository package. Run:

```
sudo pacman -S --overwrite "*" <package>
```

Be mindful of pacsave files. They will be given preference during installation
over the files shipped in packages.

## Update keys in live environment

If attempts to install packages result in PGP signature errors, update the
keyring:
```
pacman -Sy archlinux-keyring
```

Should this not work, reset all the GPG keys and restart the GPG agent.
```
killall gpg-agent
rm -r /etc/pacman.d/gnupg/
pacman-key --init
pacman-key --populate archlinux
```

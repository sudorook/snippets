# Pacman (Arch Linux)

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

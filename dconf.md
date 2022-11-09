# dconf / gsettings

## Change default terminal application

Change the default terminal in GNOME or Cinnamon:
```
gsettings set org.cinnamon.desktop.default-applications.terminal exec '<TERMINAL>'
gsettings set org.cinnamon.desktop.default-applications.terminal exec-arg '<ARGS>'
```

```
gsettings set org.gnome.desktop.default-applications.terminal exec '<TERMINAL>'
gsettings set org.gnome.desktop.default-applications.terminal exec-arg '<ARGS>'
```

For most cases, `<ARGS>` can be left untouched. The `<TERMINAL>` variable can
be the name of the executable or its absolute path. Additionally, for Debian,
one can instead set the default terminal to `/usr/bin/x-terminal-emulator`, a
symlink to the default terminal that can be set via `update-alternatives`.

**Note:** Ror desktop applications (programs run through their `.desktop`
files), use of `gnome-terminal` is hard-coded. One way to circumvent this is to
symlink the desired terminal to `/usr/local/bin/gnome-terminal`.

### Restore default terminal

To restore the terminal settings to the default terminal (likely GNOME
Terminal):
```
gsettings reset-recursively org.cinnamon.desktop.default-applications.terminal
gsettings reset-recursively org.gnome.desktop.default-applications.terminal
```

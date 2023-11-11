# meson

## Enable unity builds

Run:

```sh
meson setup _build --unity on
```

Here, `_build` is the build directory.

## Install in a custom directory

To change the default installation path (`/usr`), such as `~/.local`, use the
`--prefix` flag as follows.

```sh
meson setup --prefix=<PATH> ...
```

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

## Uninstall a compiled program

To uninstall a meson-installed program, run:

```sh
ninja -C <build> uninstall
```

where `<build>` is the build directory.

Alternatively, run `ninja uninstall` inside the build directory itself. (It is
the directory where the `build.ninja` file is located.)

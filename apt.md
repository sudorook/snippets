# Apt, apt-get, aptitude, and dpkg

## Find which program installed package as a dependency

```sh
aptitude why <package>
```

## List contents of installed package

```sh
dpkg -L <package>
```

Absolute paths are not needed.

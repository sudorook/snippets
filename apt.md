# Apt, apt-get, aptitude, and dpkg

## Find the package that own a file
```
dpkg-query -S <absolute path>
```

This command can be extended to show which packages installed any given command
`CMD`. Combine `dpkg-query` with `which` as follows:
```
dpkg-query -S $(which <CMD>)
```

## Find which program installed package as a dependency

```sh
aptitude why <package>
```

## List contents of installed package

```sh
dpkg -L <package>
```

Absolute paths are not needed.

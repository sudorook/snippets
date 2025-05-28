# Apt, apt-get, aptitude, and dpkg

## Find the package that own a file

```sh
dpkg-query -S <absolute path>
```

This command can be extended to show which packages installed any given command
`CMD`. Combine `dpkg-query` with `which` as follows:

```sh
dpkg-query -S $(which <CMD>)
```

## Find which program installed package as a dependency

```sh
aptitude why <package>
```

To query the program that installed a file, combine with `dpkg-query` as
follows:

```sh
aptutude why $(dpkg-query -S $(which <CMD> | cut -d":" -f1))
```

## List contents of installed package

```sh
dpkg -L <package>
```

Absolute paths are not needed.

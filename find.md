# find

## Replace $'\n' with ' ' in file names

```sh
find . -type f -exec rename -a $'\n' ' ' {} \;
```

Note, on Debian, `rename` installed by the `util-linux` meta-package is called
`rename.ul`. The `rename` program in its repos is a Perl script with an
incompatible API.

## Exclude path in `find` results

```sh
find <start path> -not -path "<exclude path>"
```

## Prune all Git directories

```sh
find . -type d -name ".git" -exec sh -c 'DIR="$(dirname "${1}")" && echo "${DIR}" && git -C "${DIR}" gc --prune=now --aggressive && echo' sh {} \;
```

## Delete `node_modules` directories

```sh
find . -type d -name "node_modules" -prune -exec rm -rvf {} \;
```

## Restore bak files

```sh
find . -type f -name "*.bak" -exec bash -c 'newfile="$(echo "${1}" | sed -e "s/_[0-9]\+-[0-9]\+\.bak$//g")"; mv "${1}" "${newfile}"' bash {} \;
```

## Find broken symlinks

```sh
find <path> -type l -exec test ! -e {} \; -print
```

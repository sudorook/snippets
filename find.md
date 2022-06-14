# find

## Replace $'\n' with ' ' in file names

```
find . -type f -exec rename -a $'\n' ' ' {} \;
```

## Exclude path in `find` results

```
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
find . -type f -name "*.bak" -exec bash -c 'newfile="$(echo "${1}" | sed -e "s/_.*\.bak$//g")"; mv "${1}" "${newfile}"' bash {} \;
```

## Find broken symlinks

```
find <path> -type l -exec test ! -e {} \; -print
```

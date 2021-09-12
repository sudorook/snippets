# Bash

## Replace $'\n' with ' ' in file names

```
find . -type f -exec rename $'\n' ' ' {} +
```

## Exclude path in `find` results

```
find <start path> -not -path "<exclude path>"
```

## Find broken symlinks

```
find <path> -type l -exec test ! -e {} \; -print
```

# Bash

## Replace $'\n' with ' ' in file names

```
find . -type f -exec rename $'\n' ' ' {} +
```

## Exclude path in `find` results

```
find <start path> -not -path "<exclude path>"
```

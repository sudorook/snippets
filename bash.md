# Bash

## Replace $'\n' with ' ' in file names

```
find . -type f -exec rename $'\n' ' ' {} +
```

## Exclude path in `find` results

```
find <start path> -not -path "<exclude path>"
```


## Undo add-subtitles

```
for file in *.bak; do mv "$file" "${file%.*}"; done
```


## Upgrade Julia packages from the command line

```
julia -e "Pkg.update(); using Gadfly"
```

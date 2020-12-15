# Bash

## Replace $'\n' with ' ' in file names

```
find . -type f -exec rename $'\n' ' ' {} +
```


## Undo add-subtitles

```
for file in *.bak; do mv "$file" "${file%.*}"; done
```


## Upgrade julia packages from the command line

```
julia -e "Pkg.update(); using Gadfly"
```

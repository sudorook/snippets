1. Undo add-subtitles:

```
for file in *.bak; do mv "$file" "${file%.*}"; done
```


2. Upgrade julia packages:

```
julia -e "Pkg.update(); using Gadfly"
```

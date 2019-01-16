# LaTeX

## Change local default texmf directory

Edit the texmf.cnf file (use `kpsewhich texmf.cnf` to find the path) to change
the `TEXMFHOME` variable:

```
TEXMFHOME = ~/.texmf
```


## Set encoding to UTF-8

When compiling tex files with UTF-8 (non-latin1) characters, set the following
as the first line in the file:

```
%!TEX encoding = UTF-8 Unicode
```

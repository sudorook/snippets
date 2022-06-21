# R

## Install list of packages from command line

First, make sure that the `R_LIBS_USER` environment variable is set, that the
directory it specifies exists, and that the current user has write permissions
for it. Then, run:
```R
Rscript -e "pkg <- readLines(\"<list>\"); install.packages(pkg, lib=\"${R_LIBS_USER}\", repo='https://cloud.r-project.org/')"
```

`<list>` is a file containing a list of packages. The repo variable can also be
changed to the desired package mirror.

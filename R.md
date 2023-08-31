# R

## Install list of packages from command line

First, make sure that the `R_LIBS_USER` environment variable is set, that the
directory it specifies exists, and that the current user has write permissions
for it. Then, run:

```sh
Rscript -e "pkg <- readLines(\"<list>\"); install.packages(pkg, lib=\"${R_LIBS_USER}\", repo='https://cloud.r-project.org/')"
```

`<list>` is a file containing a list of packages. The repo variable can also be
changed to the desired package mirror.

## Update packages

To update all packages from the CRAN repos, run:

```R
update.packages()
```

To update a specific package instead of all of them, run:

```R
update.packages(oldPkgs=<list>)
```

where `<list>` is either a string for a single package of list (`c()`) for more
than one.

To view any out-of-date packages, use:

```R
old.packages()
```

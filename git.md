# Git

## Create and apply patches

To create a patch against a branch, run:
```
git format-patch <branch>
```

This will generate patch files at the base of the repository. Alternately, use
`HEAD~#` or `<sha256>` instead of the branch name.

To apply the patch and add the commit to the Git history, run:
```
git am < <path/to/file.patch>
```

## Get number of commits in repository

```
git rev-list --count --all
```

## Cleanup local repository

```
git gc --prune=now --aggressive
```

To find and prune all Git directories (starting from the current working
directory), run:
```
find . -type d -name ".git" -exec sh -c 'DIR="$(dirname "${1}")" && git -C "${DIR}" gc --prune=now --aggressive' sh {} \;
```

## Push a branch to a differently named remote branch

```
git push <remote> <localbranch>:<remotebranch>
```

## Push a subset of commits to the repository

To only some commits and not the full tree, use:
```
git push <remote> <localbranch>~<# number commits behind HEAD>:<remotabranch>
```

For example, to push all but the last 5 commits on master to remote master, run:
```
git push origin master~5:master
```

## Pull from a differently named remote branch

```
git pull <remote> <remotebranch>:<localbranch>
```

## Remove a file from the git history

```
git filter-branch -f --index-filter \
  "git rm -rf --cached --ignore-unmatch <REGEX>" \
  --prune-empty --tag-name-filter cat -- --all

rm -rf .git/refs/original/
git reflog expire --expire=now --all
git gc --aggressive --prune=now
```

Replace `<REGEX>` with a pattern to match the file(s) to remove. The pattern
may be a simple, hard-coded path. Then, force push to the remote repository
(`git push -f origin master`).


## Repack a repository

Some repositories have `.pack` file so large that they cannot fit in RAM when
running `git gc`. It is possible to re-pack them so that they fit within file
size constraints. For example, run:

```
git repack -a -d --window-memory 100M --max-pack-size 1G
```

Adjust the above size thresholds as needed.

## Create a compressed release archive

To release an archived version of the source code (without the Git metadata and
version history), run:
```
git archive --prefix=<prefix> -o <output> <ID>
```

The `prefix` (optional) is a string appended to every file in the archive. If
not given, extracting the resulting archive will empty the contents on the base
of the repository in the currently working directory. Using `--prefix` allows
files to extracted to a directory instead. Be sure to include a '/' in the
prefix string.

`<output>` is the name of the archive. Specify the type of compression used
with the `--format` parameter. (Run `git archive --list` to see a list of the
available formats.)

`<ID>` refers to the branch, tag, commit hash to archive.


## Updating all submodules

Update each Git submodule to their respecting remote HEAD by running:
```
git pull --recurse-submodules
```

(Add `--jobs=...` if you want downloads to run in parallel.)

Note that if the submodules have not already been initialized, run instead:
```
git submodule update --init --recursive
```

One can also use the `foreach` option to execute commands or a shell script in
each submodule. The following example simply pulls from the master branch:
```
git submodule foreach git pull origin master
```

## Specify Git commit timestamps

To set a desired timestamp, alter the `GIT_AUTHOR_DATE` and
`GIT_COMMITTER_DATE` timestamps in the environment.
```sh
GIT_AUTHOR_DATE="<date>" GIT_COMMITTER_DATE="<date>" git commit ...
```

Look to the output format of the `date` command to understand how `<date>`
should be formatted.

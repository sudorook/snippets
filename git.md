# Git

## Get path to root of Git repository

```sh
git rev-parse --show-toplevel
```

## Create and apply patches

To create a patch against a branch, run:

```sh
git format-patch <branch>
```

This will generate patch files at the base of the repository. Alternately, use
`HEAD~#` or `<sha256>` instead of the branch name.

To apply the patch and add the commit to the Git history, run:

```sh
git am < <path/to/file.patch>
```

To create and apply patches for changes that has not yet been committed, instead
use:

```sh
git diff > patch.txt
```

and, to apply patches:

```sh
git apply patch.txt
```

## Get number of commits in repository

```sh
git rev-list --count --all
```

## Cleanup local repository

```sh
git gc --prune=now --aggressive
```

To find and prune/compact all Git directories (including submodules), run:

```sh
find . -type d -name ".git" -exec sh -c 'DIR="$(git -C "$(dirname "${1}")" rev-parse --show-toplevel)" && git -C "${DIR}" gc --prune=now --aggressive && git -C "${DIR}" submodule foreach git gc --prune=now --aggressive' sh {} \;
```

## Push a branch to a differently named remote branch

```sh
git push <remote> <localbranch>:<remotebranch>
```

## Push a subset of commits to the repository

To only some commits and not the full tree, use:

```sh
git push <remote> <localbranch>~<number of commits behind HEAD>:<remotabranch>
```

For example, to push all but the last 5 commits on master to remote master, run:

```sh
git push origin master~5:master
```

Alternatively, one can send commits up through a specific SHA number instead of
the number of commits behind HEAD. The format is:

```sh
git push <remote> <SHA>:<remotebranch>
```

## Pull from a differently named remote branch

```sh
git pull <remote> <remotebranch>:<localbranch>
```

## Remove a file from the git history

```sh
git filter-branch -f --index-filter \
  "git rm -rf --cached --ignore-unmatch <REGEX>" \
  --prune-empty --tag-name-filter cat -- --all

rm -rf .git/refs/original/
git reflog expire --expire=now --all
git gc --aggressive --prune=now
```

Replace `<REGEX>` with a pattern to match the file(s) to remove. The pattern may
be a simple, hard-coded path. Then, force push to the remote repository
(`git push -f origin master`).

## Repack a repository

Some repositories have `.pack` file so large that it cannot fit in RAM when
running `git gc`. It is possible to re-pack them so that they fit within file
size constraints. For example, run:

```sh
git repack -a -d --window-memory 100M --max-pack-size 1G
```

Adjust the above size thresholds as needed.

## Create a compressed release archive

To release an archived version of the source code (without the Git metadata and
version history), run:

```sh
git archive --prefix=<prefix> -o <output> <ID>
```

The `prefix` (optional) is a string appended to every file in the archive. If
not given, extracting the resulting archive will empty the contents on the base
of the repository in the currently working directory. Using `--prefix` allows
files to extracted to a directory instead. Be sure to include a '/' in the
prefix string.

`<output>` is the name of the archive. Specify the type of compression used with
the `--format` parameter. (Run `git archive --list` to see a list of the
available formats.)

`<ID>` refers to the branch, tag, commit hash to archive.

## Updating all submodules

Update each Git submodule to their respecting remote HEAD by running:

```sh
git pull --recurse-submodules
```

(Add `--jobs=...` if you want downloads to run in parallel.)

Note that if the submodules have not already been initialized, run instead:

```sh
git submodule update --init --recursive
```

One can also use the `foreach` option to execute commands or a shell script in
each submodule. The following example simply pulls from the master branch:

```
git submodule foreach git pull origin master
```

## Specify Git commit timestamps

To set a desired timestamp, alter the `GIT_AUTHOR_DATE` and `GIT_COMMITTER_DATE`
timestamps in the environment.

```sh
GIT_AUTHOR_DATE="<date>" GIT_COMMITTER_DATE="<date>" git commit ...
```

Look to the output format of the `date` command to understand how `<date>`
should be formatted.

## Merging stashed and remote changes

Normally, to pull remote changes while preserving local changes, stash first and
pull as follows:

```sh
git stash
git pull origin master
git stash pop
```

In the event of merge conflicts, the `git stash pop` command will fail. Use
`git mergetool` to resolve the merge conflicts that arise. Once this is done,
though, the stash will still exist. This is because the `git stash pop` command
is a combination of `git stash apply` and `git stash drop`. Failure (i.e. merge
conflicts) of the former prevents the latter from running.

Therefore, to drop the stash after the merge conflicts are resolved, run:

```sh
git stash drop
```

## Rename a branch

To rename a branch and migrate its corresponding reflog, run:

```sh
git branch -m <oldname> <newname>
```

Use `-M` instead of `-m` to force the renaming to happen should the `<newname>`
branch already exist.

## Clone specific tags or branches

Use the `-b` (`--branch`) flag when cloning to get a specific branch:

```sh
git clone <url> -b <branch>
```

The `-b` flag will also take tags and detaches from HEAD.

## Set default branch for new repositories

Edit the global .gitconfig file by running:

```sh
git config --global init.defaultBranch master
```

## Push simultaneously to multiple remotes

It is possible to configure a repository to push to multiple remotes in a single
`push` command by adding multiple push URLs to a single remote. For example, add
multiple URLs to `origin`:

```sh
git remote add origin "<origin-url>"
git remote set-url --add --push origin "<origin-url>"
git remote set-url --add --push origin "<mirror-url-1>"
git remote set-url --add --push origin "<mirror-url-2>"
```

This will result in a single fetch URL (`<origin-url>`) and three push URLs
(`<origin-url>`, `<mirror-url-1>`, and `<mirror-url-2>`).

To remote a URL from the push list for `origin`, run:

```sh
git remote set-url --delete --push origin "<url>"
```

## Push all branches

To push all branches to the corresponding remote branches in a single command,
run:

```sh
git push origin :
```

For this to actually push all branches, through, they need to actually be mapped
from local to remote repositories. There are several ways to do this. Two
options below:

```sh
git push --set-upstream <remote> <branch>
```

```sh
git branch --set-upstream-to=<remote>/<branch> <branch>
```

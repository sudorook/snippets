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
git gc --prune --aggressive
```

To find and prune all Git directories (starting from the current working
directory), run:
```
find . -type d -name ".git" \
  -exec bash -c 'DIR="$(dirname "${1}")"; git -C "${DIR}" gc --prune=now --aggressive' bash {} \;
```

## Push a branch to a differently named remote branch

```
git push <remote> <localbranch>:<remotebranch>
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

# Git

## Get number of commits in repository

```
git rev-list --count --all
```

## Cleanup local repository

```
git gc --prune --aggressive
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

Then, force push to the remote repository (`git push -f origin master`). The
regex can also be a simple path.

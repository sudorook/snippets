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

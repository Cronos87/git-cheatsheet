# Useful GIT’s commands

## Get filenames diff between two branches or tag
```bash
git diff --name-only tag..master
```

## Reset and conserve files
```bash
git reset --soft HEAD~n
```

**n** is the number of commit to reset.

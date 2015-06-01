# Useful GIT’s commands

### Get filenames diff between two branches or tag
```bash
git diff --name-only tag..master
```

### Reset and conserve files
```bash
git reset --soft HEAD~n
```

**n** is the number of commit to reset.

## Make a patch

Useful commands I use for creating a patch for clients.

### Create a zip from a diff filenames
```bash
git diff --name-only tag..master | xargs zip name.zip
```

This command will make a zip file from the diff.

If I want to delete a part of the path I will do this:

```bash
git diff --name-only tag..master | sed "s/project\///" | xargs zip name.zip
```

**project** is the part of the path I want to delete.

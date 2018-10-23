# Useful GIT’s commands

### Get filenames diff between two branches or tag

```bash
git diff --name-only tag..master
```

### Reset and conserve files

This command is useful if you want to cancel your last **n** commits and conserve all the modifications.

```bash
git reset --soft HEAD~n
```

**n** is the number of commit to reset.

### Revert merge and go back to the HEAD version

```bash
git reset --merge ORIG_HEAD
```

## Make a patch

Useful commands you use for creating a patch for clients.

### Create a zip from a diff filenames

```bash
git diff --name-only tag..master | xargs zip name.zip
```

This command will make a zip file from the diff.

If you want to delete a part of the path you have to do this:

```bash
git diff --name-only tag..master | sed "s/project\///" | xargs zip name.zip
```

**project** is the part of the path you want to delete.

## Branches

### Create a branch

```bash
git checkout -b branch_name
```

### Switch to a branch

```bash
git checkout branch_name
```

### Merge a branch

```bash
git merge branch_name
```

This command will merge **branch_name** into your current branch.
For exemple, if you are on the master, this will merge the selected branch into master.

### Delete a merged branch

```bash
git branch -d branch_name
```

### Delete a branch even not merged

```bash
git branch -D branch_name
```

### Delete a branch on origin

```bash
git push origin :branch_name
```

### Reset a branch to the origin state

```bash
git fetch origin
git reset --hard origin/branch_name
```

### Show merged branches

```bash
git branch --merged
```

Show merged branches in the current branch.

### Show unmerged branches

```bash
git branch --no-merged
```

Show unmerged branches in the current branch.

## Tag

### Create a tag

```bash
git tag tag_name
```

### Push a tag to origin

```bash
git push origin tag_name
```

### Delete a tag

```bash
git tag -d tag_name
```

### Delete a tag on origin

```bash
git push origin :tag_name
```

## Divers

### Order tags by creation date

```bash
git config --global tag.sort version:refname
```

### Add an empty directory

To add an empty directory, you have to create an empty file named `.gitkeep` and then commit this file.

### Find who create a file

```bash
git log --diff-filter=A -- filepath
```

### Remove all same files

```bash
find . -name .DS_Store -print0 | xargs -0 git rm -f --ignore-unmatch
```

# Three Trees
* HEAD: last commit tree
* index: next commit tree
* working dir: sandbox tree

# CHECKOUT
## Of sha/branches
```
git checkout == git checkout HEAD
git checkout <branch || commit>
git checkout [[-b] <new_branch>] [<start point>]
```

Update the HEAD to ```branch``` or ```commit``` or ```new_branch```, then sync the index, then
sync the working dir.  
**Safe**: don't throw away local changes.

## Of file paths
```
git checkout <paths> == git checkout <index> <paths>
git checkout <tree-ish> <paths>
git checkout [--ours || --theirs || -m] <paths>
git checkout [-p|--patch] [<paths>]
```

Update ```paths``` in working dir and index from ```tree-ish``` (```index``` if no ```tree-ish``` given).
Update ```paths``` in working dir from index with ours or theirs version of
conflicted file or restore the conflict (-m).
Update ```paths``` in working dir from index patch by patch

# RESET
```
git reset          == git reset HEAD
git reset <commit> == git reset --mixed <commit>
git reset [--hard || --mixed || --soft] <commit>
```

* soft
 * reset HEAD to ```commit```
* mixed
 * reset HEAD and index to ```commit``` (unstage)
* hard
 * reset HEAD and index and working dir to ```commit``` (wipe all changes)
 * rough equivalent of an unsafe checkout

## Of file paths
```
git reset [-p] <commit> [--] <paths>
```
reset <paths> in index from HEAD


# ADD
```
git add <filepattern>
git add [-i | -p | -u | -A | -e] [<filepattern>]
```
Add files to the index
* filepattern  = matched against the working dir. Directories are treated recursively
* ```-u```           = filepattern against index (only already staged files, good for deletions)
* ```-A```           = filepattern against index and working dir (all files, good for deletions and renames)
* ```-i``` | ```-p``` | ```-e``` = add differences between working dir and index selectively


# COMMIT
```
git commit
```
Create a commit from index

```
git commit [-o] <file>
```
Commit a file in working dir directly, without committing the index (leaving it staged)


# RM
```
rm <file>
```

Remove file from index and working dir

```
rm --cached <file>
```
Remove file from index

# CLEAN
Removes recursively untracked files from the working dir


# OPTIONS
```--work-tree=<path>``` sets the working dir for this command
```--git-dir=<path>``` sets the git dir for this command

# ENV
* GIT_INDEX_FILE
* GIT_WORK_TREE
* GIT_OBJECT_DIRECTORY


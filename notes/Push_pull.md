# PUSH
```
git push                    == git push <branch.remote || origin>
git push <remote>           == git push <remote> <remote.<name>.push || :>
git push <remote> <refspec> [<refspec> ...]
```
Push references to a remote

# FETCH
```
git fetch                   == git fetch <branch.remote || origin>
git fetch <remote>          == git fetch <remote> <remote.<name>.fetch || :>
git fetch <remote> <branch> == git fetch <remote> <branch>:
git fetch <remote> <refspec> [<refspec> ...]
```
Fetch references from a remote

# PULL
```
git pull
git pull <remote>
git pull <remote> <refspec> [<refspec> ...]
```
Fetch + merge into ```branch.<current branch>.remote``` or ```current branch```

# MERGE
```
merge == merge <branch.<current branch>.merge if merge.defaultToUpstream>
merge <commit> [<commit> ...] (merges all commits into current branch)
```

# REFSPEC
## fetch
updates ```dst``` on local to ```src``` on remote

```
+<src>:<dst>

<src>        == <src>:
:<dst>       == HEAD:<dst>
:            == HEAD:
<src>:       == fetch <src>, update FETCH_HEAD
<src>:<dst>  == fetch <src> into <dst>, update FETCH HEAD

+ = ok no fast-forward
src = ref
dst = ref
```

## push
Updates ```dst``` on remote to ```src``` on local

```
+<src>:<dst>

<src>  == <src>:<src>
:<dst> == delete <dst> (put void into dst)
:      == update matching branches (same name on both local and remote)

+ = ok no fast-forward
src = ref || sha
dst = ref
```

# REMOTE
* ssh:// url
* http:// url
* ftp:// url
* git:// url
* rsync:// url
* file:///path url
* /path
```
[remote "remote name"]
url = <remote url>
fetch = <refspecs when fetching>
```

# TRACKING BRANCH
```
[branch "name"]
remote = remote>
merge = <ref>
```

# Git Merge or Rebase?

### 1. You're working on master
```
* e159214 (HEAD, origin/master, origin/HEAD, master) goodbye file
* 2c0e242 hello file
```

### 2. You make a couple of commits
```
* 54b943f (HEAD, master) sadder goodbye
* 9e2c485 happier hello
* e159214 (origin/master, origin/HEAD) goodbye file
* 2c0e242 hello file
```
54b943f and 9e2c485 are the new commits. e159214 is when you last pulled master.

### 3. Push fails because someone committed and pushed to master
```
$ git push
To /repo
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to '/repo'
```

### 4. Let's fetch remote changes
```
* 9b4cc69 (origin/master, origin/HEAD) goodbye reason
| * 54b943f (HEAD, master) sadder goodbye
| * 9e2c485 happier hello
|/  
* e159214 goodbye file
* 2c0e242 hello file
```
9b4cc69 is the culprit.

### 5. Let's merge (or pull, it does the same)
```
*   e4a3911 (HEAD, master) Merge branch 'master' of /repo
|\  
| * 9b4cc69 (origin/master, origin/HEAD) goodbye reason
* | 54b943f sadder goodbye
* | 9e2c485 happier hello
|/  
* e159214 goodbye file
* 2c0e242 hello file
```

### 6. This looks wrong !!
Look at e4a3911. Merge branch master?? We merged (their) master into (our)
master, but there are not 2 branches. It's just master. The merge looks
artificial and if we keep doing so, we'll end up with a master history full of
"bumps" instead of a straight line.

### 7. Let's go back before the merge
```
$ git reset --hard 54b943f
* 9b4cc69 (origin/master, origin/HEAD) goodbye reason
| * 54b943f (HEAD, master) sadder goodbye
| * 9e2c485 happier hello
|/  
* e159214 goodbye file
* 2c0e242 hello file
```

### 8. Rebase to rescue
Could we remove the artificial merge by pretending our commits happened after
9b4cc69? Rebase!
```
$ git rebase origin/master
* 62eb7c1 (HEAD, master) sadder goodbye
* fb43f9b happier hello
* 9b4cc69 (origin/master, origin/HEAD) goodbye reason
* e159214 goodbye file
* 2c0e242 hello file
```
Rebase removed our commits 9e2c485 and 54b943f. Moved our master to latest
commit available 9b4cc69. Replayed our commits on that. Our commits are now
fb43f9b and 62eb7c1. Sha1 changed because their parent changed. We can push now!

### 9. Why is this rebase nice?
Because we have just one branch (master) and we're back to a straight line
history. The irrelevant fact that we committed on a obsolete master, because 
there were fresh changes available, has gone away. No noise in our history!

### 10. What if i really wanted a branch? 
What if your changes were not meant to be shoot & forget, but you really wanted
a branch, because you'll do more work on that line of development later. Let's
go back.
```
$ git reset --hard 54b943f
* 9b4cc69 (origin/master, origin/HEAD) goodbye reason
| * 54b943f (HEAD, master) sadder goodbye
| * 9e2c485 happier hello
|/  
* e159214 goodbye file
* 2c0e242 hello file
```

### 11. Let's make our branch
```
$ git branch fun_fixes
* 9b4cc69 (origin/master, origin/HEAD) goodbye reason
| * 54b943f (HEAD, master, fun_fixes) sadder goodbye
| * 9e2c485 happier hello
|/  
* e159214 goodbye file
* 2c0e242 hello file
```

### 12. Pretend we never worked on master.
Master is the latest commit available from server.
```
$ git reset --hard 9b4cc69
* 9b4cc69 (HEAD, origin/master, origin/HEAD, master) goodbye reason
| * 54b943f (fun_fixes) sadder goodbye
| * 9e2c485 happier hello
|/  
* e159214 goodbye file
* 2c0e242 hello file
```

### 13. Merge the branch into master
```
$ git merge fun_fixes
*   ac5afa6 (HEAD, master) Merge branch 'fun_fixes'
|\  
| * 54b943f (fun_fixes) sadder goodbye
| * 9e2c485 happier hello
* | 9b4cc69 (origin/master, origin/HEAD) goodbye reason
|/  
* e159214 goodbye file
* 2c0e242 hello file
```
Perfect. We can push now.

### 14. Why is this merge nice?
Because if we do more work on the branch later, we can safely merge again into master
```
$ git checkout fun_fixes 
$ vim goodbye.txt 
$ git commit -a -m "another fix"
$ git checkout master
$ git merge fun_fixes 
*   1399314 (HEAD, master) Merge branch 'fun_fixes'
|\  
| * 76f4d1c (fun_fixes) another fix
* |   ac5afa6 Merge branch 'fun_fixes'
|\ \  
| |/  
| * 54b943f sadder goodbye
| * 9e2c485 happier hello
* | 9b4cc69 (origin/master, origin/HEAD) goodbye reason
|/  
* e159214 goodbye file
* 2c0e242 hello file
```
and, having the recent merge point ac5afa6, Git "knows" it has to apply just
the new 76f4d1c and not the old 54b943f and 9e2c485.

## Morale
* If your changes are long lived, make a branch (even if you forgot to branch) and merge
* If your changes are one time, don't branch and rebase
* Watch out! Pull does merge by default (unless --rebase). Better, do fetch +
  merge/rebase for more control.

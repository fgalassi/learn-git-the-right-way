# What Git Push pushes

## How it works
```git push <remote> <branch>``` pushes exactly the branch ```<branch>``` to the
same named branch on remote ```<remote>```. You can always use this form to
achieve full control.
```
$ git push origin master
```

If you omit ```<branch>```, what git pushes is regulated by the config option
```push.default```. By default it's ```matching``` that means push
all the local branches that already have a remote branch with the same name.
So if you're on a branch ```develop``` with new commits in both ```develop```
and ```master```, git will push both.

```
$ git branch
* develop
  master
$ git push origin
Counting objects: 10, done.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 565 bytes, done.
Total 6 (delta 0), reused 0 (delta 0)
To /repo
   364576d..2525509  develop -> develop
   5548fe7..1203e9d  master -> master
```

Look at the bottom. It pushed master as well. This is good if you use ```git
push``` as a command to send everything after a work session on multiple
branches.

## The problem
This can be confusing because it makes ```push``` and ```pull``` asymmetric.
```push``` pushes all matching branches. ```pull``` pulls (merges) always just
one branch into its own ```tracking branch```. You could end up pushing unwanted
changes.

### What's a tracking branch
A tracking branch is just a branch that has configuration to let git know its
upstream branch, that is, the right remote and remote branch name to push to/pull from.
It's done in ```.git/config``` in a branch subsection

```
[branch "master"]
        remote = origin
        merge = refs/heads/master
```
This says that the local branch ```master``` should pull from
```refs/heads/master``` on ```origin``` repository.

### How tracking branches are created
A tracking branch is always created if you branch from a remote branch like ```origin/<branch>```.  

```
$ git branch develop origin/develop
Branch develop set up to track remote branch develop from origin.
```

This is also true when ```git clone``` creates the ```master``` branch.

Otherwise you can set it explicitly when branching
```
# git 1.7
$ git branch --set-upstream foo origin/foo
# git 1.8
$ git branch --set-upstream-to=origin/foo foo
```
or even when pushing with ```-u``` option
```
$ git push -u origin foo
```

## The solution
### Push.default to tracking
Change push.default to ```tracking``` (```upstream``` from git 1.8) so that push
works like pull. Git will now try to push from the current branch to its
upstream branch.
```
$ git config --global push.default tracking
$ git branch
* develop
  master
$ git push origin
Counting objects: 10, done.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 565 bytes, done.
Total 6 (delta 0), reused 0 (delta 0)
To /repo
   364576d..2525509  develop -> develop
```
Only develop this time.
### Remember to set up tracking branches for branches you create
Always setup tracking branches when pushing with ```-u``` the first time
```
git push -u origin develop
```
That's because now if you push a branch with no upstream branch, you'll get an
error
```
fatal: The current branch develop has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin develop
```
### Git 2.0
Attention: in git 2.0 push.default will default to ```simple``` (much like
```tracking``` or ```upstream```).

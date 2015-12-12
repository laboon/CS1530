## BadRepo1

```
git revert _SHA of last commit_
```

## BadRepo2

A _merge conflict_ is when two branches change the same line.  When merging, they are indicated as follows:

```
<<<<<<< HEAD
			toReturn = '_';
=======
			toReturn = ' ';
>>>>>>> wjl_display
```

When you see these, it means git could not figure out which one to use.  You need to delete all of the garbage (<<<<<< HEAD, ======, >>>>>> wjl_display), and determine yourself which line to use.  The lines _above_ the ====== signs are what is in the branch you are merging into; the lines _below_ are the ones from the branch you are merging from.  The final product should be equal to the code you want in master (or whatever branch you are merging _into_).

Merge conflicts were accidentally committed "as actual code".  Two solutions:

1. Revert back a commit (as in BadRepo1).  Then re-merge (`git merge wjl_display`).  Fix merge conflicts along the way as per normal.
2. Resolve the merge conflicts in master, and then commit that as an additional change.

In general, small issues like this would be solved the second way; larger errors in the first way.

## BadRepo3
```
git checkout wjl_commits
git rebase -i master
Squash (s) all of the commits into the first one
```

Note that you won't be able to push this back up, since you "rewrote history" on the branch!  You can override this with `git push -f _branchname_`, or you can make a new branch from that point `git checkout -b _new_branch_`.

## BadRepo4
```
git checkout master
git merge wjl_derp
```
Fix all of the merge conflicts
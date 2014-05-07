Branch Per Feature Git Work-flow
================================

Ideally for the branch per ticket work-flow you make zero changes to your master branch and make all changes on ticket branches.
You also have to maintain a committed revision (which you amend as you go) i.e. a single commit per branch.

This allows working on multiple tasks in parallel with clean separation of changes.

1. `git checkout -b ticketname master` — Creates new branch from master with the name «ticketname» and switches to it
2. Make modifications to files
3. `git status` — Check what files need to be added
4. `git add filename1 filename2` — Add modifications or new files to the staging area
5. `git commit -m "Commit message"` —  Create your commit — further commits on this branch use `--amend` to modify this commit e.g.for review fixes or switching branches
6. Make modifications to files again if needed
7. `git add filename1 filename2` — Add modifications
8. `git commit --amend` —  Amend your first commmit with new modifications. Repeat 6-8 steps as many times as needed.
9. `git checkout master` — Go back to master
10. `git pull origin master` — Update the master branch with the latest changes from other developers
11. `git checkout ticketname` — Switch back to your branch
12. `git rebase master` — Bring your ticket branch up to date with the latest changes and move your commit to the top of the history (make it latest)
13. If rebase fails you will be dumped to «no branch» go to «13.1», is successful go to «14»
    1. `git status` — See what files failed to merge
    2. Make modifications to failed merges
    3. `git add filename` — Add fixed files
    4. `git rebase --continue` — Finish the rebase
    5. `git checkout master` — Go back to master
    6. `git pull origin master` — Pull again to be sure nobody commits new changes in master while you merging files. If new commits pulled go to step «11» and rebase again
14. `git checkout master` — Go back to master
15. `git merge ticketname` — Merge branch «ticketname» to «master»
16. `git push origin master` — Push your changes to origin repository
17. `git branch -d ticketname` — Delete the branch, you can't use it anymore

Do not keep the branch and re-use it after `git merge` and `git push origin master` as this will mess up the git history.

If you ever will need to work on this feature again (improvements, bugfixes ect.), you should create new branch with the same name.

When working on a ticked by this method for a long time. it's recommended to pull the master and rebase the branch from time to time to update the files with the latest versions.

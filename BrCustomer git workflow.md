Git process with BrCustomer
===========================

Branch "master" should never be committed into or merged into.

A branch "style" has been created for front-end tasks. You should create local branches off that. And then you can merge back into "style" when done. Also make sure "style" is regularly merged from "master". And your branches regularly merged from "style".

## Setting up

As our primary branch would be "style" not "master" let make some changes in settings.

1. `git clone https://github.com/coretech/BrCustomer.git` — clone repo
2. `git cd BrCustomer` — go inside repo
3. `git pull origin style` — pull branch "style" from remote
4. `git remote set-head origin style` — set tracking remote "style" branch
5. `git checkout style` — switch to "style" branch. Should output something like this:

    ```
    $ git checkout style
    Branch style set up to track remote branch style from origin.
    Switched to a new branch 'style'
    ```
6. `git remote show origin` — check our settings. Output:

    ```
    $ git remote show origin
    * remote origin
      Fetch URL: https://github.com/coretech/BrCustomer.git
      Push  URL: https://github.com/coretech/BrCustomer.git
      HEAD branch (remote HEAD is ambiguous, may be one of the following):
        master
        style
      Remote branches:
        master tracked
        style  tracked
      Local branches configured for 'git pull':
        master merges with remote master
        style  merges with remote style
      Local refs configured for 'git push':
        master pushes to master (up to date)
        style  pushes to style  (up to date)
    ```

## Work process

1. `git checkout -b ticketname style` — Creates new branch from "style" with the name "ticketname" and switches to it
2. Make modifications to files
3. `git status` — Check what files need to be added
4. `git-citool` — Graphical alternative to git-commit:
    1. Add modifications or new files to the staging area
    2. Write comment in format: *ticket-number - description what is done*
    3. Create your commit with "save" button
5. Make modifications to files again if needed
6. `git-citool` — Graphical alternative to git-commit:
    1. Add modifications or new files to the staging area
    2. Switch radiobutton to "Use last state"
    3. Commit your changes
7. Repeat 5-6 steps as many times as needed.
8. `git checkout style` — Go back to "style"
9. `git pull origin style` — Update the "style" branch with the latest changes from other developers
10. `git checkout ticketname` — Switch back to your branch
11. `git rebase style` — Bring your ticket branch up to date with the latest changes and move your commit to the top of the history (make it latest)
12. If rebase fails you will be dumped to «no branch» go to «12.1», is successful go to «13»
    1. `git status` — See what files failed to merge
    2. Make modifications to failed merges
    3. `git add filename` — Add fixed files or use `git-citool` to do that (don't commit)
    4. `git rebase --continue` — Finish the rebase
    5. `git checkout style` — Go back to "style"
    6. `git pull origin style` — Pull again to be sure nobody commits new changes in "style" while you merging files. If new commits pulled go to step «11» and rebase again
13. `git checkout style` — Go back to "style"
14. `git merge ticketname` — Merge branch "ticketname" to "style"
15. `git push origin style` — Push your changes to origin repository
16. `git branch -d ticketname` — Delete the branch, you can't use it anymore

Do not keep the branch and re-use it after `git merge` and `git push origin style` as this will mess up the git history.

If you ever will need to work on this feature again (improvements, bugfixes ect.), you should create new branch with the same name.

When working on a ticked by this method for a long time. it's recommended to pull the "style" and rebase the branch from time to time to update the files with the latest versions.

## Updating branch "style" with changes from "master"

1. `git checkout master`
2. `git pull origin master`
3. `git checkout style`
4. `git pull origin style`
5. `git rebase master` — Bring your ticket branch up to date with the latest changes and move your commit to the top of the history (make it latest)
6. If rebase fails you will be dumped to «no branch» go to «6.1», is successful go to «7»
    1. `git status` — See what files failed to merge
    2. Make modifications to failed merges
    3. `git add filename` — Add fixed files or use `git-citool` to do that (don't commit)
    4. `git rebase --continue` — Finish the rebase
    5. `git checkout master` — Go back to "master"
    6. `git pull origin master` — Pull again to be sure nobody commits new changes in "master" while you merging files. If new commits pulled go to step «5» and rebase again
7. `git push origin style` — update remote branch with merged changes

# X13-Super-Module

This is an advanced way to manage all the board repos for IEEE ROV. 
Each board's repo is treated as a submodule. 
Git submodules do not track the files inside a submodule, they only point to a commit in the submodule.

### Updating to changes

To get the version pointed at by the super module (this repo), run:  
`git submodule update --init --recursive`  
This can be accessed easier via:  
`git config --global alias.sup 'submodule update --init --recursive'`  
so that you can then type `git sup`

When you cd into a submodule, you will be in a detached HEAD state. You will want to
`git switch` or `git checkout` a branch. To find the branches, run `git branch` or
`git branch -r` to see remote branches.

		
To get the latest version of each submodule, run:  
`git submodule foreach --recursive git pull`.  
Note: you must be on a branch in order to do this.
Alternatively, running `git submodule update --remote` will pull the latest
commits from the branch tracked in `.gitmodules`, but will finished in a detached head state.

To set up a new submodule, run:  
`git submodule add link.copied.from.github`  
To add tracking the for a branch such as master, use:  
`git submodule add -b master link.copied.from.github`  


### Other: Merging and merge conflicts
Running `git merge --ff-only` or `git pull --ff--only` will prevent git from automatically trying to merge
diverged histories. If you are in a conflict merge commit and want to exit, run `git merge --quit`.  

To merge two branches that have diverged, you have several options. 
1. `git merge -s recursive -X ours` and `git merge -s recursive -X theirs` will attempt to interleave
changes from both files. When conflicts arise, it will prefer local/current (ours) changes in 
`-X ours` and the remote/merging branch (theirs) changes in `-X theirs`.
2. `git merge -s ours` this will "merge" the other branch, but discard all of it's changes.
3. If you have diverged histories and want to delete yours, you can "undo" or "delete" several commits,
then fast-forward merge. It is recommended to first make a "backup" branch (rather than messing with reflog), 
by running `git branch local-backup` (local-backup can be any name). Then run `git reset --hard HEAD~N` where
`N` is the number of commits to undo. The run `git merge branch-name` or `git pull` to fastforward merge the
other branch.

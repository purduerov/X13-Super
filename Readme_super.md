# X13-Super-Module

This is an advanced way to manage all the board repos for IEEE ROV. 
Each board's repo is treated as a submodule. 
Git submodules do not track the files inside a submodule, they only point to a commit in the submodule.

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


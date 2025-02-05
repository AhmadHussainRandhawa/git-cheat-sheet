# Git Basics Cheat Sheet

## Configuration
- `git config --global user.name "Your Name"`                   # Set your name
- `git config --global user.email "your.email@example.com"`     # Set your email
- `git config --global core.editor "code --wait"`	            # Set vs_code as default editor
- `git config --list`  # View all configurations (use --show-origin to know the exact location)

## Starting a Repository
- `git init`                # Initialize a new repository
- `git status`              # Check status of changes
- `git add <file>`          # Stage a file
- `git add .`               # Stage all changes
- `git commit -m "Message"` # Commit changes
- `git commit --amend -m "New Message"`  # Include new changes to the last commit


## Branching
- `git branch`                          # List branches
- `git branch -r`         				# Displays the remote branches
- `git branch <branch-name>`            # Create a new branch
- `git checkout <branch-name>`          # Switch to a branch
- `git checkout -b <branch-name>`       # Create and switch to a new branch

## Delete the specific branch
- `git branch-d <branch-name>`			# Delete the specific branch locally.
- `git push origin --delete <b_name>`	# Delete the specific branch remotely.
- `git fetch --prune`				    # Remove all the references related to the deleted branch.

- `git checkout -b new origin/new`          # Create a new branch that tracks the remote serverfix branch.
- `git branch -u origin/serverfix`          # Track the existing branch with origin/serverfix.        
- `git branch -v`			                # Shows the branch name, commit hash, commit message for local branches.
- `git branch -vv`			                # Additional details like whether local is ahead, behind or up-to-date with remote.
- `git fetch <remote_name>`			    	# Downloads the changes but doesn't apply them to your branch.
- `git branch -m main master` 		        # Rename the branch.

- `git log origin/main`			  		    # Show commit history related to that branch.
- `git diff <local-branch>..origin/<remote-branch>` 	# Show the difference b/w local and remote branch.

## Merging
- `git merge <branch-name>`         # Merge a branch into the current branch
- `git branch --merged`         	# list the branches that are merged into current branch.
- `git branch --no-merged`		    # List all the branches that are not merged into current branch

## Remote Repositories
- `git clone <repo-url>`                    # Clone an existing repository
- `git remote add origin <repo-url>`        # Connect to remote repository
- `git remote -v`                           # Tells the exact address of remote repository
- `git push -u origin <branch-name>`        # Push to remote repository
- `git push`                                # Push committed changes
- `git pull`                                # Pull latest changes from remote
- `git fetch`                               # Fetch latest changes without merging

- `git remote rename pb paul`	        	# Used to rename the remote 
- `git remote remove paul`	            	# Remove the remote

- `git remote show origin`				    # Provide detail information about a specific repository.
- `git push origin main:master`				# Move local main branch to the remote with a name master for remote.			 
- `git ls-remote origin`  				    # Shows the references (branches, tags, etc) and their corresponding commit hashes 
- `git pull origin main --allow-unrelated-histories`	# case i have some extra files on remote repository

## Resetting & Reverting
- `git reset --hard HEAD~1`     # Undo last commit, remove changes

## Logs & History: Shows the commit history
- `git reflog`	                # Shows the history of HEAD.
- `git log`                     # Show commit history
- `git log -2` 		        	# Shows only the last 2 commits.
- `git log --stat`		        # Shows the commit history with the difference b/w each commit. In short
- `git log -p`			        # Shows the commit history with the difference b/w each commit. In more details
- `git log -p -2`

- `git log -- <file_name>`		# Shows the commit history related to a specific file.
- `git log --merges`			# Shows only the commits that are merge commits.
- `git log --oneline --graph`   # Shows history in a graph at one line
 
- `git log branch1..branch2`				            # Lists commits in branch2 that are not in branch1.
- `git log --grep="<keyword>" -i`			            # Search in commit messages. -i for insensitice case search.
- `git log --author="<au_nam>`					        # Shows commit history of specific author.
- `git log --since="YYYY-MM-DD" --until="YYYY-MM-DD"`	# Shows commits within a specific date range.

## diff: Show differences by comparing the changes b/w files, branches etc

- `git diff HEAD`			        # Shows the difference b/w the working directory and the last commit.
- `git diff`			            # Shows the difference b/w the working directory and the staging area.
- `git diff --stat`  		        # Shows only the changed file name.
- `git diff --cached`		        # Shows the difference b/w the staging area and the last commit.
- `git diff branch1..branch2`	    # Shows the difference b/w the branches. Check it before merging
- `git diff commit1 commit2`	    # Shows the difference b/w the commit
- `git diff <commit> <file>`	    # Shows the difference b/w the commit and file.


## Stashing
- `git stash -m "msg"`	     # Temporarily stored the file on a side structure without affecting the file in working directory.
- `git stash list`			 # Shows the list of saved stashes.
- `git stash show` 		     # Shows the exact stash.
- `git stash branch <b_name>`# Move that stashes to specific branch.

- `git stash pop`       # Apply and remove the most recent stash
- `git stash apply`     # Apply a stash without removing it
- `git stash pop --index 1`
- `git stash pop --index stash@{2} -f`	# force the stash to apply (Warning: it will permanently removes the uncommit changes)
- `git stash apply stash@{2}`		# Apply the stash without removing it from the stash list (useful for resolving conflicts).
- `git stash drop stash@{3}`      # Remove a specific stash
- `git stash clear`			# Clear all stashes


## Ignoring Files
- Create a `.gitignore` file and list files to be ignored
- `git status --ignored`        # Show the ignored files.

## Useful Aliases
- `git config --global alias.cm "commit -m"`  # Sets cm as a shortcut for commit -m 
- `git config --global --unset alias.cm`   # Remove the shortcut
- `git config --global alias.graph "log --all --oneline --graph --decorate"`  # git graph = git log --all --graph --oneline... 

## rm always removed a file from git tracking.
- `git rm <f_name>`		        # Removing a File from the Staging Area and Working directory, and from git tracking.
- `git rm --cached <f_name>`    # Removing a File from the Staging Area, and from git tracking.
- `git rm -r --cached <d_name>`	# Remove specific directory from staging area, and from git tracking.
- `git rm -r --cached .`        # Remove all the files from staging area in a current directory and sub directories, and from git tracking. 

- `git rm log/\*.log` 		    # Removes all .log files in the log/ directory from both staging area and working directory.
- `git rm \*.py` 		        # Removes all .py files tracked by Git, regardless of the directory.

- `git mv old_name new_name`    # Renames a File.
- `git mv file_name directory/` # Moves a File to the specific directory.

## Undoing Things
- `git show <commit-id>`                # Show details of a commit
- `git show --name-only <commit_hash>`    # Displays the files in specific commit.
- `git show <commit-hash>:<f_name>`		# Displays the content of specific file.

- `git checkout -- <filename>`			# Just discard your changes in working directory with last commit.
- `git checkout 9ddbs -- file.txt`		# Recover the file data from specific commit.

- `git restore --staged <filename>`		# Unstage a file from the staging area
- `git restore --source=<commit> --worktree --staged`	# Overwrite all the files in your current branch with the state of the specific commit.

-----------------Detached Head-----------------

- `git checkout 61f1cd`		# Directly accessed the Detached Head or it is just used to work with commits.
- `git branch stage` 		# Creates a branch stage in it, But the Head is no longer attached to it, cuz it is detached Head.
- `git checkout stage`		# Run this to access this branch instead of in a detached head. 


## Others
- `touch <file-name>`   # Create the file.
- `cat <file-name>`     # Display the data of the file.
- `vim <file-name>`		# it let's you create, view and edit the file.
- `ls -a`               # List all the files including the hidden file	


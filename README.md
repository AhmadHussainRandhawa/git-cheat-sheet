# Git Cheat Sheet

A practical, quick-reference Git command list — configuration, branching, remotes, stashing, logs, diffs, tags, undoing changes, and more.

## Table of Contents

- [Configuration](#configuration)
- [Starting a Repository](#starting-a-repository)
- [Branching](#branching)
- [Remote Repositories](#remote-repositories)
- [Stash](#stash)
- [Logs](#logs)
- [Diff](#diff)
- [Rebase](#rebase)
- [Tags](#tags)
- [Undoing Things](#undoing-things)
- [Ignoring Files](#ignoring-files)
- [Useful Aliases](#useful-aliases)
- [Removing & Renaming](#removing--renaming)
- [Detached HEAD](#detached-head)
- [Other Useful Commands](#other-useful-commands)

---

## Configuration

| Command | Description |
|---|---|
| `git config --global user.name "Your Name"` | Set your name |
| `git config --global user.email "your.email@example.com"` | Set your email |
| `git config --global core.editor "code --wait"` | Set VS Code as the default editor |
| `git config --global init.defaultBranch main` | Set the default branch name to `main` |
| `git config --list` | View all configurations (`--show-origin` shows the exact file each came from) |
| `git config --global color.ui auto` | Enable colored terminal output |
| `git config --global core.autocrlf input` | Normalize line endings (macOS/Linux) |
| `git config --global pull.rebase true` | Rebase instead of merge on `git pull` |

---

## Starting a Repository

| Command | Description |
|---|---|
| `git init` | Initialize a new repository |
| `git status` | Check the status of changes |
| `git add <file>` | Stage a file |
| `git add .` | Stage all changes |
| `git add -A` | Stage all changes, including deletions |
| `git commit -m "Message"` | Commit staged changes |
| `git commit --amend -m "New Message"` | Add new changes to (or edit the message of) the last commit |
| `git push origin main --force` ⚠️ | Force-push, overwriting remote history — use with caution |
| `git fetch --all` | Fetch updates from all remotes |
| `git reset --hard origin/main` ⚠️ | Discard local changes and match the remote exactly — destructive |

---

## Branching

| Command | Description |
|---|---|
| `git branch` | List local branches |
| `git branch -r` | List remote branches |
| `git branch -a` | List all branches (local + remote) |
| `git branch <branch-name>` | Create a new branch |
| `git switch <branch-name>` | Switch to an existing branch |
| `git switch -c <branch-name>` | Create and switch to a new branch |
| `git branch -d <branch-name>` | Delete a branch locally |
| `git push origin --delete <branch-name>` | Delete a branch remotely |
| `git branch -v` | Show local branches with commit hash and message |
| `git branch -vv` | Also show whether local is ahead/behind/up-to-date with remote |
| `git fetch <remote-name>` | Download updates from a remote (does **not** merge) |
| `git fetch --prune` | Remove local references to remote branches that were deleted on the server |
| `git branch -m <old-name> <new-name>` | Rename a branch |
| `git log origin/main` | Show commit history for that remote branch |
| `git diff <local-branch>..origin/<remote-branch>` | Show the difference between a local and remote branch |
| `git merge <branch-name>` | Merge a branch into the current branch |
| `git branch --merged` | List branches already merged into the current branch |
| `git branch --no-merged` | List branches **not yet** merged into the current branch |

---

## Remote Repositories

| Command | Description |
|---|---|
| `git clone <repo-url>` | Clone an existing repository |
| `git remote -v` | Show the URLs of the configured remotes |
| `git remote add origin <repo-url>` | Connect to a remote repository |
| `git push origin <branch-name>` | Push to a remote repository |
| `git push -u origin <branch-name>` | Push and set the upstream tracking branch |
| `git push` | Push committed changes |
| `git pull` | Pull the latest changes from remote |
| `git fetch` | Fetch the latest changes without merging |
| `git remote rename <old> <new>` | Rename a remote |
| `git remote remove <name>` | Remove a remote |
| `git remote show origin` | Show detailed info about a specific remote |
| `git push origin main:master` | Push local `main` to a remote branch named `master` |
| `git ls-remote origin` | List a remote's branches/tags and their commit hashes |
| `git pull origin main --allow-unrelated-histories` | Pull when the remote has unrelated history (e.g. extra pre-existing files) |

---

## Stash

Temporary storage for uncommitted changes.

| Command | Description |
|---|---|
| `git stash` | Stash current changes |
| `git stash push -m "msg"` | Stash current changes with a message |
| `git stash list` | List saved stashes |
| `git stash pop` | Apply and remove the most recent stash |
| `git stash apply` | Apply a stash without removing it |
| `git stash apply stash@{2}` | Apply a specific stash |
| `git stash apply stash@{2} <branch-name>` | Apply a specific stash to a specific branch |
| `git stash clear` | Clear all stashes |
| `git stash drop stash@{3}` | Remove a specific stash |
| `git stash branch <branch-name>` | Move a stash's changes into a new branch |

---

## Logs

| Command | Description |
|---|---|
| `git reflog` | Show the history of `HEAD` |
| `git log` | Show commit history |
| `git log -2` | Show only the last 2 commits |
| `git log --stat` | Show commit history with a summary of changes per commit |
| `git log -p` | Show commit history with full diffs |
| `git log -p -2` | Full diffs, limited to the last 2 commits |
| `git log -- <file>` | Show commit history for a specific file |
| `git log --merges` | Show only merge commits |
| `git log --oneline --graph` | Show history as a one-line-per-commit graph |
| `git log branch1..branch2` | List commits in `branch2` not present in `branch1` |
| `git log --grep="<keyword>" -i` | Search commit messages (`-i` = case-insensitive) |
| `git log --author="<name>"` | Show commits by a specific author |
| `git log --since="YYYY-MM-DD" --until="YYYY-MM-DD"` | Show commits within a date range |

---

## Diff

Shows differences between Git states — working directory, staging area, commits, branches.

| Command | Description |
|---|---|
| `git diff` | Show unstaged changes |
| `git diff --staged` | Show staged changes (staging area → last commit) |
| `git diff HEAD` | Show all changes since the last commit (staged + unstaged) |
| `git diff branch1..branch2` | Show differences between two branches (useful before merging) |
| `git diff commit1 commit2` | Show differences between two commits |
| `git diff <commit> <file>` | Show how a specific file changed in a commit |
| `git diff --stat` | Show a summary of changes (files changed, lines added/removed) |

---

## Rebase

| Command | Description |
|---|---|
| `git rebase` | Reapply commits on top of another base tip |

> This section is intentionally minimal — expand with specific rebase workflows (`git rebase -i`, `--onto`, conflict resolution) as you use them more.

---

## Tags

Tags mark specific commits — typically used at release points.

| Command | Description |
|---|---|
| `git tag` | List all tags |
| `git tag v1.0.0` | Create a lightweight tag at the current commit |
| `git tag -a v1.0.0 -m "Release version 1.0.0"` | Create an annotated tag |
| `git tag <tag-name> <commit-hash>` | Tag a specific (past) commit |
| `git push origin <tag-name>` | Push one specific tag to GitHub |
| `git push origin --tags` | Push all local tags to remote |
| `git tag -d <tag-name>` | Delete a local tag |
| `git push origin --delete v1.0.0` | Delete a tag from GitHub |

---

## Undoing Things

| Command | Description |
|---|---|
| `git show <commit-id>` | Show details of a commit |
| `git show --name-only <commit-hash>` | List the files changed in a specific commit |
| `git show <commit-hash>:<file>` | Show a file's content as of a specific commit |
| `git reset --hard <commit-hash>` ⚠️ | Undo commits and discard all changes, staged or not — destructive |
| `git restore --staged <file>` | Unstage a file |
| `git restore <file>` | Restore a file to match the last commit (only if not staged) |
| `git restore --source=<commit> -- <file>` | Restore a specific file from a specific commit |
| `git restore --source=<commit> --worktree --staged` | Restore the entire project from a specific commit |
| `git checkout <file>` | Restore a file to its state at the last commit |
| `git checkout <commit-hash> -- <file>` | Restore a file from a specific commit |

---

## Ignoring Files

- Create a `.gitignore` file and list the files/patterns to ignore.
- `git status --ignored` — show which files are currently being ignored.

---

## Useful Aliases

| Command | Description |
|---|---|
| `git config --global alias.cm "commit -m"` | Sets `git cm` as a shortcut for `git commit -m` |
| `git config --global --unset alias.cm` | Remove that alias |
| `git config --global alias.graph "log --all --oneline --graph --decorate"` | Sets `git graph` as a shortcut for a full visual log |

---

## Removing & Renaming

`git rm` always removes a file from Git's tracking, not just the working directory.

| Command | Description |
|---|---|
| `git rm <file>` | Remove a file from the staging area, working directory, and Git tracking |
| `git rm --cached <file>` | Unstage a file (keep it on disk, stop tracking it) |
| `git rm -r --cached <dir>` | Remove a directory from tracking (keep it on disk) |
| `git rm -r --cached .` | Stop tracking everything in the current directory and subdirectories (keep files on disk) |
| `git rm log/\*.log` | Remove all `.log` files in `log/` from staging and working directory |
| `git rm \*.py` | Remove all tracked `.py` files, regardless of directory |
| `git mv old_name new_name` | Rename a file |
| `git mv file_name directory/` | Move a file into a directory |

---

## Detached HEAD

- `git checkout 61f1cd` — check out a specific commit directly; this puts you in a "detached HEAD" state, useful for inspecting or experimenting with an old commit.
- `git branch stage` — creates a new branch called `stage` at the current commit, but HEAD stays detached — you're not automatically switched onto it.
- `git checkout stage` — switch onto that branch properly, out of the detached HEAD state.

---

## Other Useful Commands

| Command | Description |
|---|---|
| `touch <file>` | Create a file |
| `cat <file>` | Display a file's contents |
| `vim <file>` | Create, view, or edit a file |
| `ls -a` | List all files, including hidden ones |
| `git ls-tree -r <commit-hash>:<dir>` | Show the full file structure at a specific commit |
| `git branch -m old-branch-name new-branch-name` | Rename a branch |

---

Corrections and additions welcome — open a PR if you spot something missing or wrong.
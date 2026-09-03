# Git Cheat Sheet

A practical reference for everyday Git commands.

## 1. Setup

```bash
# Check Git version
git --version

# Configure username
git config --global user.name "Your Name"

# Configure email
git config --global user.email "you@example.com"

# View configuration
git config --list
```

---

## 2. Create / Clone Repository

```bash
# Initialize Git in current folder
git init

# Clone repository
git clone https://github.com/user/repo.git

# Clone into a specific folder
git clone https://github.com/user/repo.git my-project
```

---

## 3. Check Repository Status

```bash
# Check status
git status

# Short status
git status -s
```

---

## 4. Add Files

```bash
# Add one file
git add filename.php

# Add multiple files
git add file1.php file2.php

# Add everything
git add .

# Add all modified/deleted files
git add -A
```

---

## 5. Commit

```bash
# Commit staged files
git commit -m "Add login feature"

# Commit with a descriptive message
git commit -m "Fix authentication bug"

# Add and commit tracked files
git commit -am "Fix bug"
```

> `git commit -am` does **not** include brand-new untracked files.

---

## 6. Branches

```bash
# List branches
git branch

# List all local and remote branches
git branch -a

# Create a branch
git branch feature/login

# Switch branch
git switch feature/login

# Create and switch to a new branch
git switch -c feature/login

# Delete local branch
git branch -d feature/login

# Force delete local branch
git branch -D feature/login
```

### Older `checkout` equivalents

```bash
git checkout -b feature/login
git checkout main
```

---

## 7. Merge

```bash
# Switch to target branch
git switch main

# Merge another branch
git merge feature/login

# Abort an active merge
git merge --abort
```

### Typical merge workflow

```bash
git switch main
git pull
git merge feature/login
git push
```

---

## 8. Remote Repository

```bash
# View remotes
git remote -v

# Add remote
git remote add origin https://github.com/user/repo.git

# Change remote URL
git remote set-url origin https://github.com/user/new-repo.git

# Remove remote
git remote remove origin
```

---

## 9. Push

```bash
# Push current branch
git push

# Push branch for the first time
git push -u origin main

# Push a specific branch
git push origin feature/login

# Delete a remote branch
git push origin --delete feature/login
```

---

## 10. Pull / Fetch

```bash
# Download and merge remote changes
git pull

# Download remote changes only
git fetch

# Fetch all remotes
git fetch --all

# Pull a specific branch
git pull origin main
```

### `git fetch` vs `git pull`

```text
git fetch
    ↓
Download remote changes
    ↓
Does not automatically modify your working branch

git pull
    ↓
Fetch
    +
Merge (or rebase, depending on configuration)
```

---

## 11. View Changes

```bash
# Show unstaged changes
git diff

# Show staged changes
git diff --staged

# Compare two branches
git diff main feature/login

# View commit history
git log

# Compact history
git log --oneline

# Graphical history
git log --oneline --graph --all
```

---

## 12. Undo Changes

### Undo changes in a file that have not been staged

```bash
git restore filename.php
```

### Unstage a file

```bash
git restore --staged filename.php
```

### Undo the last commit but keep changes staged

```bash
git reset --soft HEAD~1
```

### Undo the last commit and unstage changes

```bash
git reset HEAD~1
```

### Completely remove the last commit and its changes

```bash
git reset --hard HEAD~1
```

> **Warning:** `git reset --hard` can permanently discard uncommitted work.

---

## 13. Delete / Clean Files

```bash
# Delete a tracked file
git rm filename.php

# Stop tracking a file but keep it locally
git rm --cached filename.php

# Preview untracked files that would be removed
git clean -n

# Remove untracked files
git clean -f
```

> **Warning:** Be careful with `git clean -f`.

---

## 14. Stash

Stash is useful when you have unfinished work but need to switch branches.

```bash
# Save current changes
git stash

# Save changes with a message
git stash push -m "WIP login"

# List stashes
git stash list

# Apply latest stash
git stash apply

# Apply and remove latest stash
git stash pop

# Delete a specific stash
git stash drop

# Delete all stashes
git stash clear
```

---

## 15. Tags

```bash
# Create a tag
git tag v1.0.0

# List tags
git tag

# Push a tag
git push origin v1.0.0

# Push all tags
git push origin --tags

# Delete local tag
git tag -d v1.0.0

# Delete remote tag
git push origin --delete v1.0.0
```

---

## 16. Recover Lost Work

`git reflog` can help recover commits, branches, or previous HEAD positions after accidental resets or branch changes.

```bash
# Show HEAD history
git reflog

# Recover a previous state
git reset --hard <commit-hash>
```

> Use `git reflog` before assuming that lost work is gone.

---

# Common Daily Workflow

A typical feature-development workflow:

```bash
# Start from the latest main branch
git switch main
git pull

# Create a feature branch
git switch -c feature/my-feature

# Make your changes...

# Review changes
git status
git diff

# Stage and commit
git add .
git commit -m "Add my feature"

# Push the new branch
git push -u origin feature/my-feature
```

After the feature branch has been merged:

```bash
git switch main
git pull

# Delete the local feature branch
git branch -d feature/my-feature
```

---

# Feature Branch Workflow

```text
main
 │
 ├── git switch -c feature/login
 │
 │      ↓
 │   Make changes
 │      ↓
 │   git add .
 │      ↓
 │   git commit
 │      ↓
 │   git push
 │      ↓
 │   Create Pull Request
 │      ↓
 └── Merge → main
```

---

# Quick Reference

| Task | Command |
|---|---|
| Initialize | `git init` |
| Clone | `git clone URL` |
| Status | `git status` |
| Add all | `git add .` |
| Commit | `git commit -m "message"` |
| List branches | `git branch` |
| New branch | `git switch -c name` |
| Switch branch | `git switch name` |
| Merge | `git merge name` |
| Pull | `git pull` |
| Fetch | `git fetch` |
| Push | `git push` |
| History | `git log --oneline` |
| Changes | `git diff` |
| Stash | `git stash` |
| Restore file | `git restore file` |
| Unstage | `git restore --staged file` |
| Recover work | `git reflog` |
| View remote | `git remote -v` |

---

# Commands Worth Memorizing

```bash
git status
git add .
git commit -m "message"
git pull
git push

git switch -c feature/name
git switch main
git merge branch

git stash
git log --oneline
git reflog
```

These commands cover most everyday Git development workflows.



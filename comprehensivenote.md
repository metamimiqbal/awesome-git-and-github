# The Ultimate Git & GitHub Reference Guide

> **Your complete guide to version control mastery** - From basics to advanced workflows
---
# Table of Contents

1. Initial Setup
2. Repository Initialization
3. Basic Workflow
4. Branching Strategies
5. Remote Operations
6. Merging & Rebasing
7. Undoing Changes
8. Advanced Operations
9. Collaboration Workflows
10. Troubleshooting
11. Best Practices
---

## Initial Setup

### First-Time Git Configuration

```bash
# Set your identity (REQUIRED before first commit)
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Set default branch name to 'main'
git config --global init.defaultBranch main

# Set default editor
git config --global core.editor "code --wait"  # VS Code
git config --global core.editor "vim"          # Vim
git config --global core.editor "nano"         # Nano

# Enable color output
git config --global color.ui auto

# View all configuration
git config --list
git config --global --list

# Check specific setting
git config user.name
```

### SSH Setup for GitHub (Recommended)

```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your.email@example.com"
# Press Enter to accept default location (~/.ssh/id_ed25519)
# Enter passphrase (optional but recommended)

# Start ssh-agent
eval "$(ssh-agent -s)"

# Add SSH key to agent
ssh-add ~/.ssh/id_ed25519

# Copy public key to clipboard (macOS)
pbcopy < ~/.ssh/id_ed25519.pub

# Copy public key to clipboard (Linux)
cat ~/.ssh/id_ed25519.pub | xclip -selection clipboard

# Copy public key to clipboard (Windows Git Bash)
cat ~/.ssh/id_ed25519.pub | clip

# Then: GitHub.com → Settings → SSH and GPG keys → New SSH key → Paste

# Test connection
ssh -T git@github.com
```

---

## Repository Initialization

### Starting a New Project

```bash
# Initialize git in current directory
git init

# Initialize with specific branch name - Sets the name of the very first brand new branch at the moment the repository is created.
git init -b main 
# --initial-branch -> use this for newly created project

git branch -m main # Move/Rename an existing Branch

# Initialize in a new directory
git init project-name
cd project-name

# Clone existing repository
git clone <https://github.com/username/repo.git>
git clone git@github.com:username/repo.git  # SSH (faster, more secure)

# Clone into specific directory
git clone <https://github.com/username/repo.git> my-folder

# Clone specific branch
git clone -b branch-name <https://github.com/username/repo.git>

# Shallow clone (last commit only - faster)
git clone --depth 1 <https://github.com/username/repo.git>
```

### .gitignore Essentials

```bash
# Create .gitignore file
touch .gitignore

# Common .gitignore patterns
cat > .gitignore << 'EOF'
# Compiled files
*.o
*.exe
*.out
a.out
*.class
*.pyc
__pycache__/
*.dll
*.so
*.dylib

# Logs
*.log
logs/
npm-debug.log*

# Operating System
.DS_Store
Thumbs.db
desktop.ini

# IDEs and Editors
.vscode/
.idea/
*.swp
*.swo
*~
.vscode/settings.json

# Dependencies
node_modules/
vendor/
bower_components/

# Environment variables
.env
.env.local
.env.*.local

# Build outputs
dist/
build/
out/
target/

# Temporary files
*.tmp
*.temp
.cache/

# Package manager locks (choose based on your preference)
# package-lock.json
# yarn.lock
# Pipfile.lock
EOF

# Ignore files already tracked (requires remove from index)
git rm --cached filename
git rm -r --cached directory/

# Force add ignored file (use sparingly)
git add -f ignored-file.txt

# Check if file will be ignored
git check-ignore -v filename

# List all ignored files
git status --ignored
```

---

## Basic Workflow

### The Core Git Cycle

```bash
# Check status (shows tracked, untracked, modified files)
git status
git status -s           # Short format
git status -sb          # Short format with branch info

# Add files to staging area
git add filename.txt              # Add specific file
git add file1.txt file2.txt       # Add multiple files
git add *.js                      # Add all JS files
git add .                         # Add all files in current directory
git add -A                        # Add all files (including deletions)
git add -u                        # Add only modified/deleted (not new)
git add -p                        # Interactive staging (review chunks)

# Remove from staging (unstage)
git reset filename.txt            # Unstage specific file
git reset                         # Unstage all files
git restore --staged filename.txt # Modern alternative

# Commit changes
git commit -m "Short descriptive message"
git commit -m "Title" -m "Detailed description in body"
git commit -am "Add and commit tracked files"  # Skip staging for tracked files
git commit --amend                # Modify last commit
git commit --amend --no-edit      # Add staged changes to last commit (keep message)
git commit --amend -m "New message" # Change last commit message

# View commit history
git log                           # Full log
git log --oneline                 # Compact view
git log --oneline --graph         # With branch graph
git log --oneline --graph --all   # All branches
git log -n 5                      # Last 5 commits
git log --since="2 weeks ago"     # Time-based filter
git log --author="John"           # Filter by author
git log --grep="bug fix"          # Search commit messages
git log -- filename.txt           # Commits affecting specific file
git log -p                        # Show diff in each commit
git log --stat                    # Show file change statistics

# Better log with custom format
git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit

# Create alias for beautiful log
git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
# Now use: git lg

# View changes
git diff                          # Unstaged changes
git diff --staged                 # Staged changes
git diff HEAD                     # All changes since last commit
git diff branch1 branch2          # Between branches
git diff commit1 commit2          # Between commits
git diff --name-only              # Just file names

# Show specific commit
git show commit-hash
git show HEAD                     # Last commit
git show HEAD~1                   # Second-to-last commit

q -> quit
space -> scroll
b -> scroll up
/text -> search
n -> next match
```

---

## Branching Strategies

### Branch Basics

```bash
# List branches
git branch                        # Local branches
git branch -r                     # Remote branches
git branch -a                     # All branches (local + remote)
git branch -v                     # Verbose (shows last commit)
git branch -vv                    # Very verbose (shows tracking branches)

# Create branch
git branch feature-name           # Create (doesn't switch)
git branch feature-name commit-hash # Create from specific commit

# Switch branches
git switch feature-name           # Modern way
git checkout feature-name         # Traditional way
git switch -                      # Switch to previous branch
git checkout -                    # Switch to previous branch

# Create and switch
git switch -c feature-name        # Modern way (recommended)
git checkout -b feature-name      # Traditional way

# Create branch from specific starting point
git switch -c feature-name main
git switch -c hotfix HEAD~3
git switch -c new-feature origin/develop

# Rename branch
git branch -m old-name new-name   # Rename any branch
git branch -m new-name            # Rename current branch

# Delete branch
git branch -d feature-name        # Safe delete (only if merged)
git branch -D feature-name        # Force delete (even if unmerged)

# Delete remote branch
git push origin --delete feature-name
git push origin :feature-name     # Alternative syntax

# Track remote branch
git branch --set-upstream-to=origin/feature-name
git branch -u origin/feature-name # Shorter version

# Create local branch from remote
git switch remote-branch-name     # Auto-tracks if name matches
git switch -c local-name origin/remote-branch
```

### Common Branching Workflows

### Git Flow (Feature Branches)

```bash
# Main branches
main        # Production-ready code
develop     # Integration branch

# Create develop branch
git switch -c develop main

# Start new feature
git switch -c feature/user-auth develop

# Work on feature...
git add .
git commit -m "Add user authentication"

# Finish feature (merge back to develop)
git switch develop
git merge --no-ff feature/user-auth
git branch -d feature/user-auth

# Create release branch
git switch -c release/1.0.0 develop

# After testing, merge to main and develop
git switch main
git merge --no-ff release/1.0.0
git tag -a v1.0.0 -m "Version 1.0.0"

git switch develop
git merge --no-ff release/1.0.0
git branch -d release/1.0.0

# Hotfix workflow
git switch -c hotfix/critical-bug main
# Fix the bug...
git add .
git commit -m "Fix critical security issue"

# Merge to both main and develop
git switch main
git merge --no-ff hotfix/critical-bug
git tag -a v1.0.1 -m "Hotfix: Security patch"

git switch develop
git merge --no-ff hotfix/critical-bug
git branch -d hotfix/critical-bug
```

### GitHub Flow (Simplified)

```bash
# Simple workflow: main + feature branches

# Create feature branch
git switch -c feature/add-footer

# Make changes and commit
git add .
git commit -m "Add responsive footer"

# Push to GitHub
git push -u origin feature/add-footer

# Create Pull Request on GitHub
# After review and approval, merge via GitHub UI
# Then locally:
git switch main
git pull
git branch -d feature/add-footer
```

### Trunk-Based Development

```bash
# Short-lived branches (1-2 days max)
# Frequent integration to main

git switch -c short-task
# Make small change
git add .
git commit -m "Small incremental change"
git switch main
git pull --rebase
git merge short-task
git push
git branch -d short-task
```

---

## Remote Operations

### Managing Remotes

```bash
# Add remote repository
git remote add origin <https://github.com/username/repo.git>
git remote add origin git@github.com:username/repo.git  # SSH

# View remotes
git remote                        # List remote names
git remote -v                     # List with URLs
git remote show origin            # Detailed info about remote

# Change remote URL
git remote set-url origin <https://github.com/username/new-repo.git>
git remote set-url origin git@github.com:username/repo.git  # Switch to SSH

# Rename remote
git remote rename origin upstream

# Remove remote
git remote remove origin
git remote rm origin              # Shorthand

# Add multiple remotes (forking workflow)
git remote add origin git@github.com:your-username/repo.git
git remote add upstream git@github.com:original-owner/repo.git
```

### Pushing Changes

```bash
# Push to remote
git push origin main              # Push main branch
git push origin feature-name      # Push specific branch
git push -u origin main           # Push and set upstream tracking
git push --set-upstream origin main  # Verbose version

# Push all branches
git push --all origin

# Push tags
git push origin v1.0.0            # Push specific tag
git push --tags                   # Push all tags
git push origin --tags            # Explicit remote

# Force push (DANGEROUS - use with caution)
git push -f origin main           # Overwrites remote history
git push --force-with-lease       # Safer force push (checks remote changes)

# Delete remote branch
git push origin --delete feature-name
git push origin :feature-name     # Alternative syntax

# Push to different remote branch name
git push origin local-branch:remote-branch
```

### Pulling Changes

```bash
# Fetch changes (download without merging)
git fetch origin                  # Fetch from origin
git fetch --all                   # Fetch from all remotes
git fetch origin main             # Fetch specific branch
git fetch --prune                 # Remove deleted remote branches

# Pull changes (fetch + merge)
git pull origin main              # Pull from specific branch
git pull                          # Pull from tracked branch
git pull --rebase                 # Pull with rebase instead of merge
git pull --no-rebase              # Ensure merge (not rebase)

# Pull with different strategies
git pull --ff-only                # Only if fast-forward possible
git pull --no-ff                  # Create merge commit even if ff possible

# Pull all branches
git pull --all

# Pull from upstream (forked repos)
git fetch upstream
git switch main
git merge upstream/main
# Or in one command:
git pull upstream main
```

### Syncing Forks

```bash
# Setup (one-time)
git remote add upstream git@github.com:original-owner/repo.git
git fetch upstream

# Sync your fork's main branch
git switch main
git fetch upstream
git merge upstream/main           # Or: git rebase upstream/main
git push origin main

# Sync and update your feature branch
git switch feature-branch
git fetch upstream
git rebase upstream/main          # Rebase on latest upstream
git push -f origin feature-branch # Force push (your branch is rewritten)
```

---

## Merging & Rebasing

### Merging

```bash
# Merge branch into current branch
git merge feature-name

# Merge with commit message
git merge feature-name -m "Merge feature: Add user profile"

# Merge strategies
git merge --ff-only feature-name  # Only if fast-forward possible
git merge --no-ff feature-name    # Always create merge commit
git merge --squash feature-name   # Combine all commits into one

# Abort merge during conflicts
git merge --abort

# Continue merge after resolving conflicts
git add resolved-file.txt
git commit                        # Completes the merge

# View merged branches
git branch --merged               # Branches merged into current
git branch --no-merged            # Branches not yet merged

# Delete merged branches
git branch -d $(git branch --merged | grep -v "^\\*" | grep -v "main" | xargs)
```

### Merge Conflicts

```bash
# When merge conflict occurs:
# 1. Git marks conflicts in files like:
<<<<<<< HEAD
Your current branch changes
=======
Incoming branch changes
>>>>>>> feature-name

# 2. Resolve conflicts manually or use tool
git mergetool                     # Opens configured merge tool

# 3. Mark as resolved
git add conflicted-file.txt

# 4. Complete the merge
git commit

# Check merge conflicts
git diff --name-only --diff-filter=U  # List conflicted files
git status                            # Also shows conflicted files

# Conflict resolution strategies
git checkout --ours filename      # Keep your version
git checkout --theirs filename    # Keep their version
git checkout --merge filename     # Re-mark conflicts (undo resolution)
```

### Rebasing

```bash
# Rebase current branch onto another
git rebase main                   # Rebase onto main
git switch feature
git rebase main                   # Move feature commits on top of main

# Interactive rebase (POWERFUL)
git rebase -i HEAD~3              # Last 3 commits
git rebase -i commit-hash         # From specific commit
git rebase -i main                # All commits since branching from main

# Interactive rebase commands:
# pick   = use commit
# reword = use commit, but edit message
# edit   = use commit, but stop for amending
# squash = combine with previous commit
# fixup  = like squash, but discard commit message
# drop   = remove commit

# Example interactive rebase session:
# pick abc123 Add feature
# reword def456 Fix bug
# squash ghi789 More bug fixes
# drop jkl012 Experimental code

# During rebase:
git rebase --continue             # After resolving conflicts
git rebase --skip                 # Skip current commit
git rebase --abort                # Cancel rebase

# Rebase vs Merge
git rebase main                   # Linear history (cleaner)
git merge main                    # Preserves exact history (safer)

# Rebase onto different base
git rebase --onto new-base old-base branch-name

# Update feature branch with main changes
git switch feature
git rebase main
# Or with pull:
git pull --rebase origin main
```

### Cherry-Picking

```bash
# Apply specific commit to current branch
git cherry-pick commit-hash

# Cherry-pick multiple commits
git cherry-pick commit1 commit2 commit3

# Cherry-pick range of commits
git cherry-pick commit1^..commit2

# Cherry-pick without committing
git cherry-pick -n commit-hash
git cherry-pick --no-commit commit-hash

# Continue/abort cherry-pick
git cherry-pick --continue
git cherry-pick --abort
```

---

## Undoing Changes

### Discarding Changes

```bash
# Discard unstaged changes in file
git restore filename.txt          # Modern way
git checkout -- filename.txt      # Old way

# Discard all unstaged changes
git restore .
git checkout -- .

# Discard staged changes (unstage)
git restore --staged filename.txt
git reset HEAD filename.txt       # Old way

# Discard all changes (staged and unstaged) - DANGEROUS
git reset --hard HEAD

# Restore file from specific commit
git restore --source=commit-hash filename.txt
git restore --source=HEAD~3 filename.txt
```

### Undoing Commits

```bash
# Undo last commit, keep changes staged
git reset --soft HEAD~1

# Undo last commit, keep changes unstaged
git reset --mixed HEAD~1          # Default
git reset HEAD~1

# Undo last commit, discard all changes - DANGEROUS
git reset --hard HEAD~1

# Undo multiple commits
git reset --soft HEAD~3           # Last 3 commits
git reset commit-hash             # Reset to specific commit

# Create new commit that undoes previous commit (safe for public history)
git revert commit-hash
git revert HEAD                   # Revert last commit
git revert HEAD~3                 # Revert 4th-to-last commit

# Revert merge commit
git revert -m 1 merge-commit-hash

# Revert multiple commits
git revert commit1 commit2 commit3
git revert commit1^..commit3      # Range

# Reset to remote state
git fetch origin
git reset --hard origin/main      # DANGEROUS: Discards all local changes
```

### Recovering Lost Commits

```bash
# View reflog (history of HEAD positions)
git reflog
git reflog show HEAD

# Recover deleted commit/branch
git reflog                        # Find lost commit hash
git switch -c recovered-branch commit-hash
git cherry-pick commit-hash       # Or cherry-pick it

# View all reachable objects
git fsck --lost-found

# Recover deleted file
git rev-list -n 1 HEAD -- deleted-file.txt
git checkout commit-hash^ -- deleted-file.txt
```

---

## Advanced Operations

### Stashing

```bash
# Save uncommitted changes
git stash                         # Stash tracked files
git stash -u                      # Include untracked files
git stash -a                      # Include ignored files too
git stash push -m "Work in progress on feature X"

# List stashes
git stash list

# Apply stash
git stash apply                   # Apply latest stash, keep in list
git stash apply stash@{2}         # Apply specific stash
git stash pop                     # Apply latest stash and remove from list
git stash pop stash@{2}

# View stash contents
git stash show                    # Summary
git stash show -p                 # Full diff
git stash show stash@{1} -p

# Create branch from stash
git stash branch branch-name stash@{1}

# Remove stash
git stash drop stash@{1}          # Remove specific stash
git stash clear                   # Remove all stashes
```

### Tagging

```bash
# List tags
git tag
git tag -l "v1.*"                 # Filter tags

# Create lightweight tag
git tag v1.0.0

# Create annotated tag (recommended)
git tag -a v1.0.0 -m "Release version 1.0.0"

# Tag specific commit
git tag -a v1.0.0 commit-hash -m "Release 1.0.0"

# View tag information
git show v1.0.0

# Push tags to remote
git push origin v1.0.0            # Push specific tag
git push origin --tags            # Push all tags
git push --follow-tags            # Push commits + reachable tags

# Delete tag
git tag -d v1.0.0                 # Delete local tag
git push origin --delete v1.0.0   # Delete remote tag
git push origin :refs/tags/v1.0.0 # Alternative syntax

# Checkout tag
git checkout v1.0.0               # Detached HEAD state
git switch -c branch-name v1.0.0  # Create branch from tag
```

### Submodules

```bash
# Add submodule
git submodule add <https://github.com/user/repo.git> path/to/submodule

# Clone repository with submodules
git clone --recurse-submodules <https://github.com/user/repo.git>

# Initialize submodules after clone
git submodule init
git submodule update

# Or in one command:
git submodule update --init --recursive

# Update submodules to latest commit
git submodule update --remote

# View submodule status
git submodule status

# Remove submodule
git submodule deinit path/to/submodule
git rm path/to/submodule
rm -rf .git/modules/path/to/submodule
```

### Worktrees

```bash
# Create worktree (work on multiple branches simultaneously)
git worktree add ../project-feature feature-branch

# List worktrees
git worktree list

# Remove worktree
git worktree remove ../project-feature

# Prune stale worktree info
git worktree prune
```

### Bisect (Find Bug Introduction)

```bash
# Start bisect session
git bisect start
git bisect bad                    # Current commit is bad
git bisect good commit-hash       # Known good commit

# Git checks out middle commit
# Test it, then:
git bisect good                   # If test passes
git bisect bad                    # If test fails

# Repeat until Git finds the problematic commit

# Automated bisect
git bisect start HEAD v1.0.0
git bisect run ./test-script.sh

# End bisect
git bisect reset
```

### Blame & History

```bash
# Show who changed each line
git blame filename.txt
git blame -L 10,20 filename.txt   # Lines 10-20 only
git blame -C filename.txt         # Detect moved/copied lines

# Show file history
git log -- filename.txt
git log --follow -- filename.txt  # Follow renames
git log -p -- filename.txt        # With diffs

# Show file at specific revision
git show commit-hash:path/to/file.txt

# Find when string was added/removed
git log -S "search string" --source --all
git log -G "regex pattern" --source --all
```

---

## Collaboration Workflows

### Pull Request Workflow

```bash
# 1. Fork repository on GitHub

# 2. Clone your fork
git clone git@github.com:your-username/repo.git
cd repo

# 3. Add upstream remote
git remote add upstream git@github.com:original-owner/repo.git

# 4. Create feature branch
git switch -c feature/awesome-feature

# 5. Make changes and commit
git add .
git commit -m "Add awesome feature"

# 6. Push to your fork
git push -u origin feature/awesome-feature

# 7. Create Pull Request on GitHub

# 8. Sync with upstream during review
git fetch upstream
git rebase upstream/main
git push -f origin feature/awesome-feature

# 9. After PR is merged
git switch main
git pull upstream main
git push origin main
git branch -d feature/awesome-feature
git push origin --delete feature/awesome-feature
```

### Code Review Tips

```bash
# View changes in PR locally
git fetch origin pull/123/head:pr-123
git switch pr-123

# Or add to .git/config:
# [remote "origin"]
#     fetch = +refs/pull/*/head:refs/remotes/origin/pr/*
git fetch origin
git switch pr-123

# Review changes
git diff main...pr-123
git log main..pr-123

# Test and provide feedback on GitHub
```

### Collaborative Branching

```bash
# Share WIP branch with team
git push -u origin wip/feature-x

# Team member fetches and contributes
git fetch origin
git switch -c wip/feature-x origin/wip/feature-x
# Make changes
git push origin wip/feature-x

# Sync your local branch
git pull --rebase origin wip/feature-x
```

---

## Troubleshooting

### Common Issues

```bash
# "Detached HEAD" state
# You're not on any branch
git switch main                   # Return to branch
git switch -c new-branch          # Create branch from current state

# "Your branch has diverged"
git fetch origin
git reset --hard origin/main      # DANGEROUS: Discard local changes
# Or:
git pull --rebase origin main     # Try to rebase

# "Refusing to merge unrelated histories"
git pull origin main --allow-unrelated-histories

# Large files rejected by GitHub
git filter-branch --tree-filter 'rm -rf large-file' HEAD
# Or use BFG Repo-Cleaner (better):
# bfg --delete-files large-file.zip

# Remove sensitive data from history
git filter-branch --force --index-filter \\
  "git rm --cached --ignore-unmatch path/to/secret.txt" \\
  --prune-empty --tag-name-filter cat -- --all

# Or use git-filter-repo (modern, recommended)
git filter-repo --path path/to/secret.txt --invert-paths

# Accidentally committed to main instead of feature branch
git switch -c feature-branch      # Create branch with current commits
git switch main
git reset --hard origin/main      # Reset main to remote state
git switch feature-branch         # Continue work

# Wrong commit message
git commit --amend -m "Correct message"  # If not pushed
# If already pushed:
git revert commit-hash            # Safer for shared branches

# Pushed to wrong branch
git push origin :wrong-branch     # Delete remote branch
git push -u origin correct-branch # Push to correct branch
```

### Reset vs Revert vs Rebase

```bash
# RESET - Moves branch pointer (rewrites history)
# Use for: Local-only commits you want to undo
git reset --soft HEAD~1           # Undo commit, keep changes staged
git reset --mixed HEAD~1          # Undo commit, unstage changes (default)
git reset --hard HEAD~1           # Undo commit, discard changes

# REVERT - Creates new commit undoing previous commit (preserves history)
# Use for: Undoing commits already pushed to shared branches
git revert commit-hash            # Safe for public history

# REBASE - Reapplies commits on new base (rewrites history)
# Use for: Cleaning up local commits before pushing
git rebase -i HEAD~3              # Interactive rebase to squash/reorder
```

### Checking Repository Health

```bash
# Verify repository integrity
git fsck --full

# Check for corruption
git fsck --no-reflogs

# Cleanup and optimize
git gc                            # Garbage collection
git gc --aggressive               # More thorough cleanup
git prune                         # Remove unreachable objects

# Repository statistics
git count-objects -v              # Object count and size
git ls-files                      # List tracked files
```

---

## Best Practices

### Commit Messages

```bash
# Good commit message format:
<type>: <subject>

<body>

<footer>

# Types:
# feat: New feature
# fix: Bug fix
# docs: Documentation changes
# style: Code style (formatting, missing semicolons, etc.)
# refactor: Code refactoring
# test: Adding tests
# chore: Maintenance tasks

# Examples:
feat: Add user authentication with JWT

Implement JWT-based authentication system:
- Add login/logout endpoints
- Create middleware for protected routes
- Add token refresh mechanism

Closes #123

fix: Prevent race condition in user registration

Previously, concurrent registrations could create duplicate users.
Added database constraint and improved error handling.

Fixes #456
```

### Branch Naming Conventions

```bash
# Feature branches
feature/user-authentication
feature/dark-mode
feat/issue-123-add-search

# Bug fixes
fix/login-validation
bugfix/memory-leak
hotfix/critical-security-issue

# Releases
release/v1.2.0
release/2024-03-15

# Experimental
experiment/new-algorithm
spike/performance-test

# Personal branches
username/feature-description
john/refactor-api

# Use lowercase and hyphens
# Be descriptive but concise
# Include issue numbers when relevant
```

### Workflow Best Practices

```bash
# 1. Commit early and often
# Small, focused commits are easier to review and revert

# 2. Write meaningful commit messages
# Future you (and your team) will thank you

# 3. Keep main/master stable
# Never commit directly to main
# Use feature branches and pull requests

# 4. Pull before you push
git pull --rebase origin main     # Stay up to date

# 5. Review changes before committing
git diff --staged                 # Review what you're committing
git status                        # Double-check file list

# 6. Don't commit generated files
# Add them to .gitignore

# 7. Use .gitignore from start
# Don't commit and then ignore

# 8. One feature per branch
# Keeps changes focused and reviewable

# 9. Delete merged branches
git branch -d feature-name        # Keep repository clean

# 10. Use tags for releases
git tag -a v1.0.0 -m "Release 1.0.0"
```

### Security Best Practices

```bash
# Never commit:
# - API keys
# - Passwords
# - Private keys
# - Tokens
# - Environment files (.env)

# Use environment variables instead
# Use secret management services (AWS Secrets Manager, etc.)

# If you accidentally commit secrets:
# 1. Rotate the compromised credentials IMMEDIATELY
# 2. Remove from history using git-filter-repo or BFG
# 3. Force push the cleaned history
# 4. Notify your team

# Enable secret scanning
# GitHub has automatic secret scanning
# Use pre-commit hooks to prevent commits with secrets

# Example pre-commit hook (.git/hooks/pre-commit):
#!/bin/sh
if git diff --cached | grep -E 'API_KEY|PASSWORD|SECRET'; then
    echo "ERROR: Possible secret detected!"
    exit 1
fi
```

### Useful Aliases

```bash
# Add to ~/.gitconfig or use git config --global alias.name "command"

[alias]
    # Status
    st = status -sb

    # Log
    lg = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit
    lol = log --graph --decorate --oneline --all
    last = log -1 HEAD --stat

    # Diff
    df = diff --color --color-words --abbrev
    dfs = diff --staged

    # Commit
    cm = commit -m
    cam = commit -am
    amend = commit --amend --no-edit

    # Branch
    br = branch
    bra = branch -a

    # Checkout/Switch
    co = checkout
    sw = switch
    swc = switch -c

    # Reset
    undo = reset --soft HEAD~1
    unstage = reset HEAD --

    # Remote
    pushu = push -u origin HEAD

    # Stash
    stashup = stash -u
    pop = stash pop

    # Misc
    aliases = config --get-regexp ^alias\\\\.
    contributors = shortlog -sn
```

---

## Quick Reference Cheat Sheet

```bash
### SETUP
git config --global user.name "Name"
git config --global user.email "email@example.com"
git init
git clone <url>

### BASIC WORKFLOW
git status
git add <file>
git add .
git commit -m "message"
git push origin main

### BRANCHING
git branch                    # List branches
git branch <name>             # Create branch
git switch <name>             # Switch branch
git switch -c <name>          # Create & switch
git merge <name>              # Merge into current
git branch -d <name>          # Delete branch

### REMOTES
git remote add origin <url>
git remote -v
git push -u origin main
git pull origin main
git fetch origin

### UNDOING
git restore <file>            # Discard unstaged changes
git restore --staged <file>   # Unstage
git reset --soft HEAD~1       # Undo commit, keep changes
git reset --hard HEAD~1       # Undo commit, discard changes
git revert <commit>           # Safe undo for public history

### HISTORY
git log --oneline
git log --graph --all
git diff
git show <commit>

### ADVANCED
git stash                     # Save WIP
git stash pop                 # Apply stash
git rebase main               # Reapply commits
git cherry-pick <commit>      # Apply specific commit
git tag -a v1.0 -m "message"  # Create tag
```

---

## Additional Resources

### GitHub Specific

```bash
# GitHub CLI (gh)
gh repo create
gh pr create
gh pr checkout 123
gh pr merge
gh issue create
gh issue list

# GitHub Actions (CI/CD)
# .github/workflows/ci.yml
name: CI
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - run: npm test
```

### Learning Resources

- **Official Git Documentation**: [https://git-scm.com/doc](https://git-scm.com/doc)
- **GitHub Guides**: [https://guides.github.com](https://guides.github.com)
- **Interactive Learning**: [https://learngitbranching.js.org](https://learngitbranching.js.org)
- **Git Cheat Sheet**: [https://education.github.com/git-cheat-sheet-education.pdf](https://education.github.com/git-cheat-sheet-education.pdf)
- **Pro Git Book** (free): [https://git-scm.com/book/en/v2](https://git-scm.com/book/en/v2)

### Advanced Topics to Explore

- Git hooks (pre-commit, pre-push, etc.)
- Git LFS (Large File Storage)
- Monorepo management
- Git submodules vs. subtrees
- Sparse checkout
- Git internals (objects, refs, packfiles)
- Custom merge drivers
- Git attributes for line endings, diff, and merge

---

**Remember**: Git is a powerful tool. When in doubt, create a backup branch before performing destructive operations!

```bash
# Golden rule: When unsure, backup first!
git branch backup-$(date +%Y%m%d-%H%M%S)
```

---

_Last but not least: Created with ❤️ for developers who want to master Git_
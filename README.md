# Awesome Git & GitHub

> A comprehensive, beginner-friendly guide to Git and GitHub with practical workflows, diagrams, mental models, and real-world examples.

Learn Git and GitHub from first principles through clear explanations, visual diagrams, command references, and practical workflows. This guide covers everything from version control fundamentals to branching, remote repositories, pull requests, merging, and collaboration.

---

## 📚 Topics Covered

- Version Control Fundamentals
- Problems Solved by Version Control
- Version Control System (VCS)
- Benefits of Version Control
- Popular Version Control Systems
- Why Git?
- Git vs GitHub
- Repository Hosting Platforms
- Installing Git
- Configuring Git Identity
- Local and Remote Repositories
- Creating a Repository (`git init`)
- Cloning a Repository (`git clone`)
- Git Three-State Architecture
  - Working Directory
  - Staging Area (Index)
  - Repository (Commits)
- Checking Repository Status (`git status`)
- Staging Changes (`git add`)
- Creating Commits (`git commit`)
- Viewing Commit History (`git log`, `git show`)
- Git Branches
  - Creating Branches
  - Switching Branches
  - Branch Isolation
- Connecting a Local Repository to GitHub
- Remote Repositories and `origin`
- Upstream Tracking Branches
- Pushing Branches (`git push`)
- Pull Requests (PR)
- Merging Branches
- Git Pull (`git pull`)
- Amending the Latest Commit (`git commit --amend`)
- Common Beginner Mistakes
- Best Practices
- Professional Git Workflows
- Command References
- Mental Models and Diagrams

---

## 🎯 Who This Guide Is For

- Beginners learning Git and GitHub
- University students
- Competitive programmers
- Open-source contributors
- Software engineering interns
- Developers preparing for collaborative projects

---

## 🚀 What You'll Learn

By the end of this guide, you'll be able to:

- Understand why version control is essential.
- Understand the difference between Git and GitHub.
- Install and configure Git correctly.
- Create and manage Git repositories.
- Track, stage, and commit changes confidently.
- Navigate Git history.
- Work effectively with branches.
- Connect local repositories to GitHub.
- Push and pull changes safely.
- Collaborate using Pull Requests.
- Merge branches confidently.
- Follow Git workflows used in professional software development.
- Avoid common Git mistakes and understand Git's internal workflow.

---


# Git & GitHub — Introduction

## Problems Solved by Version Control

|Problem|Cause|Solution via Version Control|
|---|---|---|
|Lost work|Project deleted, disk failure, system crash, no backup|Backup and recover previous versions|
|Cannot restore working code|New changes break application|Roll back to any previous working version|
|Team confusion|Multiple copies (`final`, `final_v2`, `final_last`)|Single source of truth with version history|
|No history|Unknown who introduced a bug|Complete change history with author and purpose|
|Fear of experimentation|Risk of breaking stable code|Isolated development environment (branches/sandbox)|

---

# Version Control System (VCS)

## Definition

A **Version Control System (VCS)** records and tracks every change made to a project over time.

## Capabilities

- Records every file change
    
- Tracks complete project history
    
- Restores any previous version
    
- Identifies:
    
    - Who made a change
        
    - What changed
        
    - Why it changed (commit message)
        
- Eliminates multiple project copies
    
- Supports safe team collaboration
    

---

# Benefits

- Automatic project history
    
- Version rollback
    
- Reliable backup
    
- Team collaboration
    
- Change tracking
    
- Safer feature development
    
- Single project folder instead of multiple duplicate folders
    

---

# Popular Version Control Systems

|VCS|Notes|
|---|---|
|Git|Fast, reliable, distributed; industry standard|
|CVS|Older VCS|
|SVN (Subversion)|Centralized VCS|

---

# Why Git?

- Fast
    
- Reliable
    
- Distributed architecture
    
- Used by ~94% of developers
    
- Adopted by major companies (e.g., Google, Microsoft)
    

---

# Git vs GitHub

|Git|GitHub|
|---|---|
|Version control software|Cloud hosting platform for Git repositories|
|Installed locally|Hosted online|
|Works offline|Requires internet|
|Tracks project history|Stores Git repositories remotely|
|Manages versions|Enables collaboration between developers|
|Open source|Cloud service built around Git|

---

# Repository Hosting Platforms

Git repositories can be hosted on:

- GitHub
    
- GitLab
    
- Bitbucket
    
- Other Git hosting services
    

---

# Concept Relationships

```
Project
   │
   ▼
Git
(Local version control)
   │
   ▼
Repository
   │
   ▼
GitHub / GitLab / Bitbucket
(Remote hosting & collaboration)
```









# Git Installation (Windows)

## Download

1. Search **Git install**.
    
2. Open the official Git website.
    
3. Navigate to **Windows**.
    
4. Download **Git for Windows**.
    

---

# Installation

Use the default installation options unless customization is required.

## Important Installation Option

### Default Initial Branch Name

During installation, Git allows configuring the default branch created by `git init`.

|Option|Meaning|
|---|---|
|`master`|Git default (selected in this course)|
|`main`|Common modern alternative|
|Custom name|Any user-defined branch name|

---

### PATH Configuration

Select:

```
Git from the command line and also from 3rd-party software
```

This makes Git accessible from the terminal and external applications.

---

# Verify Installation

Check the installed Git version:

```bash
git --version
```

Example output:

```text
git version 2.54.4
```

---

# Configure Git Identity

Set the global username:

```bash
git config --global user.name "Your Name"
```

Set the global email:

```bash
git config --global user.email "your@email.com"
```

---

# Purpose of Git Identity

Git records this information for every commit:

- Author name
    
- Author email
    

These become the default identity for all local repositories unless overridden.

---

# Result

After installation and identity configuration, the local Git environment is ready for use.












# Git Core Concepts — Repository

## Repository

### Definition

A **repository (repo)** is a **project folder tracked by Git**.

A Git repository stores:

- Project files
    
- Complete history of every file change
    

This enables:

- Version history
    
- Backup
    
- Rollback to previous versions
    
- Change tracking
    

---

# Initialize a Repository

Convert an existing project folder into a Git repository:

```bash
git init
```

### Effect

- Git starts tracking the project.
    
- A hidden `.git` directory is created.
    

---

# `.git` Directory

Created automatically after `git init`.

Contains Git's internal data, including:

- Repository metadata
    
- Commit history
    
- Configuration
    
- Object database
    
- References (branches, tags, etc.)
    

> A folder containing `.git` is a Git repository.

---

# Repository Types

|Local Repository|Remote Repository|
|---|---|
|Stored on the local machine|Hosted on a remote server (e.g., GitHub)|
|Used for local development|Used for backup and collaboration|
|Works offline|Requires network access|

---

# Local Repository Workflow

```text
Create Project Folder
        │
        ▼
git init
        │
        ▼
.git created
        │
        ▼
Local Git Repository
```

---

# Remote Repository Workflow

```text
Local Repository
       │
 Publish (push)
       ▼
Remote Repository (GitHub/GitLab/Bitbucket)
```

Purpose:

- Backup
    
- Team collaboration
    
- Shared source of truth
    

---

# Cloning a Remote Repository

Create a local copy of an existing remote repository:

```bash
git clone <repository-url>
```

Example:

```bash
git clone https://github.com/user/repository.git
```

### Process

```text
Remote Repository
        │
git clone
        ▼
Local Repository
```

Result:

- Downloads all project files.
    
- Downloads the complete Git history.
    
- Creates a `.git` directory locally.
    
- Produces a fully functional local repository.
    

---

# Obtaining the Repository URL

On GitHub:

```
Repository
    └── Code
          └── Copy HTTPS URL
```

Use the copied URL with `git clone`.

---

# Core Commands

|Command|Purpose|
|---|---|
|`git init`|Initialize Git tracking for an existing project folder|
|`git clone <url>`|Download an existing remote repository with its complete history|

---

# Repository Lifecycle

```text
New Project Folder
        │
   git init
        │
        ▼
Local Repository (.git)
        │
      Push
        │
        ▼
Remote Repository
        │
   git clone
        ▼
Another Local Repository
```

---

# Key Facts

- A repository is simply a Git-tracked project folder.
    
- `git init` creates a new local repository by adding a hidden `.git` directory.
    
- The `.git` directory contains all Git metadata and history.
    
- Every project typically has one local repository and may have one or more remote repositories.
    
- Remote repositories enable backup and collaboration.
    
- `git clone` copies both the project files and the entire Git history from a remote repository to a local machine.










# Git Three-State Architecture [git -> add, commit, log]

## Three States of a Git File

|State|Purpose|Contents|
|---|---|---|
|**Working Directory**|Local workspace where files are created or modified|New (untracked), modified, or tracked files|
|**Staging Area (Index)**|Selects changes for the next commit|Files prepared for committing|
|**Repository**|Permanent project history|Commits (snapshots)|

### Flow

```text
Working Directory
        │
   git add
        │
        ▼
 Staging Area
        │
 git commit
        │
        ▼
   Repository
```

---

# Working Directory

A file in the working directory can be:

- **Tracked** (already exists in Git history)
    
- **Modified** (tracked file changed)
    
- **Untracked** (new file not yet tracked)
    

Check current state:

```bash
git status
```

Example output:

- `Untracked files` → New files
    
- `Modified` → Existing tracked files changed
    

---

# Staging Area

Purpose:

- Select only the files that should become part of the next commit.
    
- Not every modified file must be committed.
    

Move one file to staging:

```bash
git add <filename>
```

Example:

```bash
git add index.html
```

Move **all** changes to staging:

```bash
git add .
```

After staging:

```bash
git status
```

shows files as **ready to commit**.

---

# Repository (Commit)

A **commit** is a **permanent snapshot** of all staged files.

A commit stores:

|Metadata|Description|
|---|---|
|Commit message|Purpose of the change|
|Author|Who made the commit|
|Timestamp|When it was created|
|Parent commit|Previous commit reference|
|Commit ID (SHA)|Unique identifier|

Create a commit:

```bash
git commit -m "Add index.html"
```

Example:

```bash
git commit -m "Add index.css and update index.html"
```

After a successful commit:

```bash
git status
```

Output:

```text
nothing to commit, working tree clean
```

Meaning:

- No staged changes remain.
    
- Working directory matches the latest commit.
    

---

# Commit Properties

|Property|Description|
|---|---|
|Permanent|Represents a saved project state|
|Snapshot|Captures staged files only|
|Unique ID|Generated using SHA hashing|
|Immutable|Cannot be modified after creation|

---

# Viewing Commit History

Show commit history:

```bash
git log
```

Compact one-line history:

```bash
git log --oneline
```

---

# Viewing Commit Details

Show complete information for a commit:

```bash
git show <commit-id>
```

Example:

```bash
git show cb0f68
```

Displays:

- Author
    
- Date & time
    
- Commit message
    
- Changes (diff)
    
- Commit SHA
    

---

# Typical Workflow

```text
Create/Edit Files
        │
git status
        │
git add <file>
or
git add .
        │
git status
        │
git commit -m "Meaningful message"
        │
git log --oneline
        │
git show <commit-id>
```

---

# Essential Commands

| Command                   | Purpose                           |
| ------------------------- | --------------------------------- |
| `git status`              | Show current repository state     |
| `git add <file>`          | Stage a specific file             |
| `git add .`               | Stage all changes                 |
| `git commit -m "message"` | Create a commit from staged files |
| `git log`                 | Show commit history               |
| `git log --oneline`       | Compact commit history            |
| `git show <commit-id>`    | Show details of a specific commit |










# Git Branches

## Definition

A **branch** is an **isolated workspace** that allows independent development without affecting the main project.

After changes are completed and tested, they can be merged into the main branch.

---

# Why Branches Exist

|Problem|Branch Solution|
|---|---|
|Fear of breaking the main project|Develop safely in an isolated environment|
|Multiple developers working simultaneously|Each developer works in a separate branch|
|Feature development|Every feature can have its own branch|
|Experimentation|Test ideas without affecting the stable codebase|

---

# Branch Isolation

```text
                 main (stable)
                      │
          ┌───────────┼───────────┐
          │           │           │
     feature-login feature-auth feature-cart
          │           │           │
     Independent development & testing
          │           │           │
          └────── Merge into main ──────►
```

Changes inside one branch **do not affect** other branches until they are merged.

---

# Default Branch

When a repository is initialized using:

```bash
git init
```

Git automatically creates a **default branch**.

The default branch name depends on Git configuration (commonly `main` or `master`).

---

# Branch Commands

## List All Local Branches

```bash
git branch
```

Example:

```text
* master
  feature-login
```

- `*` indicates the **current branch**.
    

---

## Create a New Branch

```bash
git branch <branch-name>
```

Example:

```bash
git branch feature-login
```

Creates the branch **without switching** to it.

---

## Switch to an Existing Branch

### Modern (Recommended)

```bash
git switch <branch-name>
```

Example:

```bash
git switch feature-login
```

### Legacy (Still Common)

```bash
git checkout <branch-name>
```

Example:

```bash
git checkout feature-login
```

Both commands switch the current working branch.

---

## Create and Switch in One Command

### Modern (Recommended)

```bash
git switch -c <branch-name>
```

Example:

```bash
git switch -c feature-auth
```

### Legacy Equivalent

```bash
git checkout -b <branch-name>
```

Example:

```bash
git checkout -b feature-auth
```

Both commands:

1. Create a new branch.
    
2. Immediately switch to it.
    

---

# Typical Feature Workflow

Create a feature branch:

```bash
git switch -c feature-login
```

Create files:

```text
login.html
```

Check status:

```bash
git status
```

Stage changes:

```bash
git add .
```

Commit:

```bash
git commit -m "Add login page"
```

At this point:

- The commit exists **only** in `feature-login`.
    
- `main/master` remains unchanged.
    

---

# Branch Isolation Example

Suppose:

```text
master
├── index.html
└── index.css
```

Create and switch:

```bash
git switch -c feature-login
```

Add:

```text
login.html
```

Commit it.

Repository now becomes:

```text
master
├── index.html
└── index.css

feature-login
├── index.html
├── index.css
└── login.html
```

Switch back:

```bash
git switch master
```

or

```bash
git checkout master
```

Result:

```text
master
├── index.html
└── index.css
```

`login.html` disappears because it exists only in `feature-login`.

This demonstrates that **each branch has its own snapshot/history**.

---

# Command Summary

|Command|Purpose|
|---|---|
|`git branch`|List local branches|
|`git branch <name>`|Create a branch|
|`git switch <name>`|Switch to an existing branch (recommended)|
|`git checkout <name>`|Switch to an existing branch (legacy)|
|`git switch -c <name>`|Create and switch to a new branch (recommended)|
|`git checkout -b <name>`|Create and switch to a new branch (legacy)|
|`git status`|Show current branch and file status|
|`git add .`|Stage all changes|
|`git commit -m "message"`|Save a snapshot of staged changes|

---

# Key Concepts

| Concept                             | Description                                                 |
| ----------------------------------- | ----------------------------------------------------------- |
| Branch                              | Independent line of development                             |
| Default Branch                      | Automatically created after `git init` (`main` or `master`) |
| Current Branch                      | Marked with `*` in `git branch`                             |
| Branch Isolation                    | Changes remain inside the current branch until merged       |
| Commit                              | Snapshot stored only in the current branch                  |
| `git switch`                        | Modern command for switching branches                       |
| `git checkout`                      | Legacy command for switching branches and other operations  |
| `git switch -c` / `git checkout -b` | Create a branch and switch to it in one step                |












# Connecting a Local Git Repository to GitHub (Remote Repository)

## Local vs Remote Repository

|Repository|Location|Purpose|
|---|---|---|
|**Local Repository**|Your computer|Development, commits, branches|
|**Remote Repository**|GitHub (or GitLab, Bitbucket, etc.)|Backup, collaboration, code sharing|

> Git is the version control system. GitHub is a hosting service for Git repositories.

---

# Overall Workflow

```text
Create Local Repository
        │
Create GitHub Repository
        │
Connect Local ↔ Remote
        │
Push Local Branches
        │
Continue Development
        │
git push
```

---

# Step 1: Create a GitHub Repository

On GitHub:

1. **New Repository**
    
2. Repository name (preferably same as local project)
    
3. Choose **Public** or **Private**
    
4. Do **NOT** initialize with:
    
    - README
        
    - .gitignore
        
    - License
        

Reason:

- The local repository already exists.
    
- Creating initial files on GitHub creates an unnecessary initial commit that may complicate the first push.
    

---

# Step 2: Connect Local Repository to GitHub

Add a remote named **origin**:

```bash
git remote add origin <repository-url>
```

Example:

```bash
git remote add origin https://github.com/username/student-portal.git
```

### What happens?

Git stores:

```text
origin
    ↓
https://github.com/username/student-portal.git
```

Now your local repository knows where the remote repository is located.

> `origin` is only a **name (alias)** for the remote. It is **not** a Git keyword. Any name can be used, but `origin` is the convention.

---

# Verify Remote Connection

```bash
git remote -v
```

Example:

```text
origin  https://github.com/username/student-portal.git (fetch)
origin  https://github.com/username/student-portal.git (push)
```

---

# Remote Tracking Branches

Each local branch can be linked to a corresponding remote branch.

Example:

```text
Local                     Remote

master      ─────────►    origin/master
feature-login ───────►    origin/feature-login
feature-auth  ───────►    origin/feature-auth
```

This relationship is called an **upstream tracking branch**.

Benefits:

- `git push` knows where to push.
    
- `git pull` knows where to pull from.
    
- Git can compare local and remote branch status.
    

---

# Push Existing Local Branches

## First Push (Set Upstream)

```bash
git push -u origin <branch-name>
```

Example:

```bash
git push -u origin master
```

or

```bash
git push -u origin feature-login
```

### What `-u` (`--set-upstream`) Does

It performs **two operations**:

1. Pushes the branch to GitHub.
    
2. Links the local branch with the remote branch.
    

Equivalent relationship:

```text
master
    │
    ▼
origin/master
```

After this mapping is created:

```bash
git push
```

is sufficient.

---

# Push Every Existing Branch (One Time)

If multiple local branches already exist:

```bash
git push --all origin
```

However, **this does NOT automatically create upstream tracking for every branch**.

For each branch, you should still run:

```bash
git push -u origin <branch-name>
```

> Modern Git workflows typically push branches individually as they are created rather than pushing all branches at once.

---

# Creating a New Feature Branch

Recommended:

```bash
git switch -c feature-logout
```

Legacy equivalent:

```bash
git checkout -b feature-logout
```

Current state:

```text
master
        │
        └────────► feature-logout
```

---

# First Push of a New Branch

Suppose you created:

```text
feature-logout
```

Initially:

```text
Local
feature-logout

Remote
(nothing)
```

Running:

```bash
git push
```

fails because Git doesn't know which remote branch should receive it.

Correct command:

```bash
git push -u origin feature-logout
```

Result:

```text
Local                     Remote

feature-logout ───────► origin/feature-logout
```

The upstream relationship is now established.

---

# Future Development

Edit files.

Check changes:

```bash
git status
```

Stage:

```bash
git add .
```

Commit:

```bash
git commit -m "Add logout page"
```

Push:

```bash
git push
```

No `-u` is needed because the upstream was already configured during the first push.

---

# Typical GitHub Workflow

```text
Create Repository on GitHub
            │
git remote add origin URL
            │
git push -u origin master
            │
Create Feature Branch
            │
git switch -c feature-login
            │
Edit Files
            │
git add .
            │
git commit -m "..."
            │
First Push:
git push -u origin feature-login
            │
Later Commits:
git push
```

---

# Common Beginner Mistakes

|Mistake|Correct Approach|
|---|---|
|`git push` on a newly created branch|First use `git push -u origin <branch>`|
|Confusing Git with GitHub|Git = version control; GitHub = remote hosting service|
|Thinking `origin` is a special keyword|`origin` is just the conventional name of the remote|
|Assuming commits automatically appear on GitHub|Commits remain local until `git push`|
|Assuming `git add` uploads files|`git add` only stages changes locally|
|Assuming `git commit` uploads changes|`git commit` only creates a local snapshot|
|Creating README on GitHub when pushing an existing local repo|Leave repository empty unless you intend to merge histories|

---

# Command Reference

|Command|Purpose|
|---|---|
|`git remote add origin <url>`|Connect local repository to GitHub|
|`git remote -v`|Show configured remotes|
|`git push -u origin <branch>`|First push + establish upstream tracking|
|`git push`|Push commits to the tracked remote branch|
|`git push --all origin`|Push all local branches (does not replace per-branch upstream setup)|
|`git switch -c <branch>`|Create and switch to a new branch|
|`git checkout -b <branch>`|Legacy equivalent of `git switch -c`|
|`git status`|Show repository status|
|`git add .`|Stage all changes|
|`git commit -m "message"`|Create a local commit|

---

# Mental Model

```text
Working Directory
        │
git add
        ▼
Staging Area
        │
git commit
        ▼
Local Repository
        │
git push
        ▼
GitHub (Remote Repository)
```

**Key distinction:**

- `git add` → prepares changes.
    
- `git commit` → saves changes locally.
    
- `git push` → uploads commits to GitHub.
    
- `git pull` (covered later) → downloads commits from GitHub.










# Pull Request (PR) and Merge

## Definition

A **Pull Request (PR)** is a request to merge changes from one branch (**source/head branch**) into another (**target/base branch**).

It enables:

- Code review
    
- Discussion
    
- Automated testing (CI)
    
- Approval before merging
    

> In most professional teams, developers **never commit directly to `main`/`master`**. They work in feature branches and merge through Pull Requests.

---

# Branch-Based Workflow

```text
main (production)
      │
      ├──────────────► feature-login
      │                    │
      │               Development
      │                    │
      │               git push
      │                    │
      │               Pull Request
      │                    │
      │             Code Review
      │                    │
      └────────────── Merge ◄─────────────
```

---

# Standard Git Workflow

```text
Create Branch
      │
Develop
      │
git add
      │
git commit
      │
git push
      │
Create Pull Request
      │
Review & Approval
      │
Merge
      │
Delete Feature Branch (optional)
```

---

# Step 1 — Create a Feature Branch

## Recommended

```bash
git switch -c feature-auth
```

## Legacy

```bash
git checkout -b feature-auth
```

---

# Step 2 — Develop

Example:

```text
auth.html
```

Check status:

```bash
git status
```

Stage:

```bash
git add .
```

Commit:

```bash
git commit -m "Add authentication page"
```

---

# Step 3 — Push the Branch

First push:

```bash
git push -u origin feature-auth
```

Later pushes:

```bash
git push
```

---

# GitHub Pull Request

After pushing the branch:

```
feature-auth
        │
        ▼
GitHub
```

GitHub detects that the branch is ahead of `main/master` and offers:

> **Compare & pull request**

Or manually:

```
Repository
    └── Pull Requests
            └── New Pull Request
```

---

# Creating a Pull Request

Choose:

|Option|Description|
|---|---|
|**Base branch**|Branch receiving changes (usually `main` or `master`)|
|**Compare branch**|Branch containing new changes (e.g., `feature-auth`)|

Example:

```text
Base:     master
Compare:  feature-auth
```

Then:

- Add title
    
- Add description (optional but recommended)
    
- Create Pull Request
    

---

# Purpose of a Pull Request

A PR exists so changes can be reviewed **before** they become part of the main branch.

Typical review process:

```text
Developer
      │
Push Branch
      │
Pull Request
      │
Review
      │
Comments / Changes Requested
      │
Approval
      │
Merge
```

Large teams often require:

- Multiple reviewers
    
- Passing CI/CD pipelines
    
- Successful automated tests
    
- Approval before merge
    

---

# Merging the Pull Request

After approval:

```
Merge Pull Request
        │
Confirm Merge
```

GitHub creates a **merge commit** (by default).

Result:

```text
Before

master
    │
feature-auth

After Merge

master
    │
    ├── Previous commits
    ├── Merge Commit
    └── feature-auth changes
```

The changes now exist in `master`.

---

# What Happens During Merge?

Suppose:

```text
master

index.html
```

Feature branch adds:

```text
auth.html
```

Before merge:

```text
master
└── index.html

feature-auth
├── index.html
└── auth.html
```

After merge:

```text
master
├── index.html
└── auth.html
```

`master` now contains every change from `feature-auth`.

---

# Performing the Merge from the Terminal

A Pull Request is a **GitHub feature**. The underlying merge is performed by Git. You can merge entirely from the terminal if collaboration or code review is unnecessary.

## Step 1 — Switch to the Target Branch

```bash
git switch master
```

or

```bash
git checkout master
```

---

## Step 2 — Update the Target Branch (Recommended)

```bash
git pull origin master
```

Ensures the local target branch is up to date before merging.

---

## Step 3 — Merge the Feature Branch

```bash
git merge feature-auth
```

Result:

```
feature-auth
        │
        ▼
master
```

If no conflicts exist, Git creates the merge automatically (or performs a fast-forward merge when possible).

---

## Step 4 — Push the Updated Branch

```bash
git push origin master
```

The merged changes are now available on GitHub.

---

# GitHub Merge vs Terminal Merge

|GitHub Pull Request|Terminal Merge|
|---|---|
|Includes code review|No built-in review|
|Team collaboration|Mainly individual workflows|
|Supports approvals|No approval process|
|Shows discussion history|Local merge only|
|Merge performed via GitHub UI|Merge performed with Git commands|

Both ultimately use **Git merge** to combine histories.

---

# Merge Commit

A merge usually creates a new commit representing the combination of two branch histories.

Contains:

- Parent branch history
    
- Feature branch history
    
- Merge metadata
    
- Commit SHA
    

This preserves the complete development history.

---

# Typical Team Workflow

```text
Create Feature Branch
        │
Code
        │
git add .
        │
git commit
        │
git push
        │
Open Pull Request
        │
Code Review
        │
Approve
        │
Merge
        │
Delete Feature Branch (optional)
```

---

# Common Beginner Mistakes

|Mistake|Correct Approach|
|---|---|
|Committing directly to `main/master`|Create a feature branch first|
|Creating a PR before pushing the branch|Push the branch to GitHub first|
|Assuming a PR automatically merges changes|A PR is only a **request** until merged|
|Forgetting to switch to the target branch before terminal merge|Always `git switch master` (or `main`) before `git merge`|
|Forgetting to push after a terminal merge|Run `git push origin <target-branch>`|
|Assuming merging deletes the feature branch|Delete it manually if no longer needed|

---

# Essential Commands

|Command|Purpose|
|---|---|
|`git switch -c feature-auth`|Create and switch to a feature branch|
|`git status`|Show repository status|
|`git add .`|Stage changes|
|`git commit -m "message"`|Create a local commit|
|`git push -u origin feature-auth`|First push and set upstream|
|`git push`|Push subsequent commits|
|`git switch master`|Switch to the target branch|
|`git pull origin master`|Update the target branch before merging|
|`git merge feature-auth`|Merge the feature branch into the current branch|
|`git push origin master`|Push the merged branch to GitHub|

---

# Mental Model

```text
Local Repository

master
   │
   ├────────────► feature-auth
   │                  │
   │              Development
   │                  │
   │            git add
   │                  │
   │            git commit
   │                  │
   │            git push
   │                  │
   └──────────────────┼──────────────────────┐
                      ▼                      │
                GitHub Pull Request          │
                      │                      │
               Review & Approval             │
                      │                      │
                  Merge (GitHub UI)          │
                      │                      │
                      ▼                      │
                    master ◄─────────────────┘

Equivalent terminal merge:

git switch master
git pull origin master
git merge feature-auth
git push origin master
```

> **Key distinction:** A **Pull Request** is a GitHub collaboration workflow. A **merge** is the underlying Git operation that combines branch histories. A PR provides review, discussion, and approval around that merge.













# Git Pull

## Definition

|Command|Purpose|
|---|---|
|`git pull`|Updates the **current local branch** by downloading and integrating the latest changes from its tracked remote branch.|
|Equivalent|`git fetch` + `git merge` (default behavior).|

---

## Problem Solved

Scenario:

```
Developer A
Feature Branch
      │
      ▼
Push → Pull Request → Merge → origin/main updated

Developer B
Local main (outdated)
      │
      ▼
git pull
      │
      ▼
Local main = origin/main
```

Without `git pull`, other collaborators' merged changes are **not available locally**.

---

## Local vs Remote

|Local Repository|Remote Repository (e.g., GitHub)|
|---|---|
|Stored on your computer|Hosted online|
|May become outdated|Usually contains latest shared code|
|Updated via `git pull`|Updated via `git push`|

---

## How `git pull` Works

```
Remote Branch
      │
      ▼
Download latest commits
      │
      ▼
Merge into current local branch
      │
      ▼
Working directory updated
```

Equivalent:

```bash
git fetch
git merge
```

---

## Syntax

```bash
git pull
```

Explicit form:

```bash
git pull origin main
```

---

## Typical Workflow

```text
Someone pushes code
        │
        ▼
PR merged into main
        │
        ▼
Your local main becomes outdated
        │
        ▼
git switch main
git pull
        │
        ▼
Local main synchronized
```

---

## Branch Requirement

Always pull **after switching to the branch you want to update**.

Modern:

```bash
git switch main
git pull
```

Legacy:

```bash
git checkout main
git pull
```

---

## Git Status Hint

When local branch is outdated:

```
Your branch is behind 'origin/main' by N commits.
(use "git pull" to update your local branch)
```

Meaning:

```
origin/main
      │
      ▼
New commits exist remotely

main (local)
      │
      ▼
Older commit
```

---

## Example

Initial state:

```
Remote (origin/main)
├── index.html
├── index.css
└── auth.html

Local (main)
├── index.html
└── index.css
```

Run:

```bash
git switch main
git pull
```

Result:

```
Local (main)
├── index.html
├── index.css
└── auth.html
```

---

## Common Collaboration Flow

```
Create feature branch
        │
        ▼
Develop
        │
        ▼
git push
        │
        ▼
Pull Request
        │
        ▼
Merge into main
        │
        ▼
Every collaborator:
git switch main
git pull
```

---

## Best Practices

|Practice|Reason|
|---|---|
|Pull before starting new work|Avoid working on outdated code.|
|Pull after teammates merge PRs|Keep local repository synchronized.|
|Pull the correct branch|`git pull` updates only the current branch.|
|Commit or stash local changes before pulling|Prevent merge conflicts or interrupted merges.|

---

## Related Commands

|Command|Purpose|
|---|---|
|`git push`|Upload local commits to remote.|
|`git fetch`|Download remote changes without merging.|
|`git pull`|Download **and** merge remote changes.|
|`git merge`|Combine histories manually.|

---

## Mental Model

```
git push
Local ─────────► Remote

git pull
Local ◄───────── Remote
```











# Git: Amend Latest Commit Message (`git commit --amend`)

## Purpose
Update the **most recent commit** (message and/or content) without creating a new commit.

---

## Syntax

```bash
# Change latest commit message
git commit --amend -m "New commit message"

# Edit message in editor
git commit --amend

# Legacy equivalent
git commit --amend
```

---

## Workflow

```text
Modify files
      │
      ▼
git add
      │
      ▼
git commit -m "Wrong message"
      │
      ▼
git commit --amend -m "Correct message"
      │
      ▼
Latest commit updated
```

---

## Effect

| Before | After |
|--------|-------|
| Latest commit has wrong message | Latest commit message replaced |
| No new commit intended | Previous commit rewritten |
| Commit history unchanged in length | Still one latest commit |

---

## Command Breakdown

| Part | Purpose |
|------|---------|
| `git commit` | Create/update a commit |
| `--amend` | Rewrite the latest commit |
| `-m` | Provide new commit message |

---

## What `--amend` Can Do

| Operation | Example |
|-----------|---------|
| Change commit message | `git commit --amend -m "Fix login validation"` |
| Add forgotten staged files to latest commit | `git add file` → `git commit --amend --no-edit` |
| Modify both files and message | `git add ...` → `git commit --amend` |

---

## Internal Behavior

```text
Old Commit
    │
    ├── Snapshot
    ├── Message
    └── Commit ID
         │
         ▼
git commit --amend
         │
         ▼
New Commit
    ├── Updated snapshot/message
    └── NEW Commit ID
```

> **Important:** `--amend` rewrites history. A **new commit object** is created, so the **commit hash (ID) changes**, even if only the message changes.

---

## Local vs Remote Rule

| Situation | Safe? |
|-----------|-------|
| Commit not pushed | ✅ Safe (recommended) |
| Already pushed | ⚠ Rewrites shared history |

If already pushed:

```bash
git push --force-with-lease
```

Prefer `--force-with-lease` over `--force` because it avoids overwriting others' work.

---

## Common Workflow

```bash
git switch feature/login          # or: git checkout feature/login

touch docs.md

git add docs.md

git commit -m "New doc file aded"   # typo

git log --oneline

git commit --amend -m "New doc file added"

git log --oneline
```

Result:

```text
Before
a12b3cd New doc file aded

After
e45f6gh New doc file added
```

History still contains **one latest commit**, but its **hash changes**.

---

## Rules

- Works **only on the latest commit**.
- Rewrites commit history.
- Produces a new commit hash.
- Does **not** create an extra commit.
- Staged changes are included in the amended commit.
- Use before pushing whenever possible.

---

## Common Mistakes

| Mistake | Correct |
|----------|---------|
| Using `--amend` to edit older commits | Use `git rebase -i` |
| Amending after pushing without care | Coordinate, then `git push --force-with-lease` |
| Expecting commit hash to remain same | Hash always changes after amend |
| Forgetting staged files are included | Review with `git status` before amending |

---

## Related Commands

| Purpose | Command |
|---------|---------|
| View latest commits | `git log --oneline` |
| Stage changes | `git add <file>` |
| Create commit | `git commit -m "message"` |
| Amend latest commit | `git commit --amend -m "message"` |
| Amend without changing message | `git commit --amend --no-edit` |
| Edit older commit messages | `git rebase -i HEAD~n` |

---

## Exam Revision

| Concept | Key Point |
|---------|-----------|
| `--amend` | Rewrite latest commit |
| New commit created? | ❌ No visible extra commit |
| Commit hash | ✅ Changes |
| Message editable | ✅ Yes |
| Files editable | ✅ Yes (staged files) |
| Safe before push | ✅ Yes |
| Safe after push | ⚠ Requires `git push --force-with-lease` |
| Older commits | Use interactive rebase (`git rebase -i`) |



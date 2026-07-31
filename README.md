# Git Training for Undergrads

## What is Version Control?

**Git** is a tool for tracking changes to your project over time. It lets you:
- **Save snapshots** of your work at important milestones
- **Collaborate** with others without overwriting each other's changes
- **Revert** to previous versions if something breaks
- **See the history** of who changed what and why

**GitHub/GitLab/Bitbucket** are cloud services that host your Git repositories and make collaboration easier.

---

## Getting Started

### Option 1: Create a new project
```bash
mkdir ProjectName
cd ProjectName
git init
```

### Option 2: Clone an existing project
```bash
git clone URL
cd ProjectName
```

### Configure Git (one-time setup)
Before making commits, tell Git who you are:
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

---

## The Basic Workflow

### 1. Check the Status
After making changes to files, check what Git sees:
```bash
git status
```

This shows:
- **Untracked files** – New files Git doesn't know about yet
- **Modified files** – Files you changed but haven't staged
- **Staged files** – Files ready to commit

### 2. Stage Your Changes
Add the files you want to include in your commit:

```bash
git add filename.txt          # Add a specific file
git add .                     # Add all changes in current directory
git add --all                 # Add all changes in entire project
git add *.py                  # Add all Python files
```

**Tip:** Stage often and in logical groups. Each commit should represent one meaningful change.

### 3. Restore Unstaged Changes
If you messed up and want to discard changes before staging:
```bash
git restore filename.txt      # Discard changes to one file
git restore .                 # Discard all changes in current directory
```

### 4. Commit Your Changes
Commit saves a snapshot of your staged changes with a message describing what you did:
```bash
git commit -m "Add login functionality to auth module"
```

**Good commit messages:**
- ✅ "Fix bug in user authentication"
- ✅ "Add error handling to file parser"
- ✅ "Refactor database connection logic"

**Bad commit messages:**
- ❌ "fix stuff"
- ❌ "asdf"
- ❌ "more changes"

**Why this matters:** Your teammates (and future you!) will read commit messages to understand why a change was made.

### 5. Undo a Commit
Already committed but regret it? You have options:

```bash
git reset HEAD~1              # Undo the commit but keep your changes staged
git restore HEAD~1            # Undo the commit and discard your changes
```

---

## Working with Branches

Branches let you work on features independently without affecting the main project.

**Scenario:** You want to add a new feature, but you're not sure if it will work. Create a branch to experiment safely.

### Create a Branch
```bash
git branch feature/dark-mode
```

### List All Branches
```bash
git branch
```

The branch with a `*` next to it is your current branch.

### Switch to a Branch
```bash
git switch feature/dark-mode
```

(Or use the older command: `git checkout feature/dark-mode`)

### Create and Switch in One Command
```bash
git switch -c feature/dark-mode
```

---

## Merging Branches

Once you've finished your feature on a branch, merge it back to `main`.

### Merge a branch into main

```bash
git switch main               # First, switch to the main branch
git pull origin main          # Get the latest changes from remote
git merge feature/dark-mode   # Merge your feature branch
git push origin main          # Push the merged changes back to remote
```

### Merging in the opposite direction
If you want to bring the latest changes from `main` into your feature branch:

```bash
git switch feature/dark-mode  # Switch to your feature branch
git merge main                # Merge main's changes into your branch
```

### Handling Merge Conflicts ⚠️
If you and a teammate both changed the same lines, Git will create a **merge conflict**. Here's what to do:

1. **See what changed:**
   ```bash
   git status
   ```
   You'll see files marked as "both modified"

2. **Open the conflicted file** and look for:
   ```
   <<<<<<< HEAD
   Your changes here
   =======
   Their changes here
   >>>>>>> feature/dark-mode
   ```

3. **Manually decide** which version to keep, then delete the conflict markers

4. **Mark as resolved:**
   ```bash
   git add resolved-file.txt
   git commit -m "Resolve merge conflict in auth module"
   ```

**Pro tip:** Communicate with your teammates when conflicts happen. A quick chat often clarifies the best solution.

---

## Ignoring Files

Some files shouldn't be tracked (node_modules, `.env`, cache files, etc.). Create a `.gitignore` file in your project root:

```bash
# .gitignore
node_modules/
__pycache__/
.env
.DS_Store
*.pyc
```

Any files matching these patterns will be ignored by Git.

---

## Viewing History

### See all commits
```bash
git log
```

Shows:
- Commit hash (unique ID)
- Author
- Date
- Commit message

### See changes in specific commit
```bash
git show abc123def          # Replace with actual commit hash
```

### Compare two commits
```bash
git diff abc123def xyz789abc
```

### Travel back in time (viewing only)
```bash
git checkout abc123def      # View this commit
git switch main             # Go back to main
```

---

## Remote Operations: Push, Pull, and Fetch

Your local repository is separate from the remote (GitHub/GitLab). You need to sync them.

### Push: Send your changes to remote
```bash
git push origin main        # Push commits from local main to remote main
git push origin feature/new-feature  # Push a branch to remote
```

**After pushing a branch, teammates can see it and review your changes.**

### Pull: Get and merge remote changes
```bash
git pull                    # Fetches and automatically merges remote changes
```

This is the most common command. Use it at the start of your work day.

### Fetch: Just see what changed (don't merge yet)
```bash
git fetch                   # See what's new on remote
```

Then review before merging:
```bash
git diff main origin/main   # See differences before merging
git merge origin/main       # Now merge if you like the changes
```

---

## Saving Work in Progress (Stash)

You're in the middle of something but need to switch branches. Don't commit unfinished work—use stash:

```bash
git stash                   # Save your changes temporarily
git switch another-branch   # Now you can safely switch
```

Later, get your work back:
```bash
git switch back-to-original-branch
git stash pop               # Restore your saved changes
```

---

## Common Beginner Mistakes 🚨

- **Forgetting `git add`** – You modified files but they won't be committed unless you add them
- **Committing secrets** – Never commit passwords, API keys, or `.env` files (use `.gitignore`)
- **Pulling before pushing** – Always `git pull` before you push to avoid conflicts
- **Bad commit messages** – Future you will hate present you for "fix stuff"
- **Merging without testing** – Test your branch locally before merging to main
- **Working directly on main** – Use feature branches; main should always be stable

---

## Quick Reference

```bash
# Setup
git init                          # Initialize a repo
git clone URL                     # Clone a repo

# Daily workflow
git status                        # Check what changed
git add .                         # Stage changes
git commit -m "message"           # Save changes locally
git pull                          # Get latest from remote
git push origin main              # Send to remote

# Branching
git switch -c feature/name        # Create and switch to branch
git switch main                   # Switch branches
git merge feature/name            # Merge feature into current branch

# Undoing
git restore filename              # Discard changes
git reset HEAD~1                  # Undo last commit
git stash                         # Save work temporarily
```

---

**Questions?** Ask during the training session!

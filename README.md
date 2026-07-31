# Git-training

**Git** is a tool for tracking changes to your project over time. It lets you:
- **Save snapshots** of your work at important milestones
- **Collaborate** with others without overwriting each other's changes
- **Revert** to previous versions if something breaks
- **See the history** of who changed what and why

**GitHub/GitLab/Bitbucket** are cloud services that host your Git repositories and make collaboration easier.

---

## Initializing our project

Create a directory to store your project using 
`mkdir ProjectName`
`cd ProjectName`
`git init`

or clone a project you want to collaborate on `git clone URL`

### Configure Git (one-time setup)
Before making commits, tell Git who you are:
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

## Setting the stage
Now you can make some changes. You check the status of those changes with
`git status` or anytime you want to know the status of your project.

Now to stage or save your changes locally you can add them to the project via: 
- `git add filename.txt` adds a specific file
- `git add --all` if there are new in files/dirs
- `git add .` for a particular directory your in
- `git add *` for new or modified files/dirs but no deleted ones

**Tip:** Stage often and in logical groups. Each commit should represent one meaningful change.

If you messed up and want to discard changes before staging:
```bash
git restore filename.txt      # Discard changes to one file
git restore .                 # Discard all changes in current directory
```

Finally to commit or implement your changes to the project: 
```bash
git commit -m "Add login functionality to auth module"
```

Already committed but regret it? You have options:

```bash
git reset HEAD~1              # Undo the commit but keep your changes staged
git restore HEAD~1            # Undo the commit and discard your changes
```

---

## Branches

Say you want to implement a new feature on the project but are unsure this may make or break the integrity of the project. You may need a testing area or a new branch of the project.

You can create a new branch with:

`git branch new_branch`

You can use `git branch` to see how many branches there are.

To go to a different branch check-it-out: `git checkout branch_name`

### Switch to a Branch
```bash
git switch new_branch2
```

## Merge

Now that you made changes to the new branch, you may want to implement them in the main project branch. To do this inside main
`git merge new_branch -m "Merges new_branch to main`

Sometimes there are changes in the main branch that can be useful in your new_branch, so to merge main's changes to another branch
`git merge main -m "Brings main's changes` (inside new_branch)

Warning sometimes there will be merging conflicts where two people made similar changes... a discussion between collaborators may be needed. 

### Merging Conflicts
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

## Logs

You can always check the different changes across your project with `git log`, you can check them out with `git checkout log_number` and compare different logs with
`git diff log_1 log_2`

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

## Saving Work in Progress (Stash)

You're in the middle of something but need to switch branches. Don't commit unfinished work‚Äîuse stash:

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

## Pushing, Fetching and Pulling

Pushing -> pushing changes to the remote repository

`git push origin main` all your commits will be pushed to the main but not the other branches

Fetching -> fetches changes from the remote repository without merging them

`git fetch` will show you how behind you are; you would need to merge if you want them in your local repo

Pulling -> pulls changes from the remote repository and merges them

`git pull` fetches and merges the remote changes to your local repo


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



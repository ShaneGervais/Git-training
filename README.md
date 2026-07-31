# Git-training

# Git
A tool for tracking changes of your projects locally or remotely for collaborative work through Github/Gitlab/Bit 

# Github
Remote cloud services using git as its core

# Initializing our project

Create a directory to store your project using `mkdir ProjectName` or clone a project you want to collaborate on `git clone URL`

# Setting the stage
Now you can make some changes. You check the status of those changes with
`git status` or anytime you want to know the status of your project.

Now to stage or save your changes locally you can add them to the project via: 
- `git add`
- `git add --all` if there are new in files/dirs
- `git add .` for a particular directory your in
- `git add *` for new or modified files/dirs but no deleted ones

to restore the changes simply `git restore` or to revert to a previous change `git reset`.

Finally to commit or implement your changes to the project: `git commit -m "Write about your changes"`

# Branches

Say you want to implement a new feature on the project but are unsure this may make or break the integrity of the project. You may need a testing area or a new branch of the project.

You can create a new branch with:

`git branch new_branch`

You can use `git branch` to see how many branches there are.

To go to a different branch check-it-out: `git checkout branch_name`

# Merge

Now that you made changes to the new branch, you may want to implement them in the main project branch. To do this inside new_branch
`git merge new_branch -m "Merges new_branch to main`

Sometimes there are changes in the main branch that can be useful in your new_branch, so to merge main's changes to another branch
`git merge main -m "Brings main's changes` (inside new_branch)

Warning sometimes there will be merging conflicts where two people made similar changes... a discussion between collaborators may be needed. 

# Logs

You can always check the different changes across your project with `git log`, you can check them out with `git checkout log_number` and compare different logs with
`git diff log_1 log_2`

# Pushing, Fetching and Pulling

Pushing -> pushing changes to the remote repository

`git push origin main` all your commits will be pushed to the main but not the other branches

Fetching -> fetches changes from the remote repository without merging them

`git fetch` will show you how behind you are; you would need to merge if you want them in your local repo

Pulling -> pulls changes from the remote repository and merges them

`git pull` fetches and merges the remote changes to your local repo

# I don't like the changes I've done

you can always `git restore` to revert to the previous commited step

# I have nothing to commit but I need to save my work before I checkout something else

`git stash` is your friend :) and when you comeback, pop it out of the stash `git stash pop`.





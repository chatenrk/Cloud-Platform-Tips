# Git Reference Guide

- [Git Reference Guide](#git-reference-guide)
  - [Quick Reference](#quick-reference)
  - [General Information](#general-information)
    - [Git Workflow](#git-workflow)
    - [Git Branching](#git-branching)

## Quick Reference

| Description                        | Command                                                                                                                                                                                                                                                                                                            |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Initialise a local git repository  | Create a new directory, open it and perform a <br> `git init` <br> to create a new git repository                                                                                                                                                                                                                  |
| Check status                       | `git status` <br><br> ![Git Status](./screenshots/git%20status.PNG) <br>                                                                                                                                                                                                                                           |
| Checkout a repository              | Create a working copy of a local repository by running the command <br> `git clone /path/to/repository` <br> when using a remote server, your command will be <br> `git clone username@host:/path/to/repository`                                                                                                   |
| Checkout a specific branch of repo | `git clone -b <branch> <remote_repo>`                                                                                                                                                                                                                                                                              |
| Add and Commit                     | You can propose changes (add it to the Index) using <br> `git add <filename>` <br> `git add *` <br> This is the first step in the basic git workflow. To actually commit these changes use <br> `git commit -m "Commit message"` <br> Now the file is committed to the HEAD, but not in your remote repository yet |
| Add remote github repository       | `git remote add origin <<insert github repository name here>>`                                                                                                                                                                                                                                                     |
| Push changes to remote repository  | `git push -u origin master`                                                                                                                                                                                                                                                                                        |
| List all git branches              | `git branch -- list`                                                                                                                                                                                                                                                                                               |
| Create new git branch              | `git branch <<insert branch name here>>`                                                                                                                                                                                                                                                                           |
| Checkout to another branch         | `git checkout <<insert branch name here`                                                                                                                                                                                                                                                                           |
| Merge changes to another branch    | `git merge <<insert branch name>>`                                                                                                                                                                                                                                                                                 |
| Delete a branch                    | `git branch -d <<insert branch name>>`                                                                                                                                                                                                                                                                             |
| Update                             | To update your local repository to the newest commit, execute <br> `git pull` <br> in your working directory to fetch and merge remote changes                                                                                                                                                                     |
| Replace local changes              | If you want to drop all your local changes and commits, fetch the latest history from the server and point your local master branch at it like this <br> `git fetch origin` <br> `git reset --hard origin/master`                                                                                                  |


## General Information

### Git Workflow

your local repository consists of three "trees" maintained by git. the first one is your **Working Directory** which holds the actual files. the second one is the **Index** which acts as a staging area and finally the **HEAD** which points to the last commit you've made.
![Git Workflow](./screenshots/git%20workflow.PNG)

### Git Branching
Branches are used to develop features isolated from each other. The master branch is the "default" branch when you create a repository. Use other branches for development and merge them back to the master branch upon completion.
![Git Branching](./screenshots/git%20branching.PNG)
# Git Reference Guide

**[Table of Contents]**

- [Quick Reference](#quick-reference)

## Quick Reference

| Description                       | Command                                                                                                                                                                                                          |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Initialise a local git repository | Create a new directory, open it and perform a <br> `git init` <br> to create a new git repository                                                                                                                |
| Checkout a repository             | Create a working copy of a local repository by running the command <br> `git clone /path/to/repository` <br> when using a remote server, your command will be <br> `git clone username@host:/path/to/repository` |
| Add and Commit                    | You can propose changes (add it to the Index) using <br> `git add <filename>` <br> `git add *`                                                                                                                   |

| Add all modified entries into the git repository | `git add .` |
| Commit changes | `git commit -m "Commit Message"` |
| Add remote github repository | `git remote add origin <<insert github repository name here>>` |
| Push changes to remote repository | `git push -u origin master` |
| List all git branches | `git branch -- list` |
| Create new git branch | `git branch <<insert branch name here>>` |
| Checkout to another branch | `git checkout <<insert branch name here` |
| Merge changes to another branch | `git merge <<insert branch name>>` |
| Check status | `git status` <br><br> ![Git Status](https://github.com/chatenrk/Cloud-Platform-Tips/blob/cleanUpGit/Git%20Related/screenshots/git%20status.PNG) <br> |

## General Information

### Git Workflow

your local repository consists of three "trees" maintained by git. the first one is your **Working Directory** which holds the actual files. the second one is the **Index** which acts as a staging area and finally the **HEAD** which points to the last commit you've made.
![Git Workflow](https://github.com/chatenrk/Cloud-Platform-Tips/blob/cleanUpGit/Git%20Related/screenshots/git%20workflow.PNG)

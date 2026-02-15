
<div id="top"></div>

# 🚀 Git & GitHub – 0 to Pro Reference

A practical cheat‑sheet for mastering Git and GitHub from basics to advanced workflows.

<details>
<summary>Table of contents</summary>

- [Command Line Basics](#️-command-line-basics)
- [Git Concepts](#-git-concepts)
- [Initialize Git](#-initialize-git)
- [Staging Changes](#-staging-changes)
- [Creating Commits](#-creating-commits)
- [Conventional Commits](#conventional-commits)
- [Specify the type of commit](#specify-the-type-of-commit)
- [Configure Git](#️-configure-git)
- [Reset & Checkout](#-reset--checkout)
- [Viewing Previous Commits](#-viewing-previous-commits)
- [Restore Files from Previous Commit](#️-restore-files-from-previous-commit)
- [Git Aliases](#-git-aliases)
- [.gitignore](#-gitignore)
- [Delete Git](#delete-git)
- [Connect to GitHub](#-connect-to-github)
- [Push Code](#️-push-code)
- [Clone / Pull](#️-clone--pull)
- [Branching](#-branching)
- [Merging](#-merging)
- [Merge Conflicts](#️-merge-conflicts)
- [Feature Branch Workflow](#-feature-branch-workflow)
- [Sync After Merge](#-sync-after-merge)
- [Delete Branch](#delete-branch)
- []
- [Pro Tip](#-pro-tip)
- [Reference](#reference)

</details>



<hr/>

## 🖥️ Command Line Basics

```bash
ls                       # List files and folders
cd ~/Desktop/folder     # Change directory
```

> ⚠️ Run git commands inside the project folder.

<hr/>

## 🧠 Git Concepts

- **Version** = Commit
- **Version History** = Commit history
- **Working Area → Staging Area → Commit History**

<hr/>

## 🆕 Initialize Git

```bash
git init  # Git will start tracking all changes in the current folder
git status  # Show all changes since the previous commit
```

<hr/>

- **Working Area** = contains changes start in the working area
- **Staging Area** = contains changes that will go into the next commit

<hr/>

## 📦 Staging Changes

```bash
git add file  # Pick individual file
git add folder/  # Pick all files inside a folder (and subfolders)
git add .  # Pick all files (in folder command line is running in)
```

<hr/>

## 💾 Creating Commits

```bash
git commit -m "message"  # Creates a commit with a message attached
git commit -m "message" --amend   # Update previous commit instead of creating new one
git log  # View the commit history
git log --all  # Show all commits (not just current branch)
git log --all --graph  # Show branching visually in the command line
git log --oneline
```

<p align="right">(<a href="#top">back to top</a>)
<hr/>

## Conventional Commits

- Structure:
```bash
<type>: <description>

[optional body]

[optional footer]
```

- Example:
```bash
git commit -m "feat: advanced login" `
-m "Added JWT token verification middleware" `
-m "Fixed bug in session timeout logic" `
-m "Closes #42"
```

### Specify the type of commit:

- **feat:** The new feature you're adding to a particular application
- **fix:** A bug fix
- **style:** Feature and updates related to styling
- **refactor:** Refactoring a specific section of the codebase
- **test:** Everything related to testing
- **docs:** Everything related to documentation
- **chore:** Regular code maintenance.[ You can also use emojis to represent commit types]

<p align="right">(<a href="#top">back to top</a>)
<hr/>

## ⚙️ Configure Git

```bash
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```

<hr/>

## 🔄 Reset & Checkout

### Staging → Working
```bash
git reset file
git reset folder/
git reset .

git reset --hard head~1  #to completely go back to previous commit | Deletes the latest commit from history.
git push -f   # to remove the future commit from present commit | Forces remote to forget that commit too
```

### Working → Remove Changes
```bash
git checkout <commit>  <file/folder>  #syntax
git checkout -- file
git checkout -- folder/
git checkout -- .
```
<p align="right">(<a href="#top">back to top</a>)
<hr/>

## 🕒 Viewing Previous Commits

```bash
git checkout <commit_hash>
git checkout <branch_name>
```

- `HEAD` → current commit
- `master/main` → latest commit on branch

<hr/>

## ♻️ Restore Files from Previous Commit

```bash
git checkout <hash> file
git checkout <hash> folder/
git checkout <hash> .
```

<hr/>

## 🧩 Git Aliases

```bash
git config --global alias.s "status"
git s
git config --global --unset alias.s # to remove an alias
```

<hr/>

## 🙈 .gitignore

Tell Git which files/folders NOT to track.
.gitignore

<hr/>

## Delete Git

```bash
rm -rf .git # to remove git completely from the project - it deletes the .git folder
```

Windows PowerShell:
```powershell
Remove-Item -Recurse -Force -LiteralPath ".\.git"
```
- Delete the .git from hidden folders in the project

<p align="right">(<a href="#top">back to top</a>)
<hr/>

## ☁️ GitHub Basics

- **Local Repo** = On your computer
- **Remote Repo** = On GitHub

<hr/>

## 🔗 Connect to GitHub

```bash
git remote add <remote_name> <url> # Link a local repository to a remote repository andgive a name for this link
git remote  # List all remote repositories that are linked
git remote -v # List all remote repositories (but with more detail)
git remote remove origin  # Removes the link to the remote repository named "origin"
git config --global credential.username <username>  # Configure your GitHub username so you can get access to your Github repository
```

<hr/>

## ⬆️ Push Code

```bash
git push origin main  # Upload a branch of your git version history to your remote repository
git push origin main --set-upstream # Next time you are on the main branch and you run git push, it will automatically push the main branch to origin
git push origin main -f # Force-push the branch to the remote repository (it will overwrite what's on the remote repository)
```

<hr/>

## ⬇️ Clone / Pull

```bash
git clone <url> <folder_name>
git fetch
git pull origin main
git pull origin main --set-upstream
```

<p align="right">(<a href="#top">back to top</a>)
<hr/>

## 🌿 Branching

```bash
git branch feature1
git checkout feature1
git branch -D feature1
```

- `HEAD -> feature1` → current branch

<hr/>

## 🔀 Merging

```bash
git checkout main
git merge feature1 -m "message"  
git merge --no-ff feature1 -m "message" # no fast forward commit, feature 1 is shown as separate and merged
```

<hr/>

## ⚠️ Merge Conflicts

When conflicts occur, Git marks the file like this:

```
<<<<<<< HEAD
code from current branch
=======
code from merging branch
>>>>>>> branch
```

### To resolve:
1. Remove conflict markers
2. Keep the final code you want
3. Commit the changes

```bash
git add .
git commit -m "resolved conflict"
```

<hr/>

## 🧪 Feature Branch Workflow

```bash
git branch new-feature
git checkout new-feature
git add .
git commit -m "new feature"
git push origin new-feature
```

Then create a Pull Request on GitHub and merge into `main`.


<p align="right">(<a href="#top">back to top</a>)
<hr/>

## 🔄 Sync After Merge

```bash
git checkout main
git pull origin main
```

<hr/>

## Delete branch

```bash
git branch -D branch-name
```

<hr/>

## Git Rebase

Rebasing is the process of moving or combining a sequence of commits to a new base commit. It is primarily used to maintain a clean, linear project history.

### Interactive Rebase
Use this to edit, squash, or reorder commits before they are shared.
```bash
git rebase -i HEAD~n
```

- Common Commands in Interactive Mode: 
    - **reword:** Use the commit, but edit the commit message.
    - **squash:** Meld the commit into the previous one.
    - **pick:** Use the commit as is.
    - **drop:** Remove the commit entirely.

<hr/>

## Git Reflog

Think of Reflog as your local "undo" history. While git log shows the history of the branch, git reflog records every time your HEAD pointer moves—including resets, checkouts, and rebases.

When to Use:
- You accidentally deleted a branch.
- You performed a git reset --hard and lost work.
- A rebase went wrong and you want to go back. 

How to Undo a Rebase
1. Find the state before the rebase:
```bash
git reflog
```
2. Locate the entry that says rebase (start) and look at the line directly below it (e.g., HEAD@{5}).

3. Reset back to that moment:
```bash
git reset --hard HEAD@{n}
```

<hr/>

## 🧠 Pro Tip

Use branches for features and fixes. Keep `main` clean and production-ready.

<hr/>

## Reference
> Reference PDF by: supersimple.dev
> Tutorial Source: https://www.youtube.com/watch?v=hrTQipWp6co  

<p align="right">(<a href="#top">back to top</a>)
<hr/>
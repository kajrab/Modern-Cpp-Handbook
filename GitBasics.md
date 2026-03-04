# Basics of Git
I'm going to start with the basics of git. The real reason I want to write this is that I frequently forget CLI commands for git, so this is just a simple handbook that I can rely on whenever I need it.

---

## 1. Signing What You Have Done
```bash
git config --global user.name "yourname"
git config --global user.email "you@email.com"
```
With this you are introducing yourself to git, so every change you make gets signed with this name and email. Your teammates can easily track who made which changes.

---

## 2. Dailies
Like every gacha daily, we have some git commands that we use daily and they are essential to control the project.
```bash
git status              # checking the situation 
git add .               # packing all files that have changed
git add FileName.txt    # packing a single file that has changed
git commit -m "message" # sealing the package with a label (label = message)
git push                # send to GitHub (GitLab, etc.)
git pull                # get the latest from GitHub (or GitLab)
```

---

## 3. Starting a Repo (Project)
Before working on a repo or project you have to create one, and for this you can use:
```bash
git init        # initiate a new repo
git clone [url] # copy someone else's repo
```

---

## 4. When You Mess Up
Let's imagine you have just made a mistake — these commands are your best friends whenever you break your code:
```bash
git log --oneline       # see history
git diff                # what changed
git restore file.txt    # undo unsaved changes
git reset HEAD~1        # undo last commit (keeps your files)
```

You can also revert a specific file to a previous commit without touching anything else:
```bash
git checkout HEAD~1 -- FileName
```

---

## 5. Teamwork and Branches
We do not work alone most of the time, so it is crucial to understand the importance of branches.
Before committing to main, you have to create your own branch, make changes inside it, and push it so someone else can review before it gets merged.
```bash
git checkout -b my-work     # create a branch
git add . 
git commit -m "changes..."
git push -u origin my-work  # first push on a new branch
git push                    # every push after that
```
If you want to switch branches, use these:
```bash
git checkout main           # go back to main
git checkout branch-name    # go to any specific branch
git pull                    # always pull before doing something new
```
> Always pull before doing something new, otherwise you might work on outdated code without realizing it.

---

## 6. Connecting a Local Repo to GitHub
Sometimes you start a project locally and then decide it is time to store it on GitHub. Here is how you connect them:
```bash
git remote add origin https://github.com/username/repo-name.git
git branch -M main
git push -u origin main
```
First create an empty repo on GitHub, then connect it via the remote command and push everything up.

If the remote is ahead of your local repo:
```bash
git pull origin main --allow-unrelated-histories
```

---

## 7. Removing a File from Tracking
To remove a file from git tracking without deleting it locally:
```bash
git rm --cached FileName
```

---

## 8. Unstage a File Before Committing
If you staged something you did not mean to, use this:
```bash
git restore --staged FileName
```
---

## 9. Ignoring Files
Some files should never be tracked by git — build outputs, system files, secrets. Create a `.gitignore` file in your repo root and list them:

Git will never touch those files.

---

## Special Note: Authentication
GitHub no longer accepts passwords. You need a **Personal Access Token** instead.

Generate one from:
`Settings → Developer Settings → Personal Access Tokens → Tokens (classic)`

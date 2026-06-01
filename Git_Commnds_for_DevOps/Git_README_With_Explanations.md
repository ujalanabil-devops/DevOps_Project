# Git & GitHub Command Guide (with Explanations)

## Clone Repository

### git clone
```bash
git clone <repo_url>
```
**Purpose:** Downloads a remote repository to your local machine.

---

## Branch Commands

### git branch
```bash
git branch
```
**Purpose:** Shows local branches.

### git branch -r
```bash
git branch -r
```
**Flag:** `-r` = remote branches only.

### git branch -a
```bash
git branch -a
```
**Flag:** `-a` = all branches (local + remote).

### git checkout -b feature-1
```bash
git checkout -b feature-1
```
**Flag:** `-b` = create a new branch and switch to it immediately.

---

## Staging and Commit

### git add .
```bash
git add .
```
**Purpose:** Adds all new and modified files in the current directory to the staging area.

### git add <file>
```bash
git add README.md
```
**Purpose:** Stages only the specified file.

### git commit -m
```bash
git commit -m "Add README"
```
**Flag:** `-m` = commit message.

---

## Push Commands

### git push origin main
```bash
git push origin main
```
**Purpose:** Push local commits to the remote branch.

### git push -u origin feature-1
```bash
git push -u origin feature-1
```
**Flag:** `-u` = sets upstream tracking branch.

---

## Pull Commands

### git pull
```bash
git pull origin main
```
**Purpose:** Fetches and merges changes from remote.

### git pull --rebase
```bash
git pull --rebase origin main
```
**Flag:** `--rebase` = replays local commits on top of remote changes.

---

## Merge

### git merge
```bash
git merge feature-1
```
**Purpose:** Combines another branch into the current branch.

---

## Log Commands

### git log
```bash
git log
```
**Purpose:** Detailed commit history.

### git log --oneline
```bash
git log --oneline
```
**Flag:** `--oneline` = short commit history.

### git log --oneline -3
```bash
git log --oneline -3
```
**Flag:** `-3` = show last 3 commits.

---

## Reset Commands

### git reset --soft HEAD~1
```bash
git reset --soft HEAD~1
```
**Flag:** `--soft` = move HEAD, keep staged changes.

### git reset --mixed HEAD~1
```bash
git reset --mixed HEAD~1
```
**Flag:** `--mixed` = move HEAD, unstage changes, keep files.

### git reset --hard HEAD~1
```bash
git reset --hard HEAD~1
```
**Flag:** `--hard` = move HEAD, delete staged and working changes.

### HEAD~1
Means:
```text
HEAD   = current commit
HEAD~1 = one commit before HEAD
HEAD~2 = two commits before HEAD
```

---

## Delete Branches

### git branch -d
```bash
git branch -d feature-1
```
**Flag:** `-d` = delete merged branch.

### git branch -D
```bash
git branch -D feature-1
```
**Flag:** `-D` = force delete branch.

### git push origin --delete
```bash
git push origin --delete feature-1
```
**Flag:** `--delete` = remove remote branch.

---

## Useful Status Messages

### Ahead by commits
```text
Your branch is ahead of 'origin/test' by 2 commits.
```
Meaning: Local branch has commits not pushed to remote.

Fix:
```bash
git push origin test
```

### Branches have diverged
```text
Your branch and 'origin/test' have diverged.
```
Meaning:
- Local has commits remote doesn't have.
- Remote has commits local doesn't have.

Fix:
```bash
git pull --rebase origin test
git push origin test
```

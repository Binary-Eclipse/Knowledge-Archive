# Git Practice — 23/07/2026

## Overview

Today I practiced several important Git and Git Bash concepts:

- Navigating directories in Git Bash
- Initializing a Git repository
- Creating files
- `.gitignore`
- Staging and committing files
- Git stash workflow
- Git tags
- Viewing commit history
- Creating and switching branches
- Rebasing a feature branch
- Merging a branch using fast-forward merge
- Understanding common Git command errors

---

# 1. Navigating Windows Directories in Git Bash

## Incorrect

```bash
cd C:\Users\shakil\OneDrive\Desktop\Git Practice
```

### Error

```text
bash: cd: too many arguments
```

### Why?

Git Bash does not handle Windows paths with spaces in this format.

## Correct

```bash
cd "C:/Users/shakil/OneDrive/Desktop/Git Practice"
```

### Alternative

```bash
cd /c/Users/shakil/OneDrive/Desktop/Git\ Practice
```

### Important

When a path contains spaces, use:

- Quotes: `"path with spaces"`
- Or escape the spaces: `path\ with\ spaces`

---

# 2. Initialize a Git Repository

```bash
git init
```

Output:

```text
Initialized empty Git repository
```

This creates a hidden `.git` directory.

The `.git` directory contains the internal database of the repository, including:

- Commit history
- Branch information
- Tags
- Staging area information
- Git configuration

---

# 3. Create Multiple Files

```bash
touch file1.txt file2.text file3.html .env .gitignore
```

## Important Observation

The command attempted to create:

```text
file2.text
```

But the actual file appeared as:

```text
file2.txt
```

Later:

```bash
git rm file2.text
```

gave:

```text
fatal: pathspec 'file2.text' did not match any files
```

## Lesson

Git commands require the exact filename.

```bash
git rm file2.text   # Wrong if the file is file2.txt
git rm file2.txt   # Correct
```

Always verify filenames using:

```bash
ls
```

or:

```bash
git status
```

---

# 4. `.gitignore`

The `.env` file was ignored using:

```bash
echo ".env" > .gitignore
```

Then:

```bash
git status
```

showed:

```text
.gitignore
file1.txt
file2.txt
file3.html
```

The `.env` file was not shown as an untracked file.

## Important

`.gitignore` tells Git which files should not be tracked.

Common examples:

```gitignore
.env
node_modules/
__pycache__/
*.log
```

## Important Limitation

`.gitignore` only prevents untracked files from being added.

If a file has already been committed, adding it to `.gitignore` does not automatically remove it from Git tracking.

---

# 5. Staging and Committing

## Check status

```bash
git status
```

## Stage all changes

```bash
git add .
```

## Commit

```bash
git commit -m "added all files"
```

The first commit is called the:

```text
Initial commit
```

Example repository history:

```text
8cad0fb added all files
```

---

# 6. Git Stash

Initially:

```bash
git stash
```

returned:

```text
You do not have the initial commit yet
```

## Lesson

Before the first commit, Git stash cannot be used normally.

You should create at least one commit first.

---

## Normal Stash Workflow

After modifying:

```text
file1.txt
file2.txt
file3.html
```

the status showed:

```text
modified: file1.txt
modified: file2.txt
modified: file3.html
```

Then:

```bash
git stash
```

temporarily saved the changes.

After stashing:

```bash
git status
```

showed only the changes that were not included in that stash.

---

## View Stashes

```bash
git stash list
```

Example:

```text
stash@{0}: WIP on master: 8cad0fb added all files
```

---

## Apply and Remove the Latest Stash

```bash
git stash pop
```

This:

1. Applies the stashed changes
2. Removes the stash from the stash list

After:

```bash
git stash pop
```

```bash
git stash list
```

returned nothing because the stash was dropped.

---

## Important Difference

### `git stash pop`

Apply changes and delete the stash:

```bash
git stash pop
```

### `git stash apply`

Apply changes but keep the stash:

```bash
git stash apply
```

### `git stash drop`

Delete a stash:

```bash
git stash drop
```

---

# 7. Common Command Mistakes

## Mistake 1

```bash
git list
```

Git has no `list` command.

For stash list:

```bash
git stash list
```

---

## Mistake 2

```bash
git git commit -m "message"
```

This has `git` twice.

Correct:

```bash
git commit -m "message"
```

---

## Mistake 3

```bash
git log -oneline
```

Incorrect.

Correct:

```bash
git log --oneline
```

`--oneline` is a long option with two hyphens.

---

## Mistake 4

```bash
git log --oneline 5
```

This treats `5` as a commit or revision.

Correct:

```bash
git log --oneline -5
```

or:

```bash
git log --oneline -3
```

This displays the latest 3 commits.

---

# 8. Git Tags

Tags are used to mark important points in Git history, usually releases.

## Create an annotated tag

```bash
git tag -a v1.0 -m "release version 1.0"
```

This created:

```text
v1.0
```

on the current commit.

---

## Create a lightweight tag

```bash
git tag v1.1
```

---

## View tags

```bash
git tag
```

Output:

```text
v1.0
v1.1
```

---

## View tags in commit history

```bash
git log --oneline
```

Example:

```text
9627336 (HEAD -> master, tag: v1.1) Release 2
af4c1df (tag: v1.0) Release1
```

This means:

```text
v1.0 → Release 1
v1.1 → Release 2
```

---

# 9. Branch Creation

A new feature branch was created:

```bash
git switch -c features/login
```

This command:

1. Creates a new branch
2. Immediately switches to it

The branch structure became:

```text
master
   \
    features/login
```

---

## Check the Current Branch

```bash
git status
```

Example:

```text
On branch features/login
```

---

## Switch Branches

```bash
git switch master
```

```bash
git switch features/login
```

---

# 10. Working on a Feature Branch

On:

```text
features/login
```

`file1.txt` was modified:

```bash
echo "I have already seen this one" > file1.txt
```

Then:

```bash
git add .
git commit -m "Login features added"
```

Created:

```text
faa9f53 Login features added
```

At this point:

```text
master → Release 2
features/login → Login features added
```

The feature branch had one additional commit.

---

# 11. Rebase

After adding a new commit to `master`:

```text
master → added this.md
```

the feature branch was rebased:

```bash
git switch features/login
git rebase master
```

Result:

```text
Successfully rebased and updated refs/heads/features/login.
```

## Before Rebase

Conceptually:

```text
master:         A---B---C
                     \
features/login:      D
```

Where:

```text
C = added this.md
D = Login features added
```

## After Rebase

```text
master:         A---B---C
                         \
features/login:          D'
```

The feature commit was recreated on top of the latest `master`.

Important:

```text
D ≠ D'
```

The commit hash changed.

Before:

```text
faa9f53
```

After:

```text
05d6cf1
```

This is a key characteristic of rebase.

---

# 12. Fast-Forward Merge

After rebasing:

```bash
git switch master
git merge features/login
```

Git showed:

```text
Fast-forward
```

The result:

```text
master ────────────────┐
                       ▼
A---B---C---D'
```

Both branches now pointed to:

```text
05d6cf1 Login features added
```

Final result:

```text
05d6cf1 (HEAD -> master, features/login) Login features added
```

## Why was it Fast-Forward?

Because `master` had no new commits after the rebase point.

Git only had to move the `master` pointer forward.

No merge commit was required.

---

# 13. Complete Commit History

The final history became:

```text
05d6cf1 (HEAD -> master, features/login) Login features added
9ff98a8 added this.md
9627336 (tag: v1.1) Release 2
af4c1df (tag: v1.0) Release1
abed9ef stashed changes uploaded
0af1405 updated file3.html file
8cad0fb added all files
```

## Timeline

```text
8cad0fb
   ↓
0af1405
   ↓
abed9ef
   ↓
af4c1df  ← v1.0
   ↓
9627336  ← v1.1
   ↓
9ff98a8
   ↓
05d6cf1  ← features/login merged into master
```

---

# 14. Key Git Concepts Learned Today

| Concept | Command |
|---|---|
| Initialize repository | `git init` |
| Check repository status | `git status` |
| Stage all files | `git add .` |
| Commit changes | `git commit -m "message"` |
| Temporarily save changes | `git stash` |
| List stashes | `git stash list` |
| Apply and remove stash | `git stash pop` |
| View commit history | `git log` |
| Compact commit history | `git log --oneline` |
| Show latest commits | `git log --oneline -3` |
| Create annotated tag | `git tag -a v1.0 -m "message"` |
| Create lightweight tag | `git tag v1.1` |
| List tags | `git tag` |
| Create and switch branch | `git switch -c branch-name` |
| Switch branch | `git switch branch-name` |
| Rebase branch | `git rebase master` |
| Merge branch | `git merge branch-name` |

---

# 15. Most Important Lessons

## 1. Commit Before Stashing

```text
No initial commit → git stash does not work normally
```

Recommended:

```bash
git init
git add .
git commit -m "Initial commit"
git stash
```

---

## 2. Always Check the Exact Filename

```bash
ls
git status
```

Git is case-sensitive and filename-sensitive.

---

## 3. `git log --oneline` Uses Two Hyphens

Correct:

```bash
git log --oneline
```

For a limited number of commits:

```bash
git log --oneline -5
```

---

## 4. Rebase Changes Commit Hashes

When a commit is rebased:

```text
Old commit → New commit
```

Example:

```text
faa9f53 → 05d6cf1
```

The content may be similar, but the commit identity changes.

---

## 5. Rebase Can Create a Clean Linear History

Instead of:

```text
A---B---C
     \
      D
```

Rebase creates:

```text
A---B---C---D'
```

This is why teams often use rebase to keep project history clean.

---

## 6. Fast-Forward Merge Is the Simplest Merge

If the target branch has no new commits, Git can simply move its pointer forward:

```text
master → A---B---C
                  \
feature →          D
```

After merging:

```text
master/feature → A---B---C---D
```

No merge commit is needed.

---

# Final Practice Summary

Today's practice successfully covered a complete Git workflow:

```text
Create repository
      ↓
Create files
      ↓
Configure .gitignore
      ↓
Stage files
      ↓
Create initial commit
      ↓
Modify files
      ↓
Use git stash
      ↓
Restore stashed changes
      ↓
Create release tags
      ↓
Create feature branch
      ↓
Commit feature work
      ↓
Add new commit to master
      ↓
Rebase feature branch
      ↓
Merge feature branch
      ↓
Fast-forward master
```

## Main Workflow to Remember

```bash
git status

git add .

git commit -m "message"

git switch -c feature/branch-name

git add .
git commit -m "feature added"

git switch master

git rebase master

git merge feature/branch-name

git log --oneline
```

> **Today's most important practical lesson:** Git is mainly about understanding the relationship between the working directory, staging area, commits, branches, tags, stash, rebase, and merge.

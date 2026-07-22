# 🔀 Git Merge Conflicts — Complete Practical Guide

> A merge conflict occurs when Git cannot automatically combine changes from two branches.

---

# 📚 Table of Contents

* [What Is a Merge Conflict?](#what-is-a-merge-conflict)
* [General Conflict Resolution Workflow](#general-conflict-resolution-workflow)
* [1. Content Conflict](#1-content-conflict)
* [2. Add/Add Conflict](#2-addadd-conflict)
* [3. Modify/Delete Conflict](#3-modifydelete-conflict)
* [4. Rename/Delete Conflict](#4-renamedelete-conflict)
* [5. Rename/Rename Conflict](#5-renamerename-conflict)
* [6. Rename/Modify Conflict](#6-renamemodify-conflict)
* [7. Directory/File Conflict](#7-directoryfile-conflict)
* [8. Submodule Conflict](#8-submodule-conflict)
* [Conflict Resolution Commands](#conflict-resolution-commands)
* [Merge Strategy Options](#merge-strategy-options)
* [Best Practices](#best-practices)

---

# 🧠 What Is a Merge Conflict?

A merge conflict occurs when two branches make changes that Git cannot safely combine automatically.

Example:

```text
                main
                 │
          ┌──────┴──────┐
          │             │
       Change A       Change B
          │             │
          └──────┬──────┘
                 │
               MERGE
                 │
                 ▼
          ⚠️ CONFLICT
```

Git stops the merge and asks you to make a decision.

---

# 🔄 General Conflict Resolution Workflow

```bash
# 1. Start the merge
git merge branch-name

# 2. Check conflicts
git status

# 3. Review the affected files

# 4. Resolve the conflict

# 5. Stage the resolution
git add <file>

# 6. Complete the merge
git commit -m "Resolve merge conflict"
```

The general process is:

```text
Merge
  ↓
Conflict
  ↓
Review
  ↓
Decide
  ↓
Resolve
  ↓
git add / git rm
  ↓
git commit
```

---

# 1. 📝 Content Conflict

## Scenario

Both branches modify the same part of the same file.

### Starting Point

```text
message.txt
```

Original content:

```text
Hello World
```

### `main` Branch

```text
Hello from Main
```

### `feature` Branch

```text
Hello from Feature
```

Both branches changed the same line.

---

## Merge

```bash
git switch main
git merge feature
```

Git may insert conflict markers:

```text
<<<<<<< HEAD
Hello from Main
=======
Hello from Feature
>>>>>>> feature
```

---

## Resolve the Conflict

Manually edit the file:

```text
Hello from Main and Feature
```

Remove:

```text
<<<<<<< HEAD
=======
>>>>>>> feature
```

Then:

```bash
git add message.txt
git commit -m "Resolve content conflict"
```

---

## Resolution Flow

```text
Main:
Hello from Main

Feature:
Hello from Feature

        ↓

Choose:
Hello from Main and Feature

        ↓

git add message.txt
git commit
```

---

# 2. ➕ Add/Add Conflict

## Scenario

Both branches create a new file with the same name.

### `main`

```text
config.txt
```

Content:

```text
Main configuration
```

### `feature`

```text
config.txt
```

Content:

```text
Feature configuration
```

Neither file existed before the branches diverged.

---

## Merge

```bash
git switch main
git merge feature
```

Git reports:

```text
CONFLICT (add/add): Merge conflict in config.txt
```

---

## Resolve

Review the file:

```bash
cat config.txt
```

Choose one version or combine them.

Example final content:

```text
Main configuration
Feature configuration
```

Then:

```bash
git add config.txt
git commit -m "Resolve add/add conflict"
```

---

## Resolution Options

### Keep Current Branch Version

```bash
git checkout --ours config.txt
git add config.txt
```

### Keep Incoming Branch Version

```bash
git checkout --theirs config.txt
git add config.txt
```

Then:

```bash
git commit
```

> Modern alternative:

```bash
git restore --ours config.txt
git restore --theirs config.txt
```

---

# 3. ✏️ Modify/Delete Conflict

## Scenario

One branch modifies a file while another branch deletes it.

### Original

```text
data.txt
```

### `main`

```text
data.txt
```

Modified content:

```text
Updated data
```

### `feature`

```text
data.txt
```

Deleted.

---

## Merge

```bash
git switch main
git merge feature
```

Git reports:

```text
CONFLICT (modify/delete):
data.txt deleted in feature and modified in HEAD.
```

Git asks:

> Keep the modified file or delete it?

---

## Option A: Keep the Modified File

```bash
git add data.txt
git commit -m "Resolve modify/delete conflict by keeping file"
```

Final:

```text
data.txt
```

---

## Option B: Accept the Deletion

```bash
git rm data.txt
git commit -m "Resolve modify/delete conflict by deleting file"
```

Final:

```text
No data.txt
```

---

# 4. 🔄 Rename/Delete Conflict

## Scenario

One branch renames a file while another branch deletes the original file.

### Original

```text
myfile.txt
```

### `main`

```text
myfile.txt
      ↓
myfile-new.txt
```

### `feature`

```text
myfile.txt
      ↓
deleted
```

---

## Merge

```bash
git switch main
git merge feature
```

Git reports:

```text
CONFLICT (rename/delete):
myfile.txt renamed to myfile-new.txt in HEAD,
but deleted in feature.
```

---

## Option A: Keep the Renamed File

```bash
git add myfile-new.txt
git commit -m "Resolve rename/delete conflict by keeping renamed file"
```

`git add` means:

> I reviewed the conflict and choose to keep this file.

It does **not** mean that you are creating the file again.

---

## Option B: Delete the Renamed File

```bash
git rm myfile-new.txt
git commit -m "Resolve rename/delete conflict by deleting file"
```

---

# 5. 🔀 Rename/Rename Conflict

## Scenario

Both branches rename the same original file differently.

### Original

```text
report.txt
```

### `main`

```text
report.txt
      ↓
final-report.txt
```

### `feature`

```text
report.txt
      ↓
project-report.txt
```

---

## Merge

```bash
git merge feature
```

Git reports:

```text
CONFLICT (rename/rename):
Rename "report.txt"->"final-report.txt"
in branch "HEAD" rename "report.txt"->"project-report.txt"
in "feature"
```

---

## Resolve

Choose one name:

```bash
git mv final-report.txt report.txt
```

or:

```bash
git mv project-report.txt report.txt
```

Or choose a new name:

```bash
git mv final-report.txt official-report.txt
```

Then:

```bash
git add -A
git commit -m "Resolve rename/rename conflict"
```

---

## Final Decision

```text
main:
report.txt → final-report.txt

feature:
report.txt → project-report.txt

             ↓

      Choose one final name

             ↓

       official-report.txt
```

---

# 6. 🛠️ Rename/Modify Conflict

## Scenario

One branch renames a file while another branch modifies the original file.

### Original

```text
app.txt
```

### `main`

```text
app.txt
    ↓
application.txt
```

### `feature`

```text
app.txt
```

Modified:

```text
Updated application content
```

---

## Merge

Git must determine:

> Should the modification be applied to the renamed file?

---

## Resolve

Review the content:

```bash
cat application.txt
```

If the modified content should remain:

```bash
git add application.txt
git commit -m "Resolve rename/modify conflict"
```

If necessary, manually edit:

```text
application.txt
```

Then:

```bash
git add application.txt
git commit
```

---

# 7. 📁 Directory/File Conflict

## Scenario

One branch creates a file while another branch creates a directory with the same name.

### `main`

```text
project
```

A file:

```text
project
```

### `feature`

```text
project/
└── README.md
```

A directory.

Git cannot have both:

```text
project        ← file
project/       ← directory
```

at the same path.

---

## Merge

```bash
git merge feature
```

---

## Resolve Option A: Keep the File

Remove the directory:

```bash
rm -rf project
```

Then restore or keep the file and stage:

```bash
git add project
git commit -m "Resolve file/directory conflict by keeping file"
```

---

## Resolve Option B: Keep the Directory

Remove the file and keep the directory:

```bash
git add project/
git commit -m "Resolve file/directory conflict by keeping directory"
```

> Be careful with `rm -rf`. It permanently removes files from the working directory.

---

# 8. 📦 Submodule Conflict

## Scenario

Two branches point to different commits of the same Git submodule.

### `main`

```text
library → Commit A
```

### `feature`

```text
library → Commit B
```

---

## Merge

Git detects different submodule commits.

You must decide which submodule commit should be used.

---

## Resolve

Enter the submodule:

```bash
cd library
```

Checkout the desired commit:

```bash
git checkout <commit-hash>
```

Return to the parent repository:

```bash
cd ..
```

Stage the submodule:

```bash
git add library
```

Complete the merge:

```bash
git commit -m "Resolve submodule conflict"
```

---

# 🧩 Conflict Markers

For normal content conflicts, Git may insert:

```text
<<<<<<< HEAD
Current branch changes
=======
Incoming branch changes
>>>>>>> feature
```

## Meaning

| Marker            | Meaning                         |
| ----------------- | ------------------------------- |
| `<<<<<<< HEAD`    | Start of current branch changes |
| `=======`         | Separator                       |
| `>>>>>>> feature` | End of incoming branch changes  |

---

## Example

```text
<<<<<<< HEAD
Version from main
=======
Version from feature
>>>>>>> feature
```

Resolve it manually:

```text
Final combined version
```

Then:

```bash
git add file.txt
git commit
```

---

# 🧭 `ours` and `theirs`

During a merge:

```text
OURS
```

means:

> The branch you are currently on.

```text
THEIRS
```

means:

> The branch you are merging into the current branch.

Example:

```bash
git checkout --ours file.txt
```

Keep the current branch version.

```bash
git checkout --theirs file.txt
```

Keep the incoming branch version.

Modern syntax:

```bash
git restore --ours file.txt
git restore --theirs file.txt
```

Then:

```bash
git add file.txt
git commit
```

---

# 📊 Conflict Type Summary

| Conflict Type  | Branch A      | Branch B           | Main Decision                      |
| -------------- | ------------- | ------------------ | ---------------------------------- |
| Content        | Modifies file | Modifies same file | Choose/combine content             |
| Add/Add        | Adds file     | Adds same file     | Choose/combine versions            |
| Modify/Delete  | Modifies file | Deletes file       | Keep or delete                     |
| Rename/Delete  | Renames file  | Deletes original   | Keep renamed or delete             |
| Rename/Rename  | Renames A     | Renames B          | Choose final name                  |
| Rename/Modify  | Renames file  | Modifies original  | Apply modification to renamed file |
| Directory/File | Creates file  | Creates directory  | Keep file or directory             |
| Submodule      | Commit A      | Commit B           | Choose submodule commit            |

---

# 🛠️ Essential Conflict Commands

## Check Status

```bash
git status
```

---

## View Differences

```bash
git diff
```

---

## View Unmerged Files

```bash
git diff --name-only --diff-filter=U
```

---

## Keep Current Branch Version

```bash
git restore --ours <file>
git add <file>
```

---

## Keep Incoming Branch Version

```bash
git restore --theirs <file>
git add <file>
```

---

## Mark a Resolved File

```bash
git add <file>
```

---

## Mark a File as Deleted

```bash
git rm <file>
```

---

## Complete Merge

```bash
git commit
```

or:

```bash
git commit -m "Resolve merge conflicts"
```

---

## Abort Merge

```bash
git merge --abort
```

---

# 🔁 Complete Conflict Resolution Workflow

```bash
# Start merge
git merge feature

# Check conflicts
git status

# Review files
git diff

# Resolve manually or choose a version

# Stage resolved files
git add <file>

# Or confirm deletion
git rm <file>

# Complete merge
git commit -m "Resolve merge conflicts"

# Verify
git status
```

---

# 🧠 The Most Important Concept

When Git reports a merge conflict:

```text
❌ Do not panic
```

Follow:

```text
1. Read the conflict message
        ↓
2. Run git status
        ↓
3. Identify the conflict type
        ↓
4. Review both branch changes
        ↓
5. Decide the desired final state
        ↓
6. Edit, git add, or git rm
        ↓
7. Commit the merge
```

---

# 🚫 Canceling a Conflict Resolution

If you do not want to continue:

```bash
git merge --abort
```

This returns the repository to the state before the merge.

---

# 🎯 Practical Mental Model

```text
                 TWO BRANCHES
                      │
          ┌───────────┴───────────┐
          │                       │
      Change A                 Change B
          │                       │
          └───────────┬───────────┘
                      │
                    MERGE
                      │
          ┌───────────┴───────────┐
          │                       │
       No Conflict             Conflict
          │                       │
        Done              Review Changes
                                  │
                              Decide
                                  │
                         ┌────────┴────────┐
                         │                 │
                       Keep              Delete
                         │                 │
                      git add           git rm
                         │                 │
                         └────────┬────────┘
                                  │
                              git commit
                                  │
                            Merge Complete
```

---

# 🏆 Best Practices

### 1. Pull Before Starting Work

```bash
git pull
```

---

### 2. Make Small Commits

Good:

```text
Add login form
Fix validation
Update README
```

Avoid:

```text
Update everything
```

---

### 3. Communicate with Your Team

Before modifying the same important files, coordinate with other developers.

---

### 4. Resolve Conflicts Carefully

Never blindly choose:

```bash
git checkout --ours .
```

or:

```bash
git checkout --theirs .
```

without reviewing the changes.

---

### 5. Test After Resolving

After a conflict:

```bash
git status
```

Then test your application before pushing.

---

# 📌 Final Formula

```text
MERGE CONFLICT
      ↓
REVIEW
      ↓
DECIDE
      ↓
RESOLVE
      ↓
git add / git rm
      ↓
git commit
      ↓
MERGE COMPLETE
```

> **A merge conflict is Git asking a human to make a decision that Git cannot safely make automatically.**

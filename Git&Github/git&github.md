# 🚀 Git Commands Cheat Sheet

> A clean and concise Git reference for beginners and professionals.

---

## ⚙️ Git Configuration

<table>
<tr>
<th width="35%">Command</th>
<th>Description</th>
</tr>

<tr>
<td><code>git --version</code></td>
<td>Display the installed Git version.</td>
</tr>

<tr>
<td><code>git config --global user.name "Your Name"</code></td>
<td>Set your Git username.</td>
</tr>

<tr>
<td><code>git config --global user.email "you@example.com"</code></td>
<td>Set your Git email.</td>
</tr>

<tr>
<td><code>git config --list</code></td>
<td>View all Git configuration settings.</td>
</tr>

</table>

---

## 📁 Repository

<table>

<tr>
<th width="35%">Command</th>
<th>Description</th>
</tr>

<tr>
<td><code>git init</code></td>
<td>Create a new Git repository.</td>
</tr>

<tr>
<td><code>git clone &lt;repository-url&gt;</code></td>
<td>Clone an existing repository.</td>
</tr>

</table>

---

## 📌 Repository Status

<table>

<tr>
<th width="35%">Command</th>
<th>Description</th>
</tr>

<tr>
<td><code>git status</code></td>
<td>Show repository status.</td>
</tr>

<tr>
<td><code>git diff</code></td>
<td>Display unstaged changes.</td>
</tr>

<tr>
<td><code>git diff --staged</code></td>
<td>Display staged changes.</td>
</tr>

</table>

---

## 📦 Staging Files

<table>

<tr>
<th width="35%">Command</th>
<th>Description</th>
</tr>

<tr>
<td><code>git add &lt;file&gt;</code></td>
<td>Stage a specific file.</td>
</tr>

<tr>
<td><code>git add .</code></td>
<td>Stage all modified files.</td>
</tr>

<tr>
<td><code>git add -A</code></td>
<td>Stage all changes including deletions.</td>
</tr>

<tr>
<td><code>git restore --staged &lt;file&gt;</code></td>
<td>Remove a file from the staging area.</td>
</tr>

</table>

---

## 💾 Commit Changes

<table>

<tr>
<th width="35%">Command</th>
<th>Description</th>
</tr>

<tr>
<td><code>git commit -m "message"</code></td>
<td>Create a commit.</td>
</tr>

<tr>
<td><code>git commit -am "message"</code></td>
<td>Stage tracked files and commit.</td>
</tr>

<tr>
<td><code>git commit --amend</code></td>
<td>Edit the most recent commit.</td>
</tr>

</table>

---

## 🌿 Branches

<table>

<tr>
<th width="35%">Command</th>
<th>Description</th>
</tr>

<tr>
<td><code>git branch</code></td>
<td>List all local branches.</td>
</tr>

<tr>
<td><code>git branch &lt;branch&gt;</code></td>
<td>Create a new branch.</td>
</tr>

<tr>
<td><code>git switch &lt;branch&gt;</code></td>
<td>Switch to another branch.</td>
</tr>

<tr>
<td><code>git switch -c &lt;branch&gt;</code></td>
<td>Create and switch to a new branch.</td>
</tr>

<tr>
<td><code>git checkout &lt;branch&gt;</code></td>
<td>Switch branch (legacy command).</td>
</tr>

<tr>
<td><code>git branch -d &lt;branch&gt;</code></td>
<td>Delete a merged branch.</td>
</tr>

<tr>
<td><code>git branch -D &lt;branch&gt;</code></td>
<td>Force delete a branch.</td>
</tr>

</table>

---

## ☁️ Remote Repository

<table>

<tr>
<th width="35%">Command</th>
<th>Description</th>
</tr>

<tr>
<td><code>git remote -v</code></td>
<td>List remote repositories.</td>
</tr>

<tr>
<td><code>git remote add origin &lt;url&gt;</code></td>
<td>Add a remote repository.</td>
</tr>

<tr>
<td><code>git remote remove origin</code></td>
<td>Remove a remote repository.</td>
</tr>

<tr>
<td><code>git remote rename origin upstream</code></td>
<td>Rename a remote.</td>
</tr>

</table>

---

## 🚀 Push & Pull

<table>

<tr>
<th width="35%">Command</th>
<th>Description</th>
</tr>

<tr>
<td><code>git push</code></td>
<td>Push commits to remote.</td>
</tr>

<tr>
<td><code>git push origin main</code></td>
<td>Push the main branch.</td>
</tr>

<tr>
<td><code>git push -u origin main</code></td>
<td>Set upstream and push.</td>
</tr>

<tr>
<td><code>git pull</code></td>
<td>Fetch and merge remote changes.</td>
</tr>

<tr>
<td><code>git fetch</code></td>
<td>Download changes without merging.</td>
</tr>

</table>

---

## 🔀 Merge & Rebase

<table>

<tr>
<th width="35%">Command</th>
<th>Description</th>
</tr>

<tr>
<td><code>git merge &lt;branch&gt;</code></td>
<td>Merge another branch.</td>
</tr>

<tr>
<td><code>git merge --abort</code></td>
<td>Cancel a merge.</td>
</tr>

<tr>
<td><code>git rebase main</code></td>
<td>Rebase onto the main branch.</td>
</tr>

<tr>
<td><code>git rebase --continue</code></td>
<td>Continue after resolving conflicts.</td>
</tr>

<tr>
<td><code>git rebase --abort</code></td>
<td>Cancel a rebase.</td>
</tr>

</table>

---

## ↩️ Undo Changes

<table>

<tr>
<th width="35%">Command</th>
<th>Description</th>
</tr>

<tr>
<td><code>git restore &lt;file&gt;</code></td>
<td>Restore a modified file.</td>
</tr>

<tr>
<td><code>git restore .</code></td>
<td>Restore all modified files.</td>
</tr>

<tr>
<td><code>git reset HEAD &lt;file&gt;</code></td>
<td>Unstage a file.</td>
</tr>

<tr>
<td><code>git reset --soft HEAD~1</code></td>
<td>Undo last commit but keep staged changes.</td>
</tr>

<tr>
<td><code>git reset --mixed HEAD~1</code></td>
<td>Undo commit and unstage changes.</td>
</tr>

<tr>
<td><code>git reset --hard HEAD~1</code></td>
<td>Completely discard the last commit.</td>
</tr>

</table>

---

## 📚 Stash

<table>

<tr>
<th width="35%">Command</th>
<th>Description</th>
</tr>

<tr>
<td><code>git stash</code></td>
<td>Temporarily save changes.</td>
</tr>

<tr>
<td><code>git stash list</code></td>
<td>Show saved stashes.</td>
</tr>

<tr>
<td><code>git stash pop</code></td>
<td>Restore and remove the latest stash.</td>
</tr>

<tr>
<td><code>git stash apply</code></td>
<td>Apply stash without removing it.</td>
</tr>

<tr>
<td><code>git stash drop</code></td>
<td>Delete a stash.</td>
</tr>

</table>

---

## 🏷️ Tags

<table>

<tr>
<th width="35%">Command</th>
<th>Description</th>
</tr>

<tr>
<td><code>git tag</code></td>
<td>List tags.</td>
</tr>

<tr>
<td><code>git tag v1.0</code></td>
<td>Create a lightweight tag.</td>
</tr>

<tr>
<td><code>git tag -a v1.0 -m "Release"</code></td>
<td>Create an annotated tag.</td>
</tr>

<tr>
<td><code>git push origin v1.0</code></td>
<td>Push a tag to the remote.</td>
</tr>

</table>

---

## 🔍 Inspection

<table>

<tr>
<th width="35%">Command</th>
<th>Description</th>
</tr>

<tr>
<td><code>git log --oneline</code></td>
<td>Compact commit history.</td>
</tr>

<tr>
<td><code>git log --graph --all</code></td>
<td>Graphical commit history.</td>
</tr>

<tr>
<td><code>git show</code></td>
<td>Show latest commit details.</td>
</tr>

<tr>
<td><code>git blame &lt;file&gt;</code></td>
<td>Display line-by-line author history.</td>
</tr>

<tr>
<td><code>git reflog</code></td>
<td>Show reference history.</td>
</tr>

</table>

---

## 🧹 Cleanup

<table>

<tr>
<th width="35%">Command</th>
<th>Description</th>
</tr>

<tr>
<td><code>git clean -n</code></td>
<td>Preview untracked files to remove.</td>
</tr>

<tr>
<td><code>git clean -f</code></td>
<td>Delete untracked files.</td>
</tr>

<tr>
<td><code>git clean -fd</code></td>
<td>Delete untracked files and folders.</td>
</tr>

</table>

---

# 🔄 Basic Git Workflow

```text
Initialize Repository
        │
        ▼
git init
        │
        ▼
Edit Files
        │
        ▼
git status
        │
        ▼
git add .
        │
        ▼
git commit -m "Your Message"
        │
        ▼
git push origin main
```

---

# 📖 Official References

| Resource | Link |
|----------|------|
| Git Documentation | https://git-scm.com/doc |
| Git Reference | https://git-scm.com/docs |
| GitHub Git Guide | https://docs.github.com/en/get-started/using-git |
| Pro Git Book (Free) | https://git-scm.com/book/en/v2 |

---

⭐ **Tip:** Bookmark this README as your everyday Git quick-reference.

# 🧰 VS Code Troubleshooting & Recovery Guide

> **A complete practical guide to fixing common Visual Studio Code issues using the GUI, keyboard shortcuts, Command Palette, terminal/CLI, Windows File Explorer, and settings.**

---

## 📑 Table of Contents

* [🎯 Quick Diagnosis](#-quick-diagnosis)
* [📁 Folder & Explorer Issues](#-folder--explorer-issues)
* [⌨️ Keyboard Solutions](#️-keyboard-solutions)
* [🖱️ GUI & Selection Methods](#️-gui--selection-methods)
* [💻 CLI & Terminal Solutions](#-cli--terminal-solutions)
* [🪟 Windows File Explorer Solutions](#-windows-file-explorer-solutions)
* [🔄 VS Code UI Recovery](#-vs-code-ui-recovery)
* [📦 Extensions Troubleshooting](#-extensions-troubleshooting)
* [⚙️ Settings Troubleshooting](#️-settings-troubleshooting)
* [🧹 Cache & Data Recovery](#-cache--data-recovery)
* [🚀 Project-Specific Issues](#-project-specific-issues)
* [🛠️ Complete Recovery Workflow](#️-complete-recovery-workflow)
* [⚡ Quick Command Reference](#-quick-command-reference)

---

# 🎯 Quick Diagnosis

| What you see                      | Most likely cause               | First solution                    |
| --------------------------------- | ------------------------------- | --------------------------------- |
| VS Code opens but no files appear | No folder opened                | `Ctrl + K` → `Ctrl + O`           |
| Explorer is missing               | Explorer view hidden            | `Ctrl + Shift + E`                |
| Folder appears but is empty       | Wrong folder opened             | Check the folder path             |
| `Open with Code` missing          | Shell integration not installed | Reinstall VS Code with PATH       |
| `code .` not recognized           | VS Code not in PATH             | Reinstall / add CLI to PATH       |
| Files disappeared from Explorer   | Exclude settings                | Check `files.exclude`             |
| VS Code looks broken              | View layout problem             | Reset View Locations              |
| Extension causes errors           | Extension conflict              | Disable extensions                |
| Project will not run              | Wrong directory/dependencies    | Check terminal and `package.json` |
| VS Code is very slow              | Extension/cache issue           | Disable extensions and reload     |

---

# 📁 Folder & Explorer Issues

## 1️⃣ Open a Folder Using the Menu

### GUI Method

```text
File
  ↓
Open Folder...
  ↓
Select Project Folder
  ↓
Select Folder
```

### Best for

* Beginners
* Opening a project for the first time
* Selecting folders from another drive

---

## 2️⃣ Open a Folder Using Keyboard

Press:

```text
Ctrl + K
```

Then:

```text
Ctrl + O
```

### Workflow

```text
Ctrl + K → Ctrl + O
        ↓
Select Folder
        ↓
Select Folder
```

---

## 3️⃣ Open the Explorer Panel

Shortcut:

```text
Ctrl + Shift + E
```

Or:

```text
View → Explorer
```

If Explorer is visible but empty, check whether a folder is actually opened.

---

## 4️⃣ Open a File

```text
Ctrl + O
```

This opens a **single file**.

⚠️ This is different from opening a complete project folder.

### Single File

```text
index.html
```

### Complete Project

```text
my-project/
├── index.html
├── style.css
├── script.js
└── package.json
```

For projects, always prefer:

```text
File → Open Folder...
```

---

## 5️⃣ Add Another Folder to the Workspace

Use:

```text
File → Add Folder to Workspace...
```

This is useful for:

```text
Frontend
Backend
Database
```

Example:

```text
My Application
├── frontend/
├── backend/
└── database/
```

---

## 6️⃣ Remove a Folder from Workspace

Right-click the folder name in Explorer:

```text
Remove Folder from Workspace
```

⚠️ This does not delete the actual folder from your computer.

---

# ⌨️ Keyboard Solutions

## Essential Shortcuts

| Action              | Shortcut                    |
| ------------------- | --------------------------- |
| Open File           | `Ctrl + O`                  |
| Open Folder         | `Ctrl + K`, then `Ctrl + O` |
| Open Explorer       | `Ctrl + Shift + E`          |
| Command Palette     | `Ctrl + Shift + P`          |
| Integrated Terminal | `` Ctrl + ` ``              |
| Search Files        | `Ctrl + P`                  |
| Search in Project   | `Ctrl + Shift + F`          |
| Settings            | `Ctrl + ,`                  |
| Reload Window       | Command Palette             |
| Close Folder        | `Ctrl + K`, then `F`        |
| Save                | `Ctrl + S`                  |
| Save All            | `Ctrl + K`, then `S`        |
| New File            | `Ctrl + N`                  |
| New Window          | `Ctrl + Shift + N`          |
| Close Window        | `Alt + F4`                  |

---

# 🧭 Command Palette: The Universal VS Code Fix Tool

Open it:

```text
Ctrl + Shift + P
```

Search for commands such as:

```text
View: Reset View Locations
Developer: Reload Window
Developer: Restart Extension Host
Preferences: Open Settings (UI)
Extensions: Disable All Installed Extensions
Workspaces: Close Workspace
```

### ⭐ General Rule

> If you do not know how to fix something in VS Code, first try `Ctrl + Shift + P`.

---

# 🖱️ GUI & Selection Methods

## Method A — File Menu

```text
File → Open Folder...
```

## Method B — Explorer Right-Click

```text
Right-click Folder
        ↓
Open with Code
```

## Method C — Drag & Drop

You can drag a folder from Windows File Explorer directly into the VS Code window.

## Method D — VS Code Start Page

On the Welcome screen:

```text
Open Folder
```

Then select the project.

---

# 💻 CLI & Terminal Solutions

## 1️⃣ Open the Current Folder

```bash
code .
```

Example:

```bash
cd C:\xampp\htdocs\my-project
code .
```

---

## 2️⃣ Open a Specific Folder

```bash
code "C:\xampp\htdocs\my-project"
```

---

## 3️⃣ Open a Specific File

```bash
code index.html
```

---

## 4️⃣ Open Multiple Files

```bash
code index.html style.css script.js
```

---

## 5️⃣ Open a New VS Code Window

```bash
code . --new-window
```

---

## 6️⃣ Check Whether the CLI Works

```bash
code --version
```

### If you get:

```text
'code' is not recognized...
```

VS Code is probably not correctly added to your system PATH.

### Fix

Reinstall VS Code and enable:

```text
☑ Add to PATH
```

Then restart your terminal.

---

# 🪟 Windows File Explorer Solutions

## Method 1 — Right-Click

```text
Project Folder
    ↓
Right-click
    ↓
Open with Code
```

---

## Method 2 — Address Bar

Open the project folder in File Explorer.

Click the address bar and type:

```bash
cmd
```

Press:

```text
Enter
```

Then:

```bash
code .
```

---

## Method 3 — PowerShell

Right-click inside the folder:

```text
Open in Terminal
```

Then:

```bash
code .
```

---

# 🔄 VS Code UI Recovery

## Problem: Explorer Layout Is Broken

Open:

```text
Ctrl + Shift + P
```

Search:

```text
View: Reset View Locations
```

Press:

```text
Enter
```

---

## Problem: VS Code Is Frozen or UI Is Not Updating

Open Command Palette:

```text
Ctrl + Shift + P
```

Run:

```text
Developer: Reload Window
```

---

## Problem: Extensions Are Not Working

Run:

```text
Developer: Restart Extension Host
```

---

## Problem: Sidebar Is Hidden

Press:

```text
Ctrl + B
```

This toggles the primary sidebar.

Then open Explorer:

```text
Ctrl + Shift + E
```

---

# 📦 Extensions Troubleshooting

Extensions can cause:

* Slow VS Code
* Crashes
* Errors
* Missing features
* Broken syntax highlighting

## Disable an Extension

1. Open Extensions:

```text
Ctrl + Shift + X
```

2. Search for the extension.
3. Click the gear icon.
4. Choose:

```text
Disable
```

---

## Test Without Extensions

From terminal:

```bash
code --disable-extensions
```

If VS Code works correctly now, an extension is probably causing the issue.

---

# ⚙️ Settings Troubleshooting

Open Settings:

```text
Ctrl + ,
```

Or open `settings.json`:

```text
Ctrl + Shift + P
```

Search:

```text
Preferences: Open User Settings (JSON)
```

---

## Check Files Excluded from Explorer

Search settings for:

```text
files.exclude
```

Example:

```json
{
  "files.exclude": {
    "**/node_modules": true
  }
}
```

⚠️ If an important folder is set to `true`, it may be hidden from Explorer.

---

## Check Search Exclusions

Search for:

```text
search.exclude
```

A folder may be hidden from search even though it exists.

---

# 🧹 Cache & Data Recovery

If VS Code behaves unusually:

### First try

```text
Ctrl + Shift + P
```

Then:

```text
Developer: Reload Window
```

### Next

Restart VS Code completely.

### Then

Restart Windows.

> Always try the least destructive solution first.

---

# 🚀 Project-Specific Issues

## Node.js Project

Check:

```text
package.json
```

Run:

```bash
npm install
```

Then:

```bash
npm run dev
```

---

## Python Project

Check Python:

```bash
python --version
```

Run a file:

```bash
python main.py
```

---

## Git Project

Check Git:

```bash
git --version
```

Check project status:

```bash
git status
```

---

## PHP Project

Example:

```text
C:\xampp\htdocs\my-project
```

Open:

```bash
cd C:\xampp\htdocs\my-project
code .
```

---

# 🛠️ Complete Recovery Workflow

Follow this order when VS Code has a problem:

```text
┌──────────────────────────────┐
│ 1. Check the Project Folder  │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ 2. Open Explorer             │
│    Ctrl + Shift + E          │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ 3. Open Folder Again          │
│    Ctrl + K → Ctrl + O        │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ 4. Try Terminal               │
│    code .                     │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ 5. Reload Window              │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ 6. Reset View Locations       │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ 7. Disable Extensions         │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ 8. Check Settings             │
└──────────────────────────────┘
```

---

# ⚡ Quick Fix Cheat Sheet

### 📁 Open Folder

```text
Ctrl + K → Ctrl + O
```

### 📂 Open Explorer

```text
Ctrl + Shift + E
```

### 🧭 Open Command Palette

```text
Ctrl + Shift + P
```

### 💻 Open Current Folder from Terminal

```bash
code .
```

### 🔄 Reload VS Code

```text
Ctrl + Shift + P
→ Developer: Reload Window
```

### 🧹 Reset Layout

```text
Ctrl + Shift + P
→ View: Reset View Locations
```

### 🧩 Test Without Extensions

```bash
code --disable-extensions
```

### ⚙️ Open Settings

```text
Ctrl + ,
```

### 🧱 Open Extensions

```text
Ctrl + Shift + X
```

---

# 🧠 Golden Rule

> **Start with the simplest solution and move toward advanced solutions.**

```text
GUI
 ↓
Keyboard Shortcut
 ↓
Command Palette
 ↓
Terminal / CLI
 ↓
Settings
 ↓
Extensions
 ↓
System Repair
```

---

## ✅ Recommended Troubleshooting Order

1. **Check the folder**
2. **Open the folder again**
3. **Open Explorer**
4. **Use `code .`**
5. **Reload VS Code**
6. **Reset the layout**
7. **Check Settings**
8. **Disable extensions**
9. **Restart VS Code**
10. **Restart Windows**
11. **Reinstall VS Code as a last resort**

---

> ⭐ **Most common solution for the problem where VS Code opens but files do not appear:**
>
> ```text
> Ctrl + K → Ctrl + O
> ```
>
> Select the correct project folder, then:
>
> ```text
> Ctrl + Shift + E
> ```
>
> Your project files should appear in the Explorer.

````
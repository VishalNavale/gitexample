# First Git Example — Start and Learn (VS Code, PowerShell)

This is a tiny hands-on Git example for beginners using Visual Studio Code on Windows (PowerShell). It contains a minimal Python app and step-by-step commands to practice commits, branches, and merges.

Files added:
- `hello.py` — a simple Python script
- `.gitignore` — common ignores for this example

Quick goals:
- Initialize or use an existing git repo
- Make an initial commit
- Create a feature branch and add a change
- Merge the feature branch back into `main`

Prerequisites
- Install Git: https://git-scm.com/
- Install Python (optional for running the sample): https://www.python.org/
- Install Visual Studio Code: https://code.visualstudio.com/

Open the folder in VS Code

1. In VS Code: `File` → `Open Folder...` → select this repository folder.
2. Open the built-in terminal: `Terminal` → `New Terminal` (PowerShell will be used by default).

PowerShell commands (copy-paste into the repo root terminal)

Initialize (only if repo is not already a git repo):
```powershell
git init
```

Check status, stage and commit:
```powershell
git status
git add .
git commit -m "chore: initial commit with hello.py"
```

Create and switch to a feature branch:
```powershell
git branch -M main
git checkout -b feat/first-example
```

Make an edit (example: change the message in `hello.py`), then:
```powershell
git add hello.py
git commit -m "feat: update greeting message"
```

Switch back to `main` and merge the feature branch:
```powershell
git checkout main
git merge --no-ff feat/first-example -m "merge: bring feat/first-example into main"
```

If you have a GitHub remote, push the branches:
```powershell
git remote add origin https://github.com/<your-username>/hello-world.git
git push -u origin main
git push -u origin feat/first-example
```

Using VS Code Source Control UI
- Click the Source Control icon (left activity bar). You can stage, commit, create branches, and push/pull from the UI.

Run the sample app
```powershell
python hello.py
```

Next steps and tips
- Try creating a second branch and resolving a merge conflict to practice conflict resolution.
- Use `git log --oneline --graph --all` to visualize the commit history.
- Explore VS Code extensions: GitLens helps see blame, history, and branch info.

Happy learning! If you want, I can also add a small README section that demonstrates a merge conflict you can practice resolving.

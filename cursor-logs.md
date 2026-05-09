## [2026-05-10 12:15] - Fix Git tracking for frontend directory

**Problem/Request:**
The user was unable to push changes from the `frontend` folder to the repository because Git was ignoring the entire directory.

**Files/State Modified:**
- `frontend/.git` directory (removed)
- Git index (removed `frontend` as a submodule, added contents of `frontend` as regular files)

**Solution Summary:**
The root cause was that `frontend` was initialized as a Git Submodule (it contained its own hidden `.git` folder). When a folder has its own `.git` directory, the parent repository ignores its contents and only tracks it as a submodule reference. 
1. I deleted the nested `frontend/.git` folder using PowerShell.
2. I cleared the submodule cache using `git rm --cached frontend`.
3. I added the frontend files to the root repository using `git add frontend/`.

**Verification:**
Running `git status` confirmed that all files inside `frontend/` (like `index.tsx`, `package.json`, etc.) are now correctly staged as new files in the main repository.

**Outcome:**
✅ Success
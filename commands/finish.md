---
description: Ship the current changes as a pull request to main
allowed-tools: [Bash, Read, Glob]
---
Ship the current changes as a pull request to main.

1. **Show what's changed**:
   ```bash
   git status
   git diff
   git log origin/main..HEAD --oneline
   ```

2. **Review the diff** — summarise the changes in 2-3 sentences and draft a commit message.

3. **Stage and commit** (prefer staging specific files over `git add .`):
   ```bash
   git add <files>
   git commit -m "<message>"
   ```

4. **Push and open a PR targeting main**:
   ```bash
   git push -u origin HEAD
   gh pr create --base main --title "<title>" --body "<body>"
   ```

5. **Report the PR URL** to the user.

6. **Kill background servers** (but leave the worktree intact):
   ```bash
   [ -f .dev.pid ] && kill $(cat .dev.pid) 2>/dev/null; true
   ```

If there are failing tests or lint errors, fix them before committing.

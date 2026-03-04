---
description: Initialise this worktree for development
allowed-tools: [Bash, Read, Glob]
---
Initialise this worktree for development.

Run these steps in order:

0. **Confirm we're in a worktree**, not the main repo:
   ```bash
   MAIN_REPO=$(git worktree list | head -1 | awk '{print $1}')
   pwd
   ```
   If `pwd` equals `MAIN_REPO`, stop and tell the user:
   > "You're in the main repo. Run `claude --worktree` to start a dev session."

1. **Symlink env files** — check `CLAUDE.md`'s `## Dev Commands` section for which env files to symlink, then link each from the main repo (only if it exists there):
   ```bash
   MAIN_REPO=$(git worktree list | head -1 | awk '{print $1}')
   # e.g. [ -f "$MAIN_REPO/.env.development" ] && ln -sf "$MAIN_REPO/.env.development" .env.development
   ```

2. **Find free ports** (frontend ≥ 5174, backend ≥ 3002):
   ```bash
   FE_PORT=5174
   while lsof -ti:$FE_PORT >/dev/null 2>&1; do FE_PORT=$((FE_PORT+1)); done
   BE_PORT=3002
   while lsof -ti:$BE_PORT >/dev/null 2>&1; do BE_PORT=$((BE_PORT+1)); done
   ```

3. **Check git status and sync with main**:
   ```bash
   git status
   git fetch origin main
   ```

4. **Install dependencies** — use the install commands from `CLAUDE.md`'s `## Dev Commands` section, only if `node_modules` is missing.

5. **Start dev servers in the background** — use the start command from `CLAUDE.md`'s `## Dev Commands` section, passing dynamic port env vars:
   ```bash
   VITE_PORT=$FE_PORT VITE_API_PORT=$BE_PORT PORT=$BE_PORT FRONTEND_URL=http://localhost:$FE_PORT \
     <start command> > ./dev.log 2>&1 &
   echo $! > .dev.pid
   ```

6. **Open the app in the browser** — if this project has a frontend, wait a few seconds for the dev server to boot, then open `http://localhost:$FE_PORT` using the browser tools (`mcp__claude-in-chrome__navigate`). This starts an active Claude debug session so you can see and interact with the running app. Skip this step if there is no frontend.

7. **Report to user**:
   - Frontend: http://localhost:$FE_PORT
   - Backend: http://localhost:$BE_PORT
   - Branch: `git branch --show-current`
   - Logs: `tail -f ./dev.log`
   - Any uncommitted changes to be aware of

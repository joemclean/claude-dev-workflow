# claude-dev-workflow

A Claude Code plugin providing four slash commands for a consistent feature development workflow: spec → start → review → finish.

## Commands

| Command | Description |
|---------|-------------|
| `/spec` | Interview-driven feature spec writer |
| `/start` | Initialise a worktree dev session (ports, deps, servers) |
| `/review` | Review changes for correctness, security, types, and test coverage |
| `/finish` | Commit, push, and open a PR to main |

### `/spec`
Walks you through four questions (what, who, success criteria, constraints) and produces a structured spec with user stories, technical approach, and acceptance criteria.

### `/start`
Sets up a worktree for development: symlinks env files, finds free ports, installs dependencies if needed, and starts dev servers in the background. Requires a `## Dev Commands` section in your project's `CLAUDE.md`.

### `/review`
Diffs your branch against `origin/main`, evaluates each changed file for correctness, security, types, error handling, and test coverage, then runs your project's lint and test commands.

### `/finish`
Stages and commits your changes, pushes the branch, and opens a pull request targeting `main` via the `gh` CLI.

## Installation

### As a Claude Code plugin (recommended)

Clone this repo into your Claude plugins directory:

```bash
git clone https://github.com/<your-org>/claude-dev-workflow \
  ~/.claude/plugins/claude-dev-workflow
```

Claude Code will automatically pick up the commands on next launch.

### Manual install

Copy the command files directly into your global commands folder:

```bash
git clone https://github.com/<your-org>/claude-dev-workflow /tmp/claude-dev-workflow
cp /tmp/claude-dev-workflow/commands/*.md ~/.claude/commands/
```

Or into a project-local `.claude/commands/` directory to scope them to one repo.

## Project setup

`/start` and `/review` read your project's `CLAUDE.md` for dev commands. Add a section like this:

```markdown
## Dev Commands

- **Install**: `npm install`
- **Start**: `npm run dev`
- **Lint**: `npm run lint`
- **Test**: `npm test`
- **Env files**: `.env.development`
```

## Workflow

```
/spec      → write a spec for the feature
/start     → boot up a dev session in a worktree
             (make your changes)
/review    → check the diff before shipping
/finish    → commit, push, open PR
```

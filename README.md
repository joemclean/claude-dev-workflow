# claude-dev-workflow

Four Claude Code skills for a consistent feature development workflow:

| Skill | Description |
|-------|-------------|
| `spec` | Interview-driven feature spec writer |
| `start` | Initialise a worktree dev session (ports, deps, servers) |
| `review` | Review changes for correctness, security, types, and test coverage |
| `finish` | Commit, push, and open a PR to main |

## Installation

Clone this repo, then copy the skills into your Claude commands directory:

```bash
git clone https://github.com/your-org/claude-dev-workflow
cp claude-dev-workflow/skills/*.md ~/.claude/commands/
```

Or into a project-local `.claude/commands/` to scope them to one repo.

That's it — restart Claude Code and the commands will be available.

## Project setup

`/start` and `/review` read your project's `CLAUDE.md` for dev commands. Add a section like:

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

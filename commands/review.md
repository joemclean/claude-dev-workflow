---
description: Review the current changes before submitting
allowed-tools: [Bash, Read, Glob, Grep]
---
Review the current changes before submitting.

1. **Get the full diff vs main**:
   ```bash
   git diff origin/main..HEAD
   git log origin/main..HEAD --oneline
   ```

2. **For each changed file evaluate**:
   - **Correctness**: does it do what it claims?
   - **Security**: any injection, auth bypass, data exposure, or missing validation?
   - **Types**: if TypeScript, are types correct, strict, and avoiding `any`?
   - **Error handling**: are all error paths handled gracefully?
   - **Tests**: is there test coverage for the changes?

3. **Run lint and tests** — use the lint and test commands from `CLAUDE.md`'s `## Dev Commands` section.

4. **Report findings** with specific `file:line` references and concrete suggestions.

5. If everything looks good, say so clearly and suggest running `/finish`.

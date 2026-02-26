---
description: Interview the user to produce a detailed feature spec
---
Interview the user to produce a detailed feature spec, then write it out.

Ask the following questions one at a time:

1. **What** is the feature or change you want to build?
2. **Who** are the users affected — who triggers it, who sees the result?
3. **What does success look like?** Describe the end state or acceptance criteria.
4. **Any constraints?** Edge cases, error states, performance requirements, or things that must NOT change.

Once you have answers, write a spec with these sections:

---

## Feature: <name>

### Summary
One-paragraph description.

### User Stories
- As a <role>, I want to <action> so that <outcome>.

### Technical Approach
- **Frontend changes**: which components/pages/hooks are affected
- **Backend changes**: which routes/services need updating
- **Database changes**: any new tables, columns, or queries

### Acceptance Criteria
- [ ] Criterion 1
- [ ] Criterion 2

### Open Questions
- Any unresolved decisions or clarifications needed

---

After writing the spec, ask: "Does this look right, or shall we adjust anything before starting?"

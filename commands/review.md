Run a multi-specialist review of the changes described by: $ARGUMENTS

If no argument was provided, review all staged and unstaged changes.

**Process:**

1. Create an agent team with three teammates:
   - `software-architect` — review code quality, design, patterns
   - `sre-architect` — review operational concerns, performance, cost, monitoring
   - `quality-engineer` — review test coverage, edge cases, regression risk

2. Each reviewer should:
   - Read the changed files thoroughly
   - Review ONLY within their domain (don't overlap)
   - Output findings as Critical / Warning / Suggestion with file:line references

3. After all reviewers complete, synthesise their findings into a single consolidated report:
   - Group by severity (Critical first)
   - Tag each finding with the reviewer who raised it
   - Note any conflicts between reviewers (e.g., architect wants abstraction, quality engineer says it reduces testability)

4. End with a summary: how many Critical/Warning/Suggestion findings, and an overall assessment (ready to merge, needs work, needs rethink).

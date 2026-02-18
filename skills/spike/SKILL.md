---
name: spike
description: Evaluate competing technical approaches by spawning one agent per option to build a proof of concept and compare trade-offs
disable-model-invocation: true
argument-hint: "[question or decision to evaluate]"
---

## Your task

Evaluate competing approaches for: $ARGUMENTS

**Process:**

1. Identify 2-4 distinct approaches to the problem. Each should be a genuinely different strategy, not minor variations of the same thing.

2. Create an agent team. Spawn one teammate per approach. Each teammate should:
   - Research their assigned approach (docs, examples, existing usage in the codebase)
   - Assess feasibility and fit for this specific project
   - Identify trade-offs: cost, complexity, performance, maintainability, team familiarity
   - Estimate effort to implement
   - List risks and unknowns
   - If practical, sketch out what the implementation would look like (key files, interfaces, data flow)

3. After all researchers report, facilitate a comparison:
   - Create a trade-off matrix (approaches as columns, criteria as rows)
   - Identify deal-breakers for any approach
   - Note where approaches are roughly equivalent (don't over-differentiate)

4. Synthesise into a recommendation:
   - Recommended approach with clear justification
   - Runner-up and when you'd choose it instead
   - What to prototype first to validate the recommendation
   - Key risks to monitor during implementation

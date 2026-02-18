# claude-team-agents

Opinionated specialist agents and team workflows for Claude Code. Focused on doing fewer things well rather than covering everything.

## Philosophy

Inspired by [Trail of Bits' approach](https://github.com/trailofbits/claude-code-config): agents encode **expertise, not procedures**. Each agent knows *how to think* about its domain, not just what steps to follow. They include reference material (anti-pattern catalogues, checklists, smell guides) that make them expert-level rather than superficial.

Key principles:
- **Agents don't overlap** — each has a clear domain boundary and explicitly states what it doesn't do
- **Severity is standardised** — Critical/Warning/Suggestion across all agents, with consistent meaning
- **Memory is enabled** — agents learn your codebase patterns across sessions via `memory: project`
- **Cost-conscious** — review agents use Sonnet (fast, cheap for read-only analysis); only the orchestrator inherits your session model

## What's Included

### Review Agents

| Agent | Domain | Key Focus |
|-------|--------|-----------|
| `software-architect` | Code quality | Design patterns, SOLID, coupling, cohesion, naming, dead code |
| `sre-architect` | Operations | Cost, performance, reliability, observability, failure modes |
| `quality-engineer` | Testing | Behavioural coverage, test quality, strategy, testability, risk |
| `security-auditor` | App security | OWASP top 10, injection, auth, data exposure, dependencies |

### Orchestration

| Agent | Role |
|-------|------|
| `tech-lead` | Reads your changes, decides which specialists to involve, synthesises findings |

### Investigation

| Agent | Role |
|-------|------|
| `investigator` | Pursues a single hypothesis. Spawned in teams for competing-hypotheses debugging |

### Skills (Slash Commands)

| Command | What It Does |
|---------|-------------|
| `/review [scope]` | Spawns architect + SRE + quality in parallel. Scope can be a path, branch, or "staged" |
| `/investigate [bug description]` | Spawns 3-5 investigators each pursuing different hypotheses, then debate |
| `/spike [question]` | Spawns one agent per competing approach to evaluate trade-offs side by side |

## Installation

### Option 1: Claude Code Plugin (recommended)

```bash
# From any Claude Code session:
/plugin install https://github.com/rayh/claude-team-agents
```

### Option 2: Copy to Global Config

```bash
# Clone the repo
git clone https://github.com/rayh/claude-team-agents.git
cd claude-team-agents

# Copy agents and skills to your global Claude config
cp -r agents/* ~/.claude/agents/
mkdir -p ~/.claude/skills/review ~/.claude/skills/investigate ~/.claude/skills/spike
cp skills/review/SKILL.md ~/.claude/skills/review/
cp skills/investigate/SKILL.md ~/.claude/skills/investigate/
cp skills/spike/SKILL.md ~/.claude/skills/spike/
```

### Option 3: Copy to a Specific Project

```bash
# From your project root
cp -r agents/* .claude/agents/
cp -r skills/* .claude/skills/
```

### Enable Agent Teams

Agent teams are experimental. Add to your `~/.claude/settings.json`:

```json
{
  "env": {
    "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"
  }
}
```

## Usage

### Quick Review (After Making Changes)

```
/review staged
/review src/api/
/review feature-branch
```

### Smart Review (Let Tech Lead Decide)

```
Use the tech-lead to review my recent changes
```

The tech-lead reads the diff, consults its decision matrix, and only spawns relevant specialists. A one-line bug fix gets quality-engineer only. An API change gets all four.

### Bug Investigation

```
/investigate Users report intermittent 500 errors on POST /api/sessions after deploying v2.3
```

### Technical Spike

```
/spike Should we use Redis, DynamoDB, or PostgreSQL for session storage?
```

### Single Specialist

```
Use the security-auditor to review the OAuth implementation in src/auth/
Use the sre-architect to evaluate the docker-compose.yml
```

## When to Use What

| Situation | Use |
|-----------|-----|
| Finished a feature, want review | `/review` |
| Small fix, just want test review | `Use quality-engineer to review...` |
| Infra change | `Use sre-architect to review...` |
| Weird bug, unclear root cause | `/investigate` |
| Choosing between technologies | `/spike` |
| Complex change, need orchestration | `Use tech-lead to review...` |
| Security-sensitive change | `Use security-auditor to audit...` |

## Team Topology Ideas

Beyond the included agents, these patterns work well with agent teams:

### Migration/Refactor Team
- **Scout**: maps all usages of the thing being changed
- **Implementer(s)**: one per module to avoid file conflicts
- **Verifier**: runs tests after each batch, reports regressions

### Documentation Team
- **Reader**: traces code flows, builds understanding
- **Writer**: produces docs from reader's findings
- **Reviewer**: checks docs against actual code

### Incident Response Team
- **Timeline builder**: reconstructs what happened from logs/metrics
- **Root cause analyst**: investigates code for the underlying bug
- **Remediation planner**: proposes fix + prevention measures

## Customisation

All agents are markdown files with YAML frontmatter. Edit them to:

- **Adjust severity calibration** — if an agent flags too many Warnings for things you consider fine
- **Add project-specific context** — domain knowledge, tech stack details, team conventions
- **Change models** — upgrade to `opus` for more thorough reviews, or `haiku` for quick checks
- **Restrict tools** — remove `Bash` if you want purely read-only analysis

## Prior Art & Inspiration

This project builds on ideas from:
- [trailofbits/claude-code-config](https://github.com/trailofbits/claude-code-config) — "encode expertise not procedures"
- [VoltAgent/awesome-claude-code-subagents](https://github.com/VoltAgent/awesome-claude-code-subagents) — 100+ agent definitions
- [contains-studio/agents](https://github.com/contains-studio/agents) — departmental agent organisation
- [affaan-m/everything-claude-code](https://github.com/affaan-m/everything-claude-code) — battle-tested config collection
- [wshobson/agents](https://github.com/wshobson/agents) — plugin-based orchestration patterns
- [Addy Osmani's agent teams writeup](https://addyosmani.com/blog/claude-code-agent-teams/) — narrow scope = better reasoning

## License

MIT

# CLAUDE.md – context for AI agents

## Project
- Name: {{PROJECT_NAME}}
- Pitch: {{one sentence}}
- PRD: `docs/PRD.md` (source of truth for scope — do not build anything outside it)
- Architecture decisions: `docs/adr/` (accepted ADRs are binding; propose a new ADR to change one)
- Linear team: `WiP` · project: {{LINEAR_PROJECT}}

## Roles
- **William (human PM):** owns the problem, validates PRD, design, architecture and demo.
- **Orchestrator (Claude):** breaks work into Linear tickets, dispatches agents, merges PRs.
- **Agents** (`.claude/agents/`): `dev`, `qa`, `reviewer`. Each works on exactly one ticket at a time.

## Working rules
1. **One ticket = one branch = one PR.** Branch name: `wip-<number>-short-slug` (e.g. `wip-12-login-form`). PR title starts with the ticket ID: `WIP-12: Add login form`. This links the PR to Linear automatically.
2. **Green CI is mandatory** before merge. Never disable or skip a test to make CI pass.
3. **Small PRs:** aim for < 400 changed lines. Split the ticket otherwise.
4. **Log every meaningful action** in `docs/BUILD_LOG.md` (date, actor, action, link). Actor is `human:william` or `agent:<role>`.
5. **Stop and ask the PM** only for: an irreversible decision, a scope change versus the PRD, or anything pushing the monthly cost above the budget in the ADRs.
6. **Secrets** never go in the repo. Use GitHub Actions secrets / the host's env vars and document the variable names in the README.
7. Code, comments, commits, docs: **English**.

## Commands
```bash
# install
{{install}}
# dev server
{{dev}}
# tests
{{test}}
# lint / typecheck
{{lint}}
```

## Definition of done
- Acceptance criteria of the Linear ticket are met
- Tests added or updated, CI green
- Reviewed by the `reviewer` agent
- BUILD_LOG updated, Linear ticket moved to Done

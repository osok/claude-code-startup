# Claude Code Sub-Agents Project

## Project Overview

A collection of specialized sub-agents designed to assist with application design, testing, deployment, and enhancement workflows.

---

## Current Work

<!-- This section tracks active work. Clear when complete. -->

**Seq:** -
**Name:** -
**Status:** Starting

**Current:** Awaiting project initialization

---

## Sub-Agent Index

<!-- Populated as agents are designed and built -->

## Sub-Agent Index

| Agent Name | Purpose | Status | Docs |
|------------|---------|--------|------|
| Requirements | Interactive requirements elicitation (ISO/IEC/IEEE 29148) | Defined | .claude/agents/requirements.md |
| Task Manager | Orchestrates workflow, tracks tasks, handles inter-agent requests | Defined | .claude/agents/task-manager.md |
| Architect | Architectural decisions, ADRs, project-wide standards | Defined | .claude/agents/architect.md |
| Designer | Design docs from requirements (IEEE 1016, mermaid UML) | Defined | .claude/agents/designer.md |
| Test Designer | Plans tests based on architecture and design | Defined | .claude/agents/test-designer.md |
| Data Agent | Schemas as source of truth, data dictionaries, migrations | Defined | .claude/agents/data-agent.md |
| Deployment | Environment config, docker compose, AWS CDK | Defined | .claude/agents/deployment.md |
| Developer | Implements code following project conventions | Defined | .claude/agents/developer.md |
| Test Coder | Writes test code (unit, integration, E2E) | Defined | .claude/agents/test-coder.md |
| Test Runner | Executes tests, debugs failures, routes issues | Defined | .claude/agents/test-runner.md |
| Test Debugger | Deep debugging across all layers; creates diagnosis for Task Manager routing | Defined | .claude/agents/test-debugger.md |
| Code Reviewer - Requirements | Reviews code completeness against requirements | Defined | .claude/agents/code-reviewer-requirements.md |
| Code Reviewer - Security | Reviews code for OWASP vulnerabilities | Defined | .claude/agents/code-reviewer-security.md |
| Code Reviewer - Integration | Reviews for stubs, incomplete code, wiring gaps | Defined | .claude/agents/code-reviewer-integration.md |
| Documentation | User docs, developer docs, code documentation | Defined | .claude/agents/documentation.md |

---

## Agent Workflow

Standard sequence for end-to-end feature development:

| Step | Agent(s) | Notes |
|------|----------|-------|
| 1 | @requirements | Elicit and document requirements (ISO 29148) |
| 2 | @architect | Architectural decisions, ADRs, constraints |
| 3 | @designer | Design docs from approved requirements |
| 4 | @test-designer, @data-agent | Plan tests; define schemas (parallel) |
| 5 | @task-manager | Create task list, orchestrate workflow |
| 6 | @developer(s) | Implement code (parallel per tech stack) |
| 7 | @code-reviewer-requirements, @code-reviewer-security, @code-reviewer-integration | Code review phase (parallel) |
| 8 | @developer(s) | Fix any gaps, vulnerabilities, or stubs found |
| 9 | *Loop to Step 7* | Re-review until all issues resolved |
| 10 | @test-designer | Revisit test plan after code complete |
| 11 | @documentation, @deployment | User/dev docs; environment setup (parallel) |
| 12 | @test-coder → @test-runner | Write & run: unit → integration → E2E |
| 13 | @test-debugger | On failure: diagnose across all layers |
| 14 | @task-manager → Agent | Execute fix (Designer, Data, Developer, etc.) |
| 15 | *Loop to Step 12* | Repeat until all tests pass |
| 16 | @documentation | Final documentation updates |

**Test Debugger Output:** Creates a diagnosis report including:
- Root cause analysis (design flaw, schema issue, code bug, config error)
- Recommended agent to fix (Designer, Data Agent, Developer, Deployment, etc.)
- Specific details for the fixing agent

---

## Project Documentation

### Naming Convention
```
{seq}-{doc type}-{short name}.md
```

### Document Sequence Tracker

| Seq | Short Name | Requirements | Design | Task List | Status |
|-----|------------|--------------|--------|-----------|--------|
| - | - | - | - | - | - |

---

## Key Decisions & Concepts

<!-- Important architectural decisions, patterns, or concepts to remember -->

1. **Bootstrap Build** - 001-dev-agents built manually. Agents don't invoke other agents during this build. Workflow applies to future projects using these agents.
2. **Single Designer Agent** - One Designer agent (not separate design + UML). Outputs `{seq}-design-{short-name}.md` with full UML.
3. **Developer Agent with Convention Files** - One Developer agent that loads language-specific `conventions/{language}.md` files. Simplifies maintenance.
4. **Mid-Task Work Requests** - Agents can request work mid-task. Task Manager queues, prioritizes, resumes. Preserves context.
5. **Schemas as Source of Truth** - Data Agent maintains schemas in `project-docs/schemas/`. All developers reference these.
6. **Test Runner Routing** - App code issues → Designer → Data Agent → Developer chain. Test code issues → Test Coder.
7. **Task Manager as Sole Writer** - Task Manager is the ONLY agent that modifies the task list. Other agents return structured output; Task Manager parses and updates state. Document-only orchestration, no MCP needed.

---

## Available Tools Reference

<!-- Tools available to sub-agents - to be documented as we understand the scope -->

*To be populated during design phase.*

---

## Folder Structure

```
sub-agents/
├── .claude/
│   └── agents/            # Sub-agent definitions
├── Claude.md              # This file - project index and memory
├── conventions/           # Language-specific coding conventions
├── developer-docs/        # Documentation for project contributors
├── user-docs/             # Documentation for users of the agents
└── project-docs/
    ├── adrs/              # Architecture Decision Records
    ├── schemas/           # Data schemas (source of truth)
    └── *.md               # Requirements, designs, task lists
```

---

## Working Principles

- Blunt, honest feedback over false agreement
- Right matters more than feelings
- Keep markdown lean and concise - enough for correct intent, no more
- Document decisions and rationale

---

## Commands

| Command | Meaning |
|---------|---------|
| `initialize` | Reset project: clear README, reset Claude.md to starting state, ask what to build |
| `continue` | Resume current work using task-list to determine next tasks |

---

## Task List Format

Task lists are created by reviewing requirements and design docs. Each task includes:

| Column | Description |
|--------|-------------|
| ID | Sequential task identifier (T001, T002...) |
| Task | Concise task name |
| Deps | Task IDs this depends on (or `-` if none) |
| Refs | Line numbers from requirements (R:) and design (D:) docs |
| Notes | Brief context to assist developer |

Example:
```
| ID | Task | Deps | Refs | Notes |
|----|------|------|------|-------|
| T001 | Create agent base class | - | R:12-15, D:8-20 | Abstract class with execute() method |
| T002 | Implement config loader | T001 | R:18, D:25-30 | YAML parsing for agent settings |
```

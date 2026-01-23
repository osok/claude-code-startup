# Claude-Code Startup

A starter template for building applications with Claude Code using specialized sub-agents for structured development workflows.

## What This Template Does

This template gives you a team of AI agents that work together to build your application. Instead of one AI doing everything, specialized agents handle different aspects of development:

- **Requirements Agent** asks clarifying questions to understand what you want
- **Architect Agent** makes technology and structure decisions
- **Designer Agent** creates detailed designs before coding starts
- **Developer Agent** writes the actual code following best practices
- **Test Agents** plan, write, and run tests to catch bugs
- **Documentation Agent** creates user and developer docs

The **Task Manager** coordinates everything, tracking what's done and what's next.

## What to Expect

### The Workflow

1. **You describe what you want to build** - in plain language
2. **Requirements Agent interviews you** - asks questions to clarify scope, constraints, and priorities
3. **Architect makes decisions** - chooses technologies, defines structure, documents rationale
4. **Designer creates blueprints** - detailed designs with diagrams before any code is written
5. **Developer implements** - writes code following the designs and project conventions
6. **Tests are written and run** - catches bugs early, routes failures to the right agent to fix
7. **Documentation is generated** - user guides and developer docs

### What You Get

- **Structured requirements document** following ISO/IEC/IEEE 29148 standards
- **Architecture Decision Records (ADRs)** explaining why choices were made
- **Design documents** with Mermaid UML diagrams
- **Clean, tested code** following language-specific conventions
- **Comprehensive tests** (unit, integration, E2E)
- **Documentation** for users and developers

### How Long Does It Take?

It depends on complexity. A simple feature might complete in one session. A full application takes multiple sessions - use `continue` to resume where you left off.

## Quick Start

### 1. Create Your Project

**GitHub Web UI:**
1. Click **"Use this template"** → **"Create a new repository"**
2. Name it and create
3. Clone locally

**Or GitHub CLI:**
```bash
gh repo create my-project --template osok/claude-code-startup --clone
cd my-project
```

### 2. Initialize

Open the project in Claude Code and run:

```
initialize
```

This resets the template for your project and asks what you want to build.

### 3. Build

The agents take over from here. They'll ask questions when needed and keep you informed of progress.

To resume work in a new session:

```
continue
```

## Commands

| Command | When to Use |
|---------|-------------|
| `initialize` | Once, right after cloning the template |
| `continue` | To resume work in a new Claude Code session |

## Included Agents

| Agent | What It Does |
|-------|--------------|
| **Requirements** | Interviews you to understand what you want to build |
| **Architect** | Makes technology choices, defines project structure |
| **Designer** | Creates detailed designs with UML diagrams |
| **Task Manager** | Coordinates all agents, tracks progress |
| **Test Designer** | Plans what tests are needed |
| **Data Agent** | Defines database schemas and data structures |
| **Deployment** | Sets up Docker, environment configs, infrastructure |
| **Developer** | Writes application code |
| **Test Coder** | Writes test code |
| **Test Runner** | Runs tests, diagnoses failures |
| **Test Debugger** | Deep debugging across all layers when tests fail |
| **Documentation** | Writes user guides and developer docs |

## Language Support

Pre-built coding and testing conventions for 27 technologies:

**Backend Languages**
- Go, Java, Python, TypeScript, Rust, C#/.NET, Ruby, PHP, Kotlin, Scala, Elixir

**Frontend Frameworks**
- React, Vue, Angular, Svelte, Next.js, Nuxt

**Mobile**
- Swift, Kotlin Android, Flutter/Dart, React Native

**Infrastructure & DevOps**
- Terraform, Kubernetes, Bash/Shell, SQL

**Emerging & Specialized**
- Zig, Solidity

The Developer and Test Coder agents automatically use the right conventions for your tech stack.

## Project Structure

After initialization, your project will have:

```
your-project/
├── .claude/agents/       # Agent definitions (don't modify)
├── Claude.md             # Project memory and status
├── conventions/          # Coding standards by language
├── project-docs/         # Requirements, designs, task lists
│   ├── adrs/             # Architecture decisions
│   └── schemas/          # Data schemas
├── developer-docs/       # Docs for contributors
└── user-docs/            # Docs for end users
```

## How It Works Under the Hood

1. **Document-based coordination** - Agents communicate through markdown files, not complex APIs
2. **Task Manager as orchestrator** - One agent controls the workflow and task list
3. **Schemas as source of truth** - Data Agent maintains schemas that all code references
4. **Smart failure routing** - When tests fail, the system figures out which agent should fix it

## Tips for Best Results

- **Be specific in requirements** - The more detail you provide upfront, the better the output
- **Answer agent questions thoughtfully** - They ask for a reason
- **Review designs before implementation** - Easier to change a design than refactor code
- **Use `continue` liberally** - Sessions can be interrupted; progress is saved

## Related

- [cursor-startup](https://github.com/osok/cursor-startup) - Similar template for Cursor IDE

## License

MIT

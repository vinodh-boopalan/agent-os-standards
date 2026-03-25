# Agent OS Standards

A standards and workflow extension for [Agent OS](https://buildermethods.com/agent-os). Provides team-wide engineering standards organized by tech stack, plus commands that add a structured product-to-architecture pipeline on top of Agent OS's built-in workflow.

Built on top of [Agent OS](https://buildermethods.com/agent-os) by Brian Casel @ [Builder Methods](https://buildermethods.com).

## What is this?

This repo provides two things on top of Agent OS:

1. **Engineering standards as profiles** — Company-wide and stack-specific conventions defined as markdown files. When installed into a project, AI coding agents (Claude Code, Cursor, etc.) automatically follow your team's standards instead of generic defaults.

2. **Workflow commands** — Three commands (`/create-prd`, `/create-adr`, `/update-c4`) that extend Agent OS with a structured requirements-to-architecture pipeline, complete with cross-referencing between documents.

## Profile Structure

```
profiles/
├── tarams/standards/              # Company-wide (inherited by all)
│   ├── code-quality.md            # TS strict, linting, naming conventions
│   ├── git-workflow.md            # Trunk-based dev, conventional commits, PRs
│   ├── testing.md                 # Coverage gates, test patterns
│   ├── cicd.md                    # GitHub Actions, environments, versioning
│   ├── security.md                # Secrets, scanning, auth, OWASP
│   └── architecture.md            # ADRs, C4 model, feature-based structure
│
├── react-native/standards/        # Expo, Router, NativeWind, EAS
├── nextjs/standards/              # App Router, Server Components, Vercel
├── node-api/standards/            # Fastify, Prisma, zod, pino
├── python-django/standards/       # DRF, Poetry, pytest, ruff
└── fullstack/standards/           # Monorepo, shared types, turborepo
```

Each stack profile **inherits** from the base profile, so every project gets company-wide standards plus stack-specific ones.

## Commands

This project adds three commands that extend the Agent OS workflow:

| Command | Description |
|---------|-------------|
| `/create-prd` | Interactive session to capture product requirements — features with IDs, user stories, acceptance criteria, personas, and non-functional requirements. Pulls context from Agent OS product docs (`mission.md`, `roadmap.md`, discovery docs) when available. |
| `/create-adr` | Interactive session to create Architecture Decision Records — auto-numbered, optionally linked to PRD features, with cross-references back to the PRD and specs. Suggests running `/update-c4` when the decision affects architecture. |
| `/update-c4` | Interactive session to create or modify C4 architecture diagrams in Structurizr DSL — add containers, components, relationships, external systems, and views with a full preview before saving. |

### Workflow

These commands fit into the broader Agent OS workflow:

```
/plan-product → /create-prd → /shape-spec → /create-adr → implementation
                     ↑              ↑              ↓
               (this project)  (Agent OS)     /update-c4
```

`/plan-product` and `/shape-spec` are provided by Agent OS. `/create-prd`, `/create-adr`, and `/update-c4` are provided by this project.

All commands can be run standalone at any time.

### Product Documents

The commands read from and write to a standard folder structure inside your project:

```
agent-os/
├── product/                  # Product context
│   ├── mission.md            # Product vision and goals (created by /plan-product)
│   ├── roadmap.md            # Phases and milestones (created by /plan-product)
│   ├── tech-stack.md         # Technology choices (created by /plan-product)
│   └── prd.md                # Product requirements (created by /create-prd)
│
├── discovery/                # Client/stakeholder inputs
│   └── *.md                  # Meeting notes, briefs, research — any docs that
│                             # capture requirements before they're formalized
│
├── architecture/
│   ├── adr/                  # Architecture Decision Records (created by /create-adr)
│   │   ├── 001-*.md
│   │   └── 002-*.md
│   └── workspace.dsl         # C4 diagram in Structurizr DSL (created by /update-c4)
│
└── specs/                    # Implementation specs (created by /shape-spec)
```

**How it flows:**

1. Run `/plan-product` (Agent OS) to establish `mission.md`, `roadmap.md`, and `tech-stack.md`
2. Drop any client briefs, meeting notes, or research into `agent-os/discovery/`
3. Run `/create-prd` — it reads product docs and discovery files to pre-fill requirements
4. Run `/create-adr` — it links decisions back to PRD features
5. Run `/update-c4` — it keeps the architecture diagram in sync with decisions

Steps 1-2 are optional. `/create-prd` works without them but produces better results when product context and discovery docs are available.

## Prerequisites

- [Agent OS](https://buildermethods.com/agent-os) installed at `~/agent-os/`
- An AI coding tool that supports Agent OS (Claude Code, Cursor, etc.)

## Quick Start

```bash
# Clone to ~/agent-os/ (or merge into existing installation)
git clone git@github.com:vinodh-boopalan/agent-os-standards.git ~/agent-os

# Install into a project
cd ~/Code/your-project
~/agent-os/scripts/project-install.sh --profile react-native
```

## Adapting for Your Team

This repo is designed to be forked and customized:

1. **Fork this repo**
2. **Rename the base profile** — Replace `tarams/` with your company name
3. **Update `config.yml`** — Change `default_profile` and `inherits_from` references
4. **Customize standards** — Edit the markdown files to match your team's conventions
5. **Add or remove stack profiles** — Only keep what your team uses
6. **Clone to `~/agent-os/`** on each team member's machine

```yaml
# config.yml — customize for your org
version: 3.0
default_profile: your-company

profiles:
  react-native:
    inherits_from: your-company
  nextjs:
    inherits_from: your-company
  # add your stacks...
```

## Credits

- **Agent OS** created by [Brian Casel](https://buildermethods.com) @ Builder Methods
- Standards profiles maintained by [Tarams](https://tarams.com)

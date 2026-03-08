# Agent OS Standards

Shared engineering standards and AI agent profiles for consistent, high-quality software delivery across teams and tech stacks.

Built on top of [Agent OS](https://buildermethods.com/agent-os) by Brian Casel @ [Builder Methods](https://buildermethods.com).

## What is this?

This repo defines **company-wide engineering standards** as markdown files, organized into **profiles** by tech stack. When paired with Agent OS, these standards are automatically injected into AI coding agents (Claude Code, Cursor, etc.) so they build the way your team builds.

**The result:** Every AI-assisted feature, bug fix, or refactor follows your team's conventions — not generic defaults.

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

## How It Works

1. **Configure** — Set `default_profile` and inheritance in `config.yml`
2. **Install** — Run `project-install.sh --profile <stack>` in any project
3. **Build** — AI agents automatically follow your standards

```bash
# Example: set up a React Native project
cd ~/Code/my-app
~/agent-os/scripts/project-install.sh --profile react-native
# Installs 9 standards files (6 company-wide + 3 React Native)
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

# In your AI tool, run:
# /index-standards   — build the standards index
# /inject-standards  — load standards into agent context
```

## Credits

- **Agent OS** created by [Brian Casel](https://buildermethods.com) @ Builder Methods
- Standards profiles maintained by [Tarams](https://tarams.com)

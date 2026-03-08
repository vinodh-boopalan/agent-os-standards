# Create ADR

Create an Architecture Decision Record through an interactive session. Produces a numbered ADR file in `agent-os/architecture/adr/`.

## Important Guidelines

- **Always use AskUserQuestion tool** when asking the user anything
- **Offer suggestions** — Pre-fill from existing context (PRD, specs) when available
- **Keep it lightweight** — ADRs should be concise and scannable
- **Auto-detect numbering** — Scan existing ADRs and use the next sequential 3-digit number

## Process

### Step 1: Determine Context

**First, find existing ADRs.**

Check `agent-os/architecture/adr/` for existing ADR files. If that folder doesn't exist, check `agent-os/architecture/decisions/`. If neither exists, this will be the first ADR.

List existing ADRs (by number and title) for reference.

**Then, check if a PRD exists.**

Check if `agent-os/product/prd.md` exists. If it does, read it and identify features.

Use AskUserQuestion:

```
[If existing ADRs found:]
Existing ADRs:
- ADR-001: {title}
- ADR-002: {title}
...

[If PRD exists:]
Is this ADR linked to a specific feature?

1. F-001: {Feature Name}
2. F-003: {Feature Name}
...
N. Standalone (not linked to a feature)

(Pick a number)

[If no PRD:]
This will be a standalone ADR (no PRD found).

Ready to proceed? (yes / cancel)
```

### Step 2: Capture Title

Use AskUserQuestion:

```
What's the decision being recorded?

Give a short descriptive title.
Example: "Use Firebase for push notifications"

(Enter the ADR title)
```

### Step 3: Capture Context

If a PRD feature was selected in Step 1, pre-fill context from the feature description.

Use AskUserQuestion:

```
Why is this decision needed? What problem or requirement triggered it?

[If feature-linked: "Based on the PRD feature description:"]
[Pre-filled context from feature]

(Describe the context, or adjust the suggestion above)
```

### Step 4: Capture Decision and Alternatives

Use AskUserQuestion:

```
What was decided, and why?

(Describe the decision)
```

Then use AskUserQuestion:

```
Were any alternatives considered?

Examples:
- "We considered X but rejected it because..."
- "Option A was faster but Option B scales better"
- "none" if no alternatives

(List alternatives, or "none")
```

### Step 5: Capture Consequences

Use AskUserQuestion:

```
What are the consequences of this decision?

Consider:
- Positive outcomes (what this enables)
- Trade-offs (what we're giving up)
- Follow-up actions (what needs to happen next)

(List consequences)
```

### Step 6: Offer C4 Update

Use AskUserQuestion:

```
Does this decision change the system architecture?

Examples of architectural changes:
- Adding a new service or container
- Introducing a new external system dependency
- Changing how components communicate

If yes, I'll suggest running /update-c4 after saving the ADR.

(yes / no)
```

Note the response for Step 9.

### Step 7: Generate ADR File

**Auto-detect the next number:**

1. Scan all files in `agent-os/architecture/adr/` (or `agent-os/architecture/decisions/`)
2. Extract the highest number from filenames matching pattern `NNN-*.md`
3. Next number = highest + 1, zero-padded to 3 digits
4. If no existing ADRs, start at `001`

**Generate the filename:**
```
{NNN}-{kebab-case-title}.md
```

Where kebab-case-title is derived from the title (lowercase, hyphens, no special characters, max 50 chars).

**Create the directory** `agent-os/architecture/adr/` if it doesn't exist.

**Write the ADR file** using this template:

```markdown
# ADR-{NNN}: {Title}

## Status
Accepted

## Context
{context from Step 3}

**Related Feature:** {F-XXX} — {feature name} _(only if feature-linked)_

## Decision
{decision from Step 4}

### Alternatives Considered
{alternatives from Step 4, omit this subsection entirely if "none"}

## Consequences
{consequences from Step 5}
```

### Step 8: Cross-Reference Updates

**If feature-linked (a PRD feature was selected in Step 1):**

1. Read `agent-os/product/prd.md`
2. Find the selected feature entry (by F-XXX ID)
3. Add this line after the existing feature fields:
   ```
   - **ADR:** agent-os/architecture/adr/{NNN}-{slug}.md
   ```
4. Update the "Last updated" date in the PRD

**If a spec exists for this feature:**

1. Check `agent-os/specs/` for folders that reference this feature
2. If a `shape.md` exists in the spec folder, add the ADR reference under an `## Architectural Decisions` section:
   ```markdown
   ## Architectural Decisions
   - [x] ADR-{NNN}: {title} — Accepted
   ```

### Step 9: Confirm

Output a summary:

```
ADR created: agent-os/architecture/adr/{NNN}-{slug}.md

Summary:
- Title: {title}
- Status: Accepted
- Linked to: {F-XXX: feature name | Standalone}
[If cross-references were updated:]
- Updated: agent-os/product/prd.md (added ADR reference to {F-XXX})

[If user said "yes" to C4 update in Step 6:]
This decision involves architectural changes. Run /update-c4 to update the C4 diagram.

[Otherwise:]
Next steps:
- Review the ADR and edit directly if needed
- Run /update-c4 if this affects system architecture
- Run /create-adr again for additional decisions
```

## Tips

- ADRs are immutable once accepted — to change a decision, create a new ADR that supersedes the old one
- Keep ADRs concise — they capture the "why" behind decisions, not implementation details
- Feature-linked ADRs create traceability: PRD → ADR → Spec → Implementation
- The 3-digit numbering convention (001, 002, ...) matches the existing project pattern

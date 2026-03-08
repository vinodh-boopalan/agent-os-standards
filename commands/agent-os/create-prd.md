# Create PRD

Capture product requirements through an interactive session. Produces `agent-os/product/prd.md` with structured features, user personas, and acceptance criteria.

## Important Guidelines

- **Always use AskUserQuestion tool** when asking the user anything
- **One question at a time** — don't overwhelm with multiple questions
- **Keep it lightweight** — capture enough to be useful without over-documenting
- **Pre-fill from existing docs** — use product context and discovery docs to suggest answers

## Process

### Step 1: Check for Existing PRD

Check if `agent-os/product/prd.md` exists.

**If it exists**, read it and use AskUserQuestion:

```
I found an existing PRD with these features:

[List features with IDs and statuses]

Would you like to:
1. Start fresh (replace entire PRD)
2. Add new requirements (append features)
3. Review & update existing requirements
4. Cancel

(Choose 1, 2, 3, or 4)
```

If option 2, skip to Step 6 (feature gathering) and use next sequential ID.
If option 3, present features for editing.
If option 4, stop here.

**If no PRD exists**, proceed to Step 2.

### Step 2: Read Product Context

Check if `agent-os/product/` contains any of these files:
- `mission.md`
- `roadmap.md`
- `tech-stack.md`

If they exist, read them and summarize key points for grounding. These will be used to pre-fill the overview and align features with roadmap phases.

If none exist, use AskUserQuestion:

```
I notice /plan-product hasn't been run yet — there's no mission.md or roadmap.md.

It's recommended to run /plan-product first to establish product vision, but we can proceed without it.

Would you like to:
1. Continue creating the PRD without product docs
2. Cancel (run /plan-product first)

(Choose 1 or 2)
```

### Step 3: Read Discovery Documents

Check if `agent-os/discovery/` exists and contains files (beyond README.md).

**If discovery documents exist**, read all documents in the folder. Summarize key findings:
- Client requirements mentioned
- Features discussed
- Constraints or technical requirements noted
- User personas or target audience mentioned

Use AskUserQuestion:

```
I found these discovery documents:

[List files found]

Key findings:
- [Summarize requirements, features, constraints found]

Should I use these to pre-populate requirements?

1. Yes, extract requirements from discovery docs
2. No, I'll provide requirements manually
3. Use some — let me pick which docs to include

(Choose 1, 2, or 3)
```

**If no discovery folder exists**, skip this step.

### Step 4: Gather Overview

If `mission.md` exists, pre-fill the overview from it.

Use AskUserQuestion:

```
Let's start with the product overview for the PRD.

[If mission.md exists: "Based on your product mission:"]
[Pre-filled overview from mission.md]

Does this capture the product overview correctly, or would you like to adjust it?

[If no mission.md: "Describe the product in 2-3 sentences — what it does and who it's for."]
```

### Step 5: Gather User Personas

If discovery docs mentioned personas or target users, propose them.

Use AskUserQuestion:

```
Who are the key user personas? Keep it brief — just name, role, and primary goal.

[If discovery docs had user info: "Based on discovery documents, I'd suggest:"]
[Pre-filled personas]

Format: Name — Role — Goal
Example: Store Owner — Small business owner — Manage inventory efficiently

(List 1-3 personas, or adjust the suggestions above)
```

### Step 6: Gather Features

Process features one at a time, following a loop pattern.

**If discovery docs were read and user approved extraction**, propose extracted features first:

Use AskUserQuestion:

```
Based on discovery documents, I extracted these potential features:

1. {Feature name} — {brief description}
2. {Feature name} — {brief description}
...

Let's go through them one by one. Starting with:

**{Feature 1 name}**
- Description: {extracted description}
- Suggested user story: As a {persona}, I want {action} so that {benefit}

Does this look right? Adjust the description, user story, or skip this feature.
```

**For each feature** (whether extracted or manually provided):

Use AskUserQuestion for feature name and description:

```
[If first feature and no extraction: "Let's capture features. We'll do one at a time."]
[If continuing: "Next feature."]

Feature name and brief description?
```

After getting the feature, use AskUserQuestion:

```
For **{Feature Name}**, what are the user stories?

Format: As a {persona}, I want {action} so that {benefit}

(List one or more user stories)
```

Then use AskUserQuestion:

```
What are the acceptance criteria for **{Feature Name}**?

These are checkable items that define "done."

(List the criteria)
```

Then use AskUserQuestion:

```
Does **{Feature Name}** have any known architectural implications?

Examples:
- Needs real-time updates (WebSocket, SSE)
- Requires offline storage / sync
- Integrates with a third-party API
- Needs background processing

(Describe implications, or "none")
```

If the user provides implications, add `- **Architectural Notes:** {implications}` to the feature entry in the PRD template.

Then use AskUserQuestion:

```
Got it. **{Feature Name}** captured.

Next feature, or done?

(Describe next feature, or say "done")
```

Assign sequential IDs: F-001, F-002, etc. If adding to existing PRD, continue from the last ID.

Group features by roadmap phase if `roadmap.md` exists and has phases.

### Step 7: Gather Non-Functional Requirements

Use AskUserQuestion:

```
Any non-functional requirements? List what applies:

- **Performance:** Response times, load capacity
- **Security:** Auth, encryption, compliance
- **Scalability:** Expected growth, concurrent users
- **Accessibility:** WCAG level, screen reader support
- **Other:** Anything else

(List requirements, or "none" to skip)
```

### Step 8: Gather Constraints, Assumptions, Out of Scope

Use AskUserQuestion:

```
Three quick items:

1. **Constraints** — Technical, budget, timeline, or regulatory limits?
2. **Assumptions** — What are we assuming to be true?
3. **Out of scope** — What are we explicitly NOT building?

(Answer any or all, or "skip" to leave blank)
```

### Step 9: Generate PRD

Write `agent-os/product/prd.md` using the template below.

If adding to an existing PRD (option 2 from Step 1), append new features with the next sequential ID and update the "Last updated" date.

Add a `## Discovery References` section if discovery documents were used.

**Template:**

```markdown
# Product Requirements Document

_Last updated: YYYY-MM-DD_

## Overview
{Product overview from Step 4}

## User Personas

### {Name}
- **Role:** {role}
- **Goal:** {goal}

## Features

### Phase 1: MVP

#### F-001: {Feature Name}
- **Description:** {brief description}
- **Status:** draft
- **User Stories:**
  - As a {persona}, I want {action} so that {benefit}
- **Acceptance Criteria:**
  - [ ] {criterion}

### Phase 2: Post-Launch

#### F-00N: {Feature Name}
- **Description:** {brief description}
- **Status:** draft
- **User Stories:**
  - As a {persona}, I want {action} so that {benefit}
- **Acceptance Criteria:**
  - [ ] {criterion}

## Non-Functional Requirements
- **Performance:** {or N/A}
- **Security:** {or N/A}
- **Scalability:** {or N/A}
- **Accessibility:** {or N/A}

## Constraints
- {constraint}

## Assumptions
- {assumption}

## Out of Scope
- {item}

## Success Metrics
- {metric}

## Discovery References
- [{document name}](../discovery/{filename})
```

Notes:
- **Feature IDs (F-001)** — Give `/shape-spec` a stable reference
- **Status field** — Track progress: `draft` → `specced` → `in-progress` → `shipped`
- **Phases map to roadmap.md** — Direct correspondence with roadmap phases
- If no roadmap phases exist, put all features under "Phase 1: MVP"

### Step 10: Confirm Completion

After creating the PRD, output:

```
PRD created: agent-os/product/prd.md

Summary:
- {N} personas defined
- {N} features captured (F-001 through F-{NNN})
- Organized into {N} phases

Next steps:
- Review the PRD and edit directly if needed
- Run /shape-spec to pick a feature and create an implementation spec
- Run /create-prd again to add more features later
```

## Tips

- If the user provides brief answers, that's fine — PRDs can be expanded later
- Feature IDs are stable — they don't change when features are reordered
- Status values: `draft` (captured), `specced` (has a /shape-spec), `in-progress` (being built), `shipped` (done)
- Discovery docs are optional — the PRD works without them
- The PRD is a living document — encourage iterating on it

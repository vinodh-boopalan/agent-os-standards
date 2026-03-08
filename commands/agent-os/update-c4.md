# Update C4

Update the C4 architecture diagram (Structurizr DSL) through an interactive session. Reads and modifies `agent-os/architecture/workspace.dsl`.

## Important Guidelines

- **Always use AskUserQuestion tool** when asking the user anything
- **Show before saving** — Always preview the full updated DSL before writing
- **Preserve existing structure** — Only modify what the user requests
- **Minimum views** — The architecture standard requires System Context + Container views at minimum

## Process

### Step 1: Read Current Workspace

Read `agent-os/architecture/workspace.dsl`.

If the file doesn't exist, use AskUserQuestion:

```
No workspace.dsl found in agent-os/architecture/. Would you like to create one from scratch?

I'll need:
- System name and description
- Key users/personas
- Main containers (e.g., mobile app, API, database)

(yes / cancel)
```

If creating from scratch, gather the basics and generate a minimal workspace, then continue to Step 2 for additions.

**If the file exists**, parse and summarize the current architecture:

Use AskUserQuestion:

```
Current C4 architecture:

**Persons:**
- {name} — {description}

**Software Systems:**
- {name} — {description}

**Containers:**
- {name} — {technology} — {description}

**Relationships:**
- {source} → {target}: "{description}"

**Views:**
- {list of defined views}

[If container view is missing:]
⚠️ Note: No container view is defined. The architecture standard requires both System Context and Container views minimum.

What would you like to change?
```

### Step 2: Gather Changes

Use AskUserQuestion:

```
What changes do you want to make?

Options:
1. Add a container (e.g., database, message queue, new service)
2. Add a component within a container
3. Add or modify relationships
4. Add a person or external system
5. Add a missing view (container view, component view)
6. Describe changes in your own words

(Pick one or more, or describe the changes)
```

Based on the user's response, ask follow-up questions as needed:

**For adding a container:**
```
Container details:
- Name?
- Technology? (e.g., "PostgreSQL", "Redis", "Node.js")
- Description? (brief, e.g., "Caches session data")
- Which system does it belong to?
- Relationships? (what talks to it, what does it talk to?)
```

**For adding a relationship:**
```
Relationship details:
- From? (person or container name)
- To? (person or container name)
- Description? (e.g., "Reads/writes data", "Sends notifications")
- Technology? (optional, e.g., "REST API", "gRPC")
```

**For adding a person/external system:**
```
Details:
- Name?
- Description?
- What does it interact with? (relationships)
```

**For adding a view:**
```
What view would you like to add?
- Container view (shows containers within a system)
- Component view (shows components within a container)
- Deployment view (shows deployment infrastructure)

Which system/container should it show?
```

Gather all necessary details before proceeding.

### Step 3: Preview Changes

Generate the full updated `workspace.dsl` content.

Use AskUserQuestion:

```
Here's the updated workspace.dsl:

\`\`\`dsl
{full updated DSL content}
\`\`\`

Changes made:
- {list each change, e.g., "Added container: Redis Cache"}
- {e.g., "Added relationship: Mobile App → Redis Cache"}
- {e.g., "Added container view"}

Save this? (yes / adjust: describe what to change)
```

If the user wants adjustments, make them and preview again.

### Step 4: Save and Suggest Preview

Write the updated content to `agent-os/architecture/workspace.dsl`.

Create the directory `agent-os/architecture/` if it doesn't exist.

Output:

```
Updated: agent-os/architecture/workspace.dsl

Changes saved:
- {list changes}

To preview the diagram locally, run:
docker run -p 8080:8080 -v ./agent-os/architecture:/usr/local/structurizr structurizr/lite

Then open http://localhost:8080 in your browser.

Alternatively, paste the DSL content into https://structurizr.com/dsl to preview online.
```

## Structurizr DSL Reference

Use this as a guide when generating DSL content:

```dsl
workspace "{Name}" {
  model {
    // Persons
    user = person "{Name}" "{Description}"

    // Software Systems
    system = softwareSystem "{Name}" "{Description}" {
      // Containers
      app = container "{Name}" "{Description}" "{Technology}"
      db = container "{Name}" "{Description}" "{Technology}"
    }

    // External Systems
    external = softwareSystem "{Name}" "{Description}" {
      tags "External"
    }

    // Relationships
    user -> system "Uses"
    app -> db "Reads/writes" "SQL"
    system -> external "Sends data to" "REST API"
  }
  views {
    systemContext system "SystemContext" {
      include *
      autoLayout
    }
    container system "Containers" {
      include *
      autoLayout
    }
    // Component views (optional)
    // component app "Components" {
    //   include *
    //   autoLayout
    // }
  }
}
```

## Tips

- Keep the DSL readable — use consistent indentation and comments for clarity
- The architecture standard requires System Context + Container views at minimum
- External systems should be tagged with `"External"` for visual distinction
- Relationship descriptions should be brief action phrases: "Reads/writes", "Sends notifications to"
- Technology labels on relationships help document integration patterns (e.g., "REST API", "WebSocket")
- Run /update-c4 whenever an ADR introduces architectural changes

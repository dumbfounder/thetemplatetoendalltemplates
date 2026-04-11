# TEMPLATE_PLATFORM_PLAN.md

This file captures the current plan for turning the feature-template idea into a real platform that can pick and choose best-of-breed features to build applications.

## Goal

Turn the template system from a loose documentation setup into a **template composition platform** that can:

- discover relevant project and feature templates
- score them for the current task
- choose the best combination
- compose them into an implementation plan
- build the thinnest working version
- write improvements back into the template library

## Core idea

Each feature template should become a **structured capability unit**.

That means each template should describe:

- when to use it
- what it depends on
- what it pairs well with
- what it conflicts with
- what files it creates
- what env vars it needs
- how to verify it
- what other templates it can build on

The platform then does 4 things:

1. discover candidate templates
2. score them for the current project
3. compose the best set
4. write back improvements after implementation

## Canonical repository

Template-platform work should live in and be committed to:

- `git@github.com:dumbfounder/thetemplatetoendalltemplates.git`

Anything primarily about:
- feature templates
- project templates
- template manifests
- template registry
- template composition
- template selection/scoring
- template-platform prompts/drivers

should be treated as belonging to that repository.

When this work is moved into that repo, keep it as the canonical source of truth.

## What already exists

These files already exist in the workspace:

- `/Users/dumbfounder/Dropbox/codex apps/templates/NEW_PROJECT_TEMPLATE.md`
- `/Users/dumbfounder/Dropbox/codex apps/templates/FEATURE_TEMPLATE_FORMAT.md`
- `/Users/dumbfounder/Dropbox/codex apps/templates/TEMPLATE_SYSTEM_PROMPT.md`
- `/Users/dumbfounder/Dropbox/codex apps/templates/FEATURE_TEMPLATE_DRIVER.md`
- `/Users/dumbfounder/Dropbox/codex apps/templates/feature-templates/_template.md`

These form the documentation/instruction layer.

## Single-file template strategy

The default template unit should be one markdown file per template.

Preferred shape:

```text
/Users/dumbfounder/Dropbox/codex apps/templates/feature-templates/
  <slug>.md
```

Why:
- easier sharing
- easier copy/paste into chats and prompts
- lower friction for reuse
- simpler versioning
- fewer sidecar files to drift out of sync

If deeper research or examples are needed, embed them in an appendix section inside the same file by default.

## What is needed to make it a platform

### 1. Standard template format

Keep the human-readable markdown format.

This is the durable reusable explanation layer.

Current required sections are:

- Summary
- Use When
- Inputs
- Defaults
- Chris Preferences Applied
- Best Patterns
- Avoid
- Build Order
- Env
- Ports
- Files To Create
- Starter Commands
- Verification
- Variants
- Reuse From Other Templates
- Notes
- Appendix (Optional)

### 2. Machine-readable manifest per template

Add a `template.json` next to each markdown template if and when the platform layer truly needs it.

Purpose:
- make templates queryable
- support scoring/composition logic
- let the system choose templates without relying only on prose

Example shape:

```json
{
  "name": "google-oauth-auth",
  "type": "feature",
  "file": "feature-templates/google-oauth-auth.md",
  "useWhen": ["google login", "auth", "user accounts"],
  "stack": ["nextjs", "react", "node"],
  "dependsOn": [],
  "pairsWellWith": ["admin-dashboard", "audit-log"],
  "conflictsWith": ["clerk-auth"],
  "inputs": ["GOOGLE_CLIENT_ID", "GOOGLE_CLIENT_SECRET"],
  "creates": ["auth routes", "session config", "login ui"],
  "verification": ["sign in works", "session persists"],
  "scoreHints": {
    "speed": 9,
    "reuse": 8,
    "complexity": 3
  }
}
```

### 3. Registry

Add a central registry to index all templates.

Suggested path:

`/Users/dumbfounder/Dropbox/codex apps/templates/templates/registry/index.json`

Example:

```json
{
  "templates": [
    "feature-templates/google-oauth-auth.md",
    "feature-templates/chat-ui.md",
    "feature-templates/admin-dashboard.md"
  ]
}
```

Purpose:
- one place to enumerate templates
- easier scanning for a selector/composer
- enables future automation

### 4. Selector / composer layer

Need a prompt, script, or agent workflow that:

- reads all template manifests
- matches them to the application or feature request
- ranks by relevance, speed, compatibility, and proof
- chooses a primary template
- adds supporting templates
- rejects conflicting templates
- outputs a build plan

This is what makes the system behave like a platform instead of a note pile.

### 5. Automatic template harvesting

After a feature works well, saying things like:

- create template
- update template
- turn this into a template

should trigger:

- creation or update of `<slug>.md`
- creation or update of `template.json` if manifests are in play
- linking to dependencies and related templates
- capture of reusable defaults, verification, anti-patterns, and embedded research appendix

## Platform loop

### Input

Example:

> Build me an app with chat, auth, and admin tools.

### Platform behavior

1. Find matching templates
   - chat-ui
   - openai-api
   - google-oauth-auth
   - admin-dashboard
   - audit-log

2. Score them
   - fastest
   - most reusable
   - best verified
   - fewest dependencies
   - compatible stack

3. Compose them
   - primary app starter
   - auth layer
   - chat layer
   - admin layer
   - logging layer

4. Generate implementation plan
   - file structure
   - env vars
   - ports
   - startup commands
   - verification steps

5. Build

6. Write back improvements

## Best-of-breed scoring model

Each template should be scored on:

- relevance
- speed to MVP
- real-world proof
- verification quality
- port/env discipline
- modern defaults
- compatibility with chosen stack
- composability with other templates
- single-file portability

Suggested weighted formula:

- relevance: 35%
- speed: 20%
- compatibility: 20%
- verification: 10%
- reuse quality: 10%
- modern defaults: 5%

## What makes it a platform instead of docs

Need these 3 layers:

### Layer 1: Template library

Current `/Users/dumbfounder/Dropbox/codex apps/templates/feature-templates/` plus future project templates.

### Layer 2: Composition engine

A selector/composer prompt or script that can choose and merge templates.

### Layer 3: Feedback / writeback

Every successful build improves the template library.

That combination is the platform.

## Suggested future directory structure

```text
templates/
  FEATURE_TEMPLATE_DRIVER.md
  FEATURE_TEMPLATE_FORMAT.md
  registry/
    index.json
  feature-templates/
    _template.md
    google-oauth-auth.md
    chat-ui.md
    admin-dashboard.md
```

## Future build prompt shape

Suggested prompt once the platform exists:

```text
Use ./templates/FEATURE_TEMPLATE_DRIVER.md.

Read the registry and all relevant templates.
Choose the best-of-breed combination for this application.
Prefer the fastest verified compatible patterns.
Compose the selected templates into one implementation plan.
Then build the thinnest working version and update the templates with any improvements.

Application:
```

## Honest current state

Right now this system is:
- a strong documentation and workflow layer
- a good starting template system
- not yet a full composition platform

To become a real platform, the next concrete additions should be:

1. `template.json` schema
2. `registry/index.json`
3. first selector/composer prompt or script
4. first real set of populated feature manifests/templates

## Best next actions

1. define the `template.json` schema
2. create `/Users/dumbfounder/Dropbox/codex apps/templates/templates/registry/index.json`
3. add 5-10 real feature templates with manifests or consistent markdown metadata
4. create the selector/composer prompt
5. test composition on a real app request

## Notes

The intended long-term behavior is:
- drop the platform files into any project
- tell the agent to use the driver file
- let it discover all available templates
- let it choose best-of-breed building blocks
- let it compose them into the fastest working implementation
- let successful work continuously improve the template library

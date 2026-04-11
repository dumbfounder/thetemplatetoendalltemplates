# The Template To End All Templates

This repo is the template library and instruction set for template-driven project and feature work.

The current local working-copy path is:

```text
/Users/dumbfounder/Dropbox/codex apps/templates
```

If you are using this repo from another checkout, replace that root path in the prompts below with your own absolute repo path.

## What Is Here

### Core instruction files

- `TEMPLATE_SYSTEM_PROMPT.md`
  - Base controlling workflow for template-driven project and feature work.
- `NEW_PROJECT_TEMPLATE.md`
  - Default build behavior for new projects.
- `FEATURE_TEMPLATE_FORMAT.md`
  - Exact required format for reusable feature templates.
- `FEATURE_TEMPLATE_DRIVER.md`
  - Controlling workflow for creating or iterating feature templates.
- `TEMPLATE_PLATFORM_PLAN.md`
  - Platform-level plan for turning the template library into a composition system.

### Active feature templates

- `feature-templates/_template.md`
  - Base blank template file.
- `feature-templates/2wayvoice.md`
  - Mobile-first embedded two-way voice interface for a live app.
- `feature-templates/mobile-design-best-practices.md`
  - Reusable mobile UX and mobile-first product design framework.
- `feature-templates/openai-realtime-voice-web.md`
  - Mountable browser voice feature using OpenAI Realtime over WebRTC.
- `feature-templates/unread-first-email-voice-assistant.md`
  - Unread-first mobile email assistant with voice control and recent-history fallback.

### Legacy backups

- `feature-templates/_legacy-multifile-backups/`
  - Historical multi-file template layouts kept for reference during migration to single-file templates.

## Exact Usage

### 1. Use the system for a new project

Use this prompt as-is:

```text
Use these files as the controlling instructions for this new project:

- /Users/dumbfounder/Dropbox/codex apps/templates/TEMPLATE_SYSTEM_PROMPT.md
- /Users/dumbfounder/Dropbox/codex apps/templates/NEW_PROJECT_TEMPLATE.md
- /Users/dumbfounder/Dropbox/codex apps/templates/FEATURE_TEMPLATE_FORMAT.md

Also scan:
- /Users/dumbfounder/Dropbox/codex apps/templates/feature-templates/

Task:
Build this project using the template system. Scan existing templates and sibling repos, choose the best-of-breed patterns, build the thinnest working end-to-end slice first, keep model selection env-driven, reuse working nearby config before asking, and always run local servers on a free unused port.
```

### 2. Apply one feature template to another project as a one-off

Use this prompt shape:

```text
Apply this feature template to the current project as a one-off implementation pass:

Template:
- /Users/dumbfounder/Dropbox/codex apps/templates/feature-templates/<template-file>.md

Also use these base files:
- /Users/dumbfounder/Dropbox/codex apps/templates/TEMPLATE_SYSTEM_PROMPT.md
- /Users/dumbfounder/Dropbox/codex apps/templates/NEW_PROJECT_TEMPLATE.md

Task:
Audit the current project against the template, identify the highest-leverage gaps, implement the thinnest high-impact changes first, and verify the main happy path. Do not create or update a reusable template unless I explicitly ask.
```

Example for mobile design:

```text
Apply this feature template to the current project as a one-off implementation pass:

Template:
- /Users/dumbfounder/Dropbox/codex apps/templates/feature-templates/mobile-design-best-practices.md

Also use these base files:
- /Users/dumbfounder/Dropbox/codex apps/templates/TEMPLATE_SYSTEM_PROMPT.md
- /Users/dumbfounder/Dropbox/codex apps/templates/NEW_PROJECT_TEMPLATE.md

Task:
Audit the current app against the mobile design template, identify the top mobile UX issues, implement the highest-leverage fixes first, and verify the main mobile flows. Do not create or update any reusable template unless I explicitly ask.
```

### 3. Create a new feature template from another project

Use this prompt as-is and replace the source path:

```text
Add a new feature template to the template library by extracting it from another project.

Source project:
- /ABSOLUTE/PATH/TO/THE/OTHER/PROJECT

Template system files to use:
- /Users/dumbfounder/Dropbox/codex apps/templates/FEATURE_TEMPLATE_DRIVER.md
- /Users/dumbfounder/Dropbox/codex apps/templates/FEATURE_TEMPLATE_FORMAT.md
- /Users/dumbfounder/Dropbox/codex apps/templates/TEMPLATE_SYSTEM_PROMPT.md
- /Users/dumbfounder/Dropbox/codex apps/templates/NEW_PROJECT_TEMPLATE.md

Template library destination:
- /Users/dumbfounder/Dropbox/codex apps/templates/feature-templates/

Task:
Scan the source project, identify a reusable feature worth extracting, and turn it into a new single-file feature template in /Users/dumbfounder/Dropbox/codex apps/templates/feature-templates/<slug>.md.

Instructions:
- treat /Users/dumbfounder/Dropbox/codex apps/templates/FEATURE_TEMPLATE_DRIVER.md as the controlling workflow
- follow the exact section order required by /Users/dumbfounder/Dropbox/codex apps/templates/FEATURE_TEMPLATE_FORMAT.md
- scan existing templates in /Users/dumbfounder/Dropbox/codex apps/templates/feature-templates/ and reference related ones in "Reuse From Other Templates"
- inspect the source project for the real implementation, env patterns, startup commands, ports, file structure, verification steps, and anti-patterns
- extract only durable reusable knowledge, not project-specific noise
- keep the result as one self-contained markdown file
```

### 4. Iterate or improve an existing feature template

Use this prompt:

```text
We are creating a feature template. Use these files:

- /Users/dumbfounder/Dropbox/codex apps/templates/FEATURE_TEMPLATE_DRIVER.md
- /Users/dumbfounder/Dropbox/codex apps/templates/FEATURE_TEMPLATE_FORMAT.md
- /Users/dumbfounder/Dropbox/codex apps/templates/NEW_PROJECT_TEMPLATE.md
- /Users/dumbfounder/Dropbox/codex apps/templates/TEMPLATE_SYSTEM_PROMPT.md

Scan:
- /Users/dumbfounder/Dropbox/codex apps/templates/feature-templates/
- sibling repos one level up
- the current implementation

Task:
Improve the matching feature implementation and update its template in the same pass. Refresh Defaults, Chris Preferences Applied, Best Patterns, Avoid, Build Order, Env, Ports, Files To Create, Starter Commands, Verification, Variants, Reuse From Other Templates, Notes, and Appendix if needed.
```

### 5. Use the base blank template directly

If you already know the feature and just want the skeleton:

```text
Use /Users/dumbfounder/Dropbox/codex apps/templates/feature-templates/_template.md as the base and create a new feature template at /Users/dumbfounder/Dropbox/codex apps/templates/feature-templates/<slug>.md. Follow /Users/dumbfounder/Dropbox/codex apps/templates/FEATURE_TEMPLATE_FORMAT.md exactly and fill it with durable reusable implementation guidance only.
```

## Which File To Use

- Use `TEMPLATE_SYSTEM_PROMPT.md` when you want the whole template-driven workflow to control the task.
- Use `NEW_PROJECT_TEMPLATE.md` when the task is a new app or project build.
- Use `FEATURE_TEMPLATE_FORMAT.md` when the main task is writing a template file in the standard section order.
- Use `FEATURE_TEMPLATE_DRIVER.md` when creating, extracting, or iterating a feature template.
- Use a file in `feature-templates/` when you want to apply a specific reusable feature pattern to a project.

## Operating Rules Embedded In These Templates

- Scan sibling repos and the parent directory before asking for config.
- Reuse working env names, startup scripts, and proven patterns before inventing new ones.
- Prefer the thinnest working end-to-end slice first.
- Keep model selection env-driven.
- Default to the latest strong OpenAI model unless a task needs something else.
- Always use a free unused port.
- Write durable wins back into templates when the task is template creation or template iteration.

## Repo Goal

This repo is intended to become the canonical home for:

- feature templates
- project templates
- template manifests
- template registry
- template selection and composition logic
- template-system prompts and drivers

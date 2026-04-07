# TEMPLATE_SYSTEM_PROMPT.md

Use this file as the single base instruction for template-driven project and feature work.

If Chris says **"use this file"**, treat this document as the controlling workflow.

## Mission

When creating or modifying a project or feature:

- determine which templates apply
- scan for existing templates and sibling-project implementations
- choose the best-of-breed patterns
- merge them into the thinnest working implementation
- avoid making Chris restate standing preferences

## Core behavior

Be scrappy.

Reuse what already works before inventing new setup.

Assume the best clues usually live:
- one level up
- in sibling repos
- in existing feature templates
- in project env files, startup scripts, prompts, and prior working implementations

## Source priority order

When deciding how to build something, use sources in this order:

1. the file Chris explicitly tells you to use
2. `NEW_PROJECT_TEMPLATE.md`
3. `FEATURE_TEMPLATE_FORMAT.md`
4. `feature-templates/`
5. sibling repos one level up
6. current repo implementation patterns
7. ask Chris only if the above are insufficient

## Standing preferences

Always apply these unless Chris says otherwise:

- optimize for fastest safe iteration
- build the thinnest working end-to-end slice first
- look one level up before asking for missing config
- scan sibling repos for working env files, prompts, scripts, and feature patterns
- reuse discovered working keys/config where appropriate
- use latest strong OpenAI model by default
- keep model selection env-driven
- always start local servers on a free unused port
- prefer minimal dependencies and minimal ceremony
- prefer direct readable code over premature abstraction
- verify the happy path quickly
- write back durable wins into templates

## Template discovery workflow

When given a new request:

1. Identify whether the request is:
   - a full project
   - a feature
   - a refinement of an existing feature

2. Scan these locations:
   - `feature-templates/`
   - parent directory / one level up
   - sibling repos nearby

3. Look for evidence in:
   - `template.md`
   - `README.md`
   - `AGENTS.md`
   - `.env.example`
   - `.env*`
   - startup scripts
   - prompts
   - reusable components or feature folders

4. Match candidate templates by:
   - similar feature goal
   - similar stack
   - similar external integration
   - similar auth/data/deploy pattern
   - evidence of successful real-world use

## Best-of-breed selection rules

If multiple templates or sibling implementations overlap, score them by:

1. fastest path to running code
2. working env/config reuse
3. free-port startup behavior
4. latest-model / modern defaults
5. minimal dependencies
6. clear build order
7. real verification steps
8. evidence of successful use in a real project

Prefer proven simple patterns over theoretically elegant ones.

## Merge workflow

After identifying candidate templates:

1. Choose a primary template.
2. Pull supporting patterns from other templates.
3. Merge:
   - best defaults
   - best startup commands
   - best env conventions
   - best verification steps
   - best reusable file structure
4. Remove duplicate or conflicting patterns.
5. Produce the smallest coherent implementation that can run now.

## Build workflow

Default order:

1. inspect templates and sibling repos
2. pick best-of-breed patterns
3. scaffold quickly
4. wire env/config
5. start on a free port
6. verify boot
7. implement happy path
8. re-test
9. summarize briefly
10. write back reusable lessons

## Port rule

Never assume the default port is free.

Use:
- frontend: first open port from 3000+
- backend/API: first open port from 4000+
- workers/devtools: first open port from 5000+ or 6000+

Always state the chosen port clearly.

## Env/key rule

Before asking for keys or config:

1. inspect sibling repos and parent directory
2. look for working env names and config patterns
3. reuse discovered conventions
4. if a working key/config is already available locally, use it appropriately
5. do not expose secrets in summaries

## OpenAI rule

If OpenAI is involved:

- use the user-provided or discovered working key
- default to the latest strong model
- keep model selection in env/config
- expose the model in one obvious place
- avoid stale hardcoded model names unless compatibility requires them

## Output style

Be brief and operational.

When reporting progress, include:
- what was chosen
- what templates/patterns were reused
- where it runs
- which port it chose
- what still needs doing

Do not write long essays unless asked.

## Writeback rule

After a successful build or feature implementation:

1. identify the reusable winning pattern
2. update an existing template or create a new one
3. keep only durable reusable knowledge
4. update:
   - Best Patterns
   - Avoid
   - Build Order
   - Verification
   - Reuse From Other Templates

If Chris says any version of:
- "create template"
- "turn this into a template"
- "make this a feature template"
- "save this as a template"

then automatically:

1. create a new folder in `feature-templates/<slug>/`
2. create `template.md` in the standard format from `FEATURE_TEMPLATE_FORMAT.md`
3. extract the best reusable defaults, build order, env shape, ports, verification, and anti-patterns from the feature
4. link it to related templates in `Reuse From Other Templates`
5. keep only the reusable durable pattern, not project-specific noise

## Fallback behavior

If no good template exists:

1. use `feature-templates/_template/template.md`
2. apply the standing preferences in this file
3. build the feature
4. turn the result into a new reusable template

## One-line operating instruction

> Scan templates and sibling repos first, pick the best proven patterns, reuse working config, start on a free port, build the thinnest working slice, and write the winning pattern back into the template system.

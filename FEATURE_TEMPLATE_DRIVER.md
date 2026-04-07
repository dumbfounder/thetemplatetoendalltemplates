# FEATURE_TEMPLATE_DRIVER.md

Use this file when Chris says:

- "we are creating a feature template"
- "use this file to create a feature template"
- "use this file to iterate a feature template"

This file is the controlling workflow for creating, improving, and maintaining reusable feature templates.

## Mission

Create feature templates that:
- follow one common format
- can reference every other feature template
- can build on top of one another
- get updated automatically as the implementation improves
- preserve Chris preferences without Chris repeating them

## Base files to always use

Read and follow these first:

1. `FEATURE_TEMPLATE_DRIVER.md`
2. `FEATURE_TEMPLATE_FORMAT.md`
3. `NEW_PROJECT_TEMPLATE.md`
4. `TEMPLATE_SYSTEM_PROMPT.md`

Then scan:
- `feature-templates/`
- sibling repos one level up
- the current project implementation

## Operating mode

When in feature-template mode, do not treat the feature as a one-off build.
Treat it as:
1. a reusable system component
2. a future building block for other templates
3. a living template that should improve as the feature improves

## Core rules

- Be scrappy.
- Reuse what already works.
- Look one level up first.
- Scan sibling repos before asking for missing config.
- Reuse discovered working env patterns, prompts, startup commands, and feature structures.
- Default to the latest strong model when OpenAI is involved.
- Always use a free unused port.
- Build the thinnest working slice first.
- Keep the template compact and reusable.

## Template creation rule

When Chris says a feature is being turned into a template:

1. create or update `feature-templates/<slug>/template.md`
2. use the exact required format from `FEATURE_TEMPLATE_FORMAT.md`
3. optionally add:
   - `references/`
   - `assets/`
   - `prompts/`
   if they improve reuse materially

## Template iteration rule

When iterating on a feature that already has a template:

Automatically update that template as part of the work.

Always review and refresh these sections when the feature improves:
- `Defaults`
- `Chris Preferences Applied`
- `Best Patterns`
- `Avoid`
- `Build Order`
- `Env`
- `Ports`
- `Files To Create`
- `Starter Commands`
- `Verification`
- `Variants`
- `Reuse From Other Templates`
- `Notes`

Do not wait for Chris to separately ask for the template update if the work clearly improved the reusable pattern.

## Cross-template rule

Every feature template must be able to reference and build on every other relevant feature template.

That means every time you create or update a template, you must:

1. scan `feature-templates/`
2. identify related templates
3. explicitly note useful dependencies in `Reuse From Other Templates`
4. borrow proven patterns from related templates when they improve the current one
5. keep the current template composable with the others

Examples:
- auth template can reference admin dashboard and audit log templates
- chat UI template can reference streaming API and OpenAI config templates
- ingestion template can reference worker template and admin monitoring template

## Best-of-breed composition rule

When multiple templates could help:

1. identify all relevant templates
2. compare their:
   - Defaults
   - Best Patterns
   - Avoid
   - Build Order
   - Verification
3. take the strongest parts from each
4. merge them into a coherent implementation
5. write any new winning merged pattern back into the current template

## Automatic update triggers

If Chris says any variant of:
- "iterate this"
- "improve this"
- "make it better"
- "refactor this"
- "use this file"
- "we are creating a feature template"

and a matching feature template already exists, then:
- update the feature implementation
- update the template in the same pass

## Template quality bar

A good feature template should make future builds faster by clearly encoding:
- when to use it
- what defaults to pick
- what files to create
- how to boot fast
- how to verify quickly
- what to avoid
- what other templates it builds on

## Discovery order

When starting template work, scan in this order:

1. existing template for this feature
2. related templates in `feature-templates/`
3. sibling repos one level up
4. current repo implementation
5. ask Chris only if still blocked

## Required output behavior

When finishing a template-creation or template-iteration task, report briefly:
- which template was created or updated
- which related templates were referenced
- what best-of-breed patterns were incorporated
- what changed in the implementation
- where it runs / which port was used if relevant

## One-line instruction

> We are creating a feature template. Use this file, scan all existing feature templates plus sibling repos, build with best-of-breed patterns, and automatically update the template as the feature evolves.

# FEATURE_TEMPLATE_FORMAT.md

Use this as the **standard format** for reusable project and feature templates.

Goal: when creating something new, the agent should be able to scan existing templates, compare them, pick the best pieces, and assemble a fast MVP without Chris re-explaining the same preferences.

## Design goals

- Be easy for an agent to scan quickly.
- Make strong patterns reusable across projects.
- Support **best-of-breed composition** across multiple prior features.
- Keep the format short, structured, and consistent.
- Optimize for **fast iteration**, not documentation theater.

## Rules

- One feature template = one folder.
- Each feature template must contain a `template.md` file at minimum.
- Prefer a small amount of structured metadata plus a few opinionated sections.
- Keep prose tight.
- Include only implementation knowledge that improves future execution speed.
- Anything primarily about this template system should ultimately be committed to: `git@github.com:dumbfounder/thetemplatetoendalltemplates.git`

## Directory format

```text
feature-templates/
  <template-slug>/
    template.md
    assets/             # optional starter code / boilerplate / UI pieces
    references/         # optional detailed notes, API quirks, examples
    prompts/            # optional reusable agent prompts
```

## Naming

Use short hyphenated names.

Examples:
- `openai-chat-ui`
- `auth-google-oauth`
- `stripe-subscriptions`
- `background-worker`
- `admin-dashboard`
- `rag-document-ingestion`

## Required file: template.md

Every template must follow this exact section order.

```markdown
# <Template Name>

## Summary
<2-5 lines: what this template does and when to reuse it>

## Use When
- <trigger>
- <trigger>
- <trigger>

## Inputs
- <required input>
- <required input>

## Defaults
- stack: <preferred stack>
- model: <preferred latest model / env-driven>
- port: <port strategy>
- auth: <default auth choice>
- data: <default data/storage choice>

## Chris Preferences Applied
- <standing preference>
- <standing preference>
- <standing preference>

## Best Patterns
- <pattern name>: <short explanation>
- <pattern name>: <short explanation>

## Avoid
- <mistake / anti-pattern>
- <mistake / anti-pattern>

## Build Order
1. <step>
2. <step>
3. <step>

## Env
```env
KEY=value
```

## Ports
- preferred: <range or rule>
- fallback: <rule>

## Files To Create
- <path>
- <path>
- <path>

## Starter Commands
```bash
<commands>
```

## Verification
- <smoke check>
- <smoke check>

## Variants
- <variant>: <when to use>
- <variant>: <when to use>

## Reuse From Other Templates
- <template slug>: <what to borrow>
- <template slug>: <what to borrow>

## Notes
- <sharp edge>
- <sharp edge>
```
```

## Section guidance

### Summary
Say what the template is for in plain language.

### Use When
This is the routing section. Make it obvious when the template applies.

### Inputs
List the real decisions or inputs needed from the user or neighboring repos.

### Defaults
Capture the preferred defaults so the agent does not reinvent them.

Required defaults to think about every time:
- stack
- model
- port strategy
- auth
- storage/data layer
- deploy shape

### Chris Preferences Applied
This is mandatory.

Use it to encode standing preferences like:
- look one level up first
- search sibling repos for working env files and keys
- use discovered working config before asking
- use latest strong OpenAI model by default
- start servers on an unused port
- be scrappy
- prefer thin end-to-end slices

### Best Patterns
List the few patterns worth stealing later.

Examples:
- env-driven model config
- split web/worker process
- resumable transcript model
- boring deployable DB-backed ingestion
- app-level whitelist on top of provider auth

### Avoid
Explicit anti-patterns speed up future work.

Examples:
- hardcoding old model names
- binding blindly to port 3000
- placeholder fake env values when working keys already exist nearby
- over-abstracting v1

### Build Order
The exact preferred order to build this feature.

### Env
Show only the env vars that matter.

### Ports
Always declare the port rule.

Preferred default:
- frontend: first open from 3000+
- backend/API: first open from 4000+
- worker/devtools: first open from 5000+/6000+

### Files To Create
List the minimum file skeleton.

### Starter Commands
The shortest commands to get the feature running.

### Verification
State the actual smoke test.

### Variants
Capture common forks without bloating the main template.

### Reuse From Other Templates
This is the key section for best-of-breed composition.

When writing a template, explicitly say which other templates are worth borrowing from and why.

## Best-of-breed merge algorithm

When creating a new project or feature:

1. Scan all nearby templates.
2. Pick primary templates whose `Use When` matches.
3. Compare `Best Patterns` across them.
4. Pull the best defaults from each template.
5. Preserve Chris-wide preferences from every applicable template.
6. Build the thinnest combined working version first.
7. After success, write back any new winning pattern into the relevant template.

## Template scoring rubric

When multiple templates overlap, prefer the one with:

1. fastest path to running code
2. real verification steps
3. clean env handling
4. free-port startup behavior
5. reusable defaults
6. fewer unnecessary dependencies
7. evidence it handled a real project successfully

## Project template vs feature template

Use the same format for both.

Difference:
- **Project template** = whole app starter
- **Feature template** = reusable slice inside an app

Examples of project templates:
- `nextjs-openai-saas-starter`
- `worker-backed-ingestion-app`

Examples of feature templates:
- `google-oauth-auth`
- `chat-streaming-ui`
- `admin-audit-log`
- `document-rag-pipeline`

## Writeback rule

After building something successfully:

- decide whether it belongs as a new template or an improvement to an existing one
- extract only the durable reusable pattern
- update `Best Patterns`, `Avoid`, `Build Order`, and `Verification`
- keep templates compact

If Chris says "create template" or equivalent after a feature is built, convert that feature into a new template automatically using this format.

## Default instruction for future builds

> Before starting a new project or feature, scan the feature templates directory plus sibling repos one level up. Match relevant templates, merge the best patterns, reuse working env/config from nearby projects, use the latest strong model by default, start on a free port, and ship the thinnest working version first.

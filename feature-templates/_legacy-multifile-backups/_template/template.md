# Template Name

## Summary
Short description of what this template does and when it should be reused.

## Use When
- You need this feature pattern in a new or existing project.
- The same setup keeps recurring across repos.
- You want to steal proven defaults instead of rethinking everything.

## Inputs
- user goal
- nearby sibling repos / parent directory
- available env vars / discovered working keys

## Defaults
- stack: choose the fastest sensible stack for the job
- model: latest strong OpenAI model via env
- port: choose first open port in the appropriate range
- auth: reuse existing working auth pattern if applicable
- data: simplest deployable storage that works

## Chris Preferences Applied
- look one level up first
- search sibling repos for working env files and config
- use discovered working keys before asking
- use latest strong model by default
- start on a free unused port
- be scrappy
- build the thinnest end-to-end slice first

## Best Patterns
- env-driven config: keep all runtime choices obvious and overridable
- free-port startup: never assume defaults are open
- nearby-repo reuse: steal what already works

## Avoid
- asking for config before checking nearby repos
- hardcoding stale model names
- blindly using port 3000
- overengineering v1

## Build Order
1. inspect sibling repos / parent directory
2. identify reusable patterns, env names, and startup scripts
3. scaffold the thinnest working version
4. wire env/config
5. boot on a free port
6. verify the happy path
7. capture reusable lessons back into templates

## Env
```env
OPENAI_API_KEY=
OPENAI_MODEL=
```

## Ports
- preferred: frontend first open from 3000+, backend first open from 4000+
- fallback: scan upward until a free port is found

## Files To Create
- README.md
- .env.example
- app entrypoint
- config file

## Starter Commands
```bash
npm install
npm run dev
```

## Verification
- app boots without errors
- main happy path works end to end
- chosen port is printed clearly

## Variants
- project template: use for whole-app starters
- feature template: use for reusable slices inside apps

## Reuse From Other Templates
- none yet: add links to stronger templates as they appear

## Notes
- keep this file compact
- optimize for future agent reuse, not human ceremony

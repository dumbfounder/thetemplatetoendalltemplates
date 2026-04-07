# NEW_PROJECT_TEMPLATE.md

Use this template by default when creating new projects for Chris.

## Core rule

Optimize for **fastest safe iteration**.
Do not make Chris restate the same operating preferences every time.

## Default operating assumptions

- Prefer **shipping a working MVP fast** over designing a perfect architecture.
- Be **scrappy and resourceful**. Reuse what already exists before inventing new setup.
- Use the **API key / secrets the user provides**, not placeholders once real credentials are available.
- If the user did not paste the key in the current chat, **look for working keys/config in nearby sibling projects first**.
- Treat the **parent directory / one level up** as the first place to look, because that is where Chris usually keeps related projects.
- Reuse proven env names, setup patterns, scripts, and service config from neighboring repos when that speeds things up safely.
- Use the **latest strong OpenAI model available by default** unless the user explicitly asks for a different model, cheaper model, or local model.
- Keep setup and dependencies minimal.
- Prefer tools, frameworks, and patterns that reduce iteration time.
- Avoid overengineering, premature abstraction, and speculative infra.
- Make the app easy to run, restart, inspect, and modify.

## Project startup checklist

When starting a new project:

1. **Create the app skeleton quickly**
   - Pick the fastest sensible stack for the task.
   - Prefer boring defaults that are well supported.

2. **Set up environment config immediately**
   - Add `.env.example`.
   - Add `.env.local` / `.env` guidance.
   - Wire in the real env vars the user mentions.
   - Before asking for credentials, inspect nearby sibling projects for existing working env files, key names, and config patterns.
   - Look **one directory up first**, then sibling repos nearby.
   - Reuse existing keys/config only for the local build context; do not dump secrets into summaries.
   - If OpenAI is involved, assume:
     - `OPENAI_API_KEY`
     - latest capable model as default

3. **Run the dev server on an unused port**
   - Never assume the default port is free.
   - Check for an open port and start there.
   - Print the chosen port clearly.
   - If restarting, avoid conflicting with already-running local services.

4. **Make the project runnable immediately**
   - Install deps.
   - Start dev mode.
   - Verify the main page / endpoint loads.
   - Fix boot errors before doing anything fancy.

5. **Tighten the feedback loop**
   - Enable hot reload / watch mode.
   - Add a minimal smoke test when useful.
   - Keep logs readable.
   - Keep commands short and obvious.

6. **Document only what helps iteration**
   - How to run
   - Which env vars matter
   - Which port it picked
   - How to test the main flow
   - Skip essay-length docs unless asked

## Coding rules for fast iteration

- Start with the **thinnest working end-to-end slice**.
- Build the happy path first.
- Use mock data only until real integration is available; then switch to the real integration quickly.
- Keep files organized, but do not waste time on elaborate structure too early.
- Prefer direct readable code over clever abstractions.
- Add comments only where future iteration speed benefits.
- Avoid giant refactors during initial build.
- If something is uncertain, choose the option that gets to a testable result fastest.

## OpenAI defaults

When a project uses OpenAI:

- Use the **user-provided API key**.
- If no key was pasted in the current request, **search nearby projects for an existing working OpenAI key/config first**.
- Check parent/sibling project env files before falling back to placeholders.
- Default to the **latest capable production model**.
- Keep model selection configurable via env vars.
- Expose model config in one obvious place.
- Do not hardcode old model names unless required for compatibility.

Suggested env pattern:

```env
OPENAI_API_KEY=
OPENAI_MODEL=
```

And in code:
- `OPENAI_MODEL` should default to the latest strong model available at build time.
- If the user specifies a model, prefer that.

## Port management rule

Always choose a free port before starting local servers.

Preferred behavior:

- Try the framework default first only if free.
- Otherwise scan upward to find the next free port.
- Tell the user exactly which port is being used.
- If multiple services are needed, assign each a distinct open port.

Example policy:

- frontend: first free from 3000+
- backend: first free from 4000+
- storybook/dev tools: first free from 6000+

## Deliverable shape for new projects

By default, a new project should include:

- runnable app
- env example
- clear startup command
- free-port startup behavior
- real API wiring if credentials are available
- minimal README
- basic smoke verification

## What not to do

- Don’t ask Chris to repeat standing preferences.
- Don’t leave the app half-wired if real keys/config already exist nearby.
- Don’t ignore sibling repos when they likely contain the working env setup.
- Don’t bind blindly to a port that may already be taken.
- Don’t default to stale models when a newer one is available.
- Don’t spend early cycles on deep architecture astronautics.
- Don’t produce lots of ceremony before the first working version.

## Default response style when building

Be action-oriented.

Good:
- what I built
- where it runs
- which port it chose
- what env vars are needed
- next highest-leverage step

Bad:
- long motivational filler
- excessive caveats before trying the obvious path
- asking unnecessary setup questions too early

## Standard build sequence

For most new app requests, follow this order:

1. scaffold
2. install
3. env wire-up
4. start on free port
5. verify boot
6. implement main feature
7. re-test
8. summarize briefly

## Short instruction block to reuse

Use this when delegating or starting a build:

> Build the thinnest working version first. Be scrappy. Look one level up and through sibling projects for working env files, API keys, scripts, and setup patterns before asking me for anything. Use the provided or discovered working API keys, default to the latest model, start every local server on a free unused port, and tell me the port. Keep setup minimal, make it runnable immediately, and optimize for fast iteration over perfect architecture.

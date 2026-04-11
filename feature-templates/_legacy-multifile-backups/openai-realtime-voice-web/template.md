# OpenAI Realtime Voice Web

## Summary
Reusable browser voice feature for OpenAI Realtime over WebRTC.
Use it when a project needs a drop-in voice route with one-click connect, hands-free conversation, push-to-talk fallback, and a lightweight Node mount point instead of a full custom voice stack.

## Use When
- You need ChatGPT-style browser voice interaction inside an existing Node or Express app.
- You want a reusable voice feature that mounts under a route like `/voice/` instead of a separate app.
- You want a low-latency OpenAI Realtime implementation with live transcript and session diagnostics.

## Inputs
- mount path for the feature, such as `/voice`
- server-side `OPENAI_API_KEY`
- preferred default voice and instructions
- host app port or preferred free-port starting point

## Defaults
- stack: Express mountable feature plus vanilla browser JS and WebRTC
- model: `gpt-realtime` via env
- port: feature mounts inside an existing app; demo host starts at the first open port from `3011+`
- auth: none at the feature layer; rely on the host app if gating is needed
- data: no persistent storage; keep transcript and state in memory
- deploy: same Node process as the host app

## Chris Preferences Applied
- look one level up first for working env patterns and keys
- use discovered working OpenAI config before asking
- keep model selection env-driven and current
- use a free unused port for the demo host
- be scrappy and prefer the thinnest end-to-end slice
- make the feature runnable immediately and easy to transplant

## Best Patterns
- mountable router feature: package the server endpoint and static UI together so another app can drop the folder in and mount it quickly
- relative client paths plus trailing-slash redirect: keep the UI working under nested routes like `/voice/` instead of assuming root
- env-driven realtime session config: keep model, voice, instructions, and API key overridable in one obvious place
- dual interaction modes: ship hands-free VAD by default and push-to-talk as a built-in fallback
- demo-host wrapper: keep a tiny standalone host so the feature can be verified in isolation before integration

## Avoid
- root-relative asset and API paths that break when the feature is mounted under a sub-route
- exposing the OpenAI API key to the browser
- hardcoding stale or non-realtime model names
- forcing a separate microservice when the host app can mount the feature directly
- over-abstracting the first reusable version

## Build Order
1. Extract the voice UI and Realtime broker into a single feature folder.
2. Export a mount function for the host Express app.
3. Make client assets and API calls route-relative so nested mounts work.
4. Add a tiny standalone host that uses a free port and demonstrates the mount pattern.
5. Verify config loading, route mounting, and Realtime session creation.
6. Write back the reusable defaults and anti-patterns into the feature template.

## Env
```env
OPENAI_API_KEY=
OPENAI_REALTIME_MODEL=gpt-realtime
OPENAI_REALTIME_VOICE=marin
OPENAI_REALTIME_INSTRUCTIONS="You are a concise, natural voice assistant."
VOICE_FEATURE_MOUNT_PATH=/voice
PORT=3011
```

## Ports
- preferred: mount inside an existing app route; for standalone verification use the first open port from `3011+`
- fallback: scan upward until a free port is found

## Files To Create
- `features/openai-realtime-voice-web/index.mjs`
- `features/openai-realtime-voice-web/public/index.html`
- `features/openai-realtime-voice-web/public/styles.css`
- `features/openai-realtime-voice-web/public/app.js`
- host server or route mount file
- `.env.example`

## Starter Commands
```bash
npm install
npm run dev
```

## Verification
- open the printed URL and confirm the root route lands on the feature entry path
- hit `GET ./api/config` and verify `hasApiKey`, mount path, model, and port are correct
- start a session in the browser and confirm microphone access, remote audio, and transcript updates
- verify push-to-talk still works after mounting under a non-root route

## Variants
- root-mounted feature: use when the host app is only the voice experience
- nested route feature: use when adding voice to a larger app like `/voice/`
- gated feature route: put host-app auth in front of the mount when access should be restricted

## Reuse From Other Templates
- `_template`: reuse the base rules for env-driven config, free-port startup, nearby-repo discovery, and thin end-to-end slices

## Notes
- Redirect the bare mount path to the trailing-slash entry path or relative assets will resolve incorrectly.
- OpenAI Realtime voice selection is effectively locked after the first emitted audio in a session.
- Keep this feature framework-light unless a host app already requires a heavier UI stack.

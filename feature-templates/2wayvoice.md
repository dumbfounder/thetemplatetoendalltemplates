# 2-Way Voice

## Summary
Reusable feature template for a mobile-first two-way voice surface embedded inside an existing web app.
Use it when the user should tap one big button, start talking immediately, hear a short spoken brief, and control real app state through voice without getting trapped in a generic chat UI.

## Use When
- You need live browser voice conversation inside an existing product, not a separate voice-only app.
- The app already has meaningful state, actions, and context that should drive the conversation.
- You want OpenAI Realtime over WebRTC with very short responses and low-latency turn handling.
- The feature must work well on mobile, including PWA-style full-screen behavior and safe-area constraints.
- You need voice to trigger real app actions through tools, not just answer questions.

## Inputs
- host app auth/session model
- live context source the assistant should know about at all times
- set of allowed voice actions and which ones require explicit confirmation
- opening brief content and voice tone
- fallback route for older context or server-side search
- whether the feature is read-only, action-enabled, or send-enabled

## Defaults
- stack: Next.js App Router, React client sheet, authenticated server routes, OpenAI Realtime over WebRTC
- model: `gpt-realtime` via env for live voice; server-side model stays env-driven for heavier fallback tasks
- port: embedded in the main app on the first open port from `3000+`
- auth: reuse the host app session; do not add separate voice auth
- data: bounded transcript in client memory, live context from app state, server-side fallback routes for history or heavier retrieval
- deploy: same web app process as the host product, with server-side OpenAI credentials

## Chris Preferences Applied
- make voice start from one obvious button and get into talk mode immediately
- keep answers extremely short, direct, and summary-first
- do not let the assistant fill silence with politeness or chatter
- keep the mic lifecycle explicit: close means close, disconnect means disconnect
- keep dangerous actions explicit and never infer them from vague wording
- make the mobile UI simple enough that the primary state is obvious at a glance
- keep model and voice selection env-driven and current

## Best Patterns
- full-screen voice sheet: use a fixed overlay with safe-area padding, backdrop blur, and one dominant live-state surface instead of a small modal
- auto-start session flow: opening the voice sheet should request config, connect the session, and start listening without an extra setup screen
- one-sentence opening brief: start with a concise spoken brief generated from current app context, then stop and listen
- bounded conversation state: keep only the last handful of visible turns and a slightly larger bounded in-memory transcript so the UI stays legible and the client stays cheap
- live `session.update` context: rebuild instructions from current app state and push them into the Realtime session whenever context changes
- tool-first action model: expose real app actions as tools and keep model instructions tightly aligned with those tools
- direct client intercepts: catch critical commands like `disconnect` on the client from user transcript events instead of waiting for the model to behave perfectly
- explicit action gating: treat commands like `send`, `mark as read`, or destructive operations as opt-in language patterns, not intent guesses
- spoken exact-line helper: use a dedicated helper for fixed phrases like the opening brief, idle prompt, and disconnect acknowledgement
- echo suppression window: ignore user transcripts that substantially overlap with the assistant’s just-spoken output
- idle prompt then shutdown: after idle time, ask `Anything else?`, then disconnect automatically if the user stays silent
- live state refresh while open: poll or stream the latest app state while the voice surface is open so the assistant stays current mid-conversation

## Avoid
- making voice a generic assistant that does not know the host app context
- keeping the mic active after the sheet closes or after a disconnect command
- relying on the model alone to enforce action safety
- waiting on expensive provider refreshes before every spoken answer
- stuffing full raw app state or giant transcripts into every prompt update
- exposing the OpenAI API key to the browser
- making the voice UI settings-heavy above the fold on mobile
- asking the user clarifying questions when the host app state already answers them

## Build Order
1. Add a server-authenticated config route that returns model, default voice, available voices, and whether the API key is present.
2. Add a server-authenticated WebRTC session route that exchanges the SDP offer for a Realtime call using server-side credentials.
3. Build the client voice sheet with a single primary `Talk to me` / `Stop talking` control and a hard `X` close path.
4. Create the session lifecycle: config fetch, mic acquisition, `RTCPeerConnection`, data channel, remote audio playback, and teardown.
5. Build the host-context instruction generator and wire it into `session.update`.
6. Define tools for real actions and add concise tool-specific response instructions.
7. Add event handling for speech start/stop, transcript updates, tool calls, assistant output, and errors.
8. Add client-side intercepts for disconnect and any other safety-critical commands.
9. Add echo suppression, idle prompt/disconnect timers, and bounded transcript storage.
10. Refresh host state while the sheet is open and push live context changes into the active session.
11. Add fallback search or server-side retrieval for questions the current context cannot answer.
12. Verify the mobile happy path end to end before polishing secondary controls.

## Env
```env
OPENAI_API_KEY=
OPENAI_REALTIME_MODEL=gpt-realtime
OPENAI_REALTIME_VOICE=marin
OPENAI_REALTIME_INSTRUCTIONS="You are a concise English voice assistant for this app. Keep answers short. Do not fill silence. Do not switch languages."
```

## Ports
- preferred: embed the feature in the main app on the first open port from `3000+`
- fallback: scan upward until a free port is found

## Files To Create
- `src/components/voice-assistant-sheet.tsx`
- `src/lib/realtime-voice.ts`
- `src/app/api/voice/realtime/config/route.ts`
- `src/app/api/voice/realtime/session/route.ts`
- `src/app/api/voice/history/route.ts`
- host app state refresh hook or effect
- host app action routes for any voice-triggered mutations

## Starter Commands
```bash
npm install
npm run dev
```

## Verification
- Tap the primary voice CTA and confirm the sheet opens and starts the voice session without extra setup steps.
- Confirm the assistant opens with one short spoken brief and then listens.
- Ask a simple app-context question and confirm the answer is short, grounded, and not chatty.
- Trigger a real tool action and confirm the result is reflected in both the UI and the spoken response.
- Say `disconnect` or `hang up` and confirm the mic closes immediately.
- Tap the `X` and confirm the mic closes immediately.
- Stay silent and confirm the assistant says `Anything else?` after the idle threshold, then shuts off if the user remains silent.
- Speak while assistant audio is active and confirm the client does not treat the assistant’s own speech as user input.
- Change underlying app state while voice is open and confirm the active session gets fresh context without restarting the conversation.
- Confirm all OpenAI credentials remain server-side.

## Variants
- embedded workspace assistant: use when the user is already inside a stateful product view and voice is a faster control layer
- read-only voice layer: use when voice can summarize and navigate but must not mutate app state
- action-enabled voice layer: use when voice can perform safe bounded mutations through tools
- push-to-talk fallback: add when hands-free VAD is unreliable in the target environment

## Reuse From Other Templates
- `openai-realtime-voice-web`: reuse the basic WebRTC Realtime session wiring and server-side session exchange
- `mobile-design-best-practices`: reuse the phone-first hierarchy, one-obvious-action rule, and safe-area/mobile state discipline
- `unread-first-email-voice-assistant`: reuse the live-context refresh, concise voice prompt style, action gating, and fallback search patterns for stateful assistants
- `_template`: reuse the base template structure and portability rules

## Notes
- Use `semantic_vad` with low eagerness by default when you want the assistant to avoid hyperactive turn-taking.
- Keep `interrupt_response` off unless interruption is a deliberate product choice.
- Mono audio with echo cancellation, noise suppression, and auto gain control is a good default for mobile browser sessions.
- Keep the first screen about talking, not settings. Voice/model selectors belong in secondary controls.
- Treat close, disconnect, and stop-listening as client responsibilities, not model aspirations.
- If the app has live state updates, refresh or stream them while voice is open; otherwise the assistant will feel stale mid-session.

## Appendix (Optional)
- Durable extraction from the PulseMail implementation:
  - voice surface is a full-screen overlay with safe-area padding and a single dominant live-state card
  - the primary control flips between `Talk to me` and `Stop talking`
  - the opening brief is spoken with an exact-line helper instead of relying on the model to improvise
  - visible conversation is trimmed to recent turns instead of becoming a chat transcript dump
  - client-side echo suppression uses a short time window plus transcript overlap against the last assistant utterance
  - disconnect is handled from user transcript events directly, not only through a model tool call
  - while the sheet is open, the host app refreshes state on a short interval so the voice session can absorb new context
  - when current context is insufficient, the assistant should say it is checking older context, then use a server route for grounded retrieval instead of guessing

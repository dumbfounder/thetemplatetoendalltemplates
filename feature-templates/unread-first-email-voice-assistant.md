# Unread-First Email Voice Assistant

## Summary
Reusable feature template for a mobile-first email assistant where voice is a fast control surface over an unread queue.
Use it when the product should brief the user on what matters, read specific emails aloud, revise drafts, and search recent mailbox history without turning into a chatty general-purpose bot.

## Use When
- You want an email app where the primary workflow is triaging unread mail, not browsing the whole mailbox.
- You need OpenAI Realtime voice for quick spoken commands like `what's up`, `read the one from Bobbie`, `mark as read`, or `disconnect`.
- You want server-side mailbox sync and indexing, with the client only handling UI state and the live voice session.
- You want a mobile-friendly voice experience with very short answers and aggressive silence handling.

## Inputs
- mail providers to support: IMAP, Gmail API, optional POP for read-only fetch
- unread queue window: max unread count and date lookback
- recent-history window for fallback search
- whether reply drafting and sending are enabled now or later
- deployment target and persistent storage path

## Defaults
- stack: Next.js App Router with TypeScript, server routes, React client voice sheet, OpenAI Realtime over WebRTC
- model: `gpt-realtime` for live voice, stronger server model via env for draft/rewrite or analysis tasks
- port: single web app on the first open port from `3000+`
- auth: mailbox login is the only login; persist mailbox-backed session server-side
- data: per-user server storage plus SQLite FTS for the recent-history index
- deploy: single web service with a persistent disk for sessions, mailbox state, and the history DB

## Chris Preferences Applied
- keep the product unread-first and hide the archive-like complexity
- default to concise voice responses with no filler and no polite throat-clearing
- do mailbox sync and indexing server-side, not on every client refresh
- keep mobile interaction absurdly simple and thumb-friendly
- use live working mailbox context before falling back to older history
- make state-changing actions explicit, never inferred from a vague spoken request
- persist everything that should survive mobile PWA restarts

## Best Patterns
- unread queue as primary context: treat unread mail as the product, and only reach for older history when the queue cannot answer the question
- server-side mailbox loop: fetch and classify mail on the server, then let clients consume already-processed state
- inbox-plus-sent history index: index recent inbox mail and recent sent replies so the assistant can tell whether you already responded
- SQLite FTS prefilter: use a local full-text index for fast history retrieval before any model call
- live session context refresh: rebuild Realtime session instructions from the current unread queue instead of stuffing every update into the transcript
- silent mailbox deltas: new mail should update context immediately, but only speak up when the new item is urgent enough to matter
- explicit action gating: only allow `mark as read`, `mark all as read`, or `send` when the spoken command is unambiguous
- voice idle lifecycle: after 15 seconds of silence say `Anything else?`, then disconnect 5 seconds later if the user stays silent

## Avoid
- letting the voice assistant mark mail read just because the user asked to hear it
- making the voice route wait on mailbox refresh before answering
- using LLMs to determine simple reply evidence when sent-folder heuristics can do it deterministically
- forcing a second auth layer on top of mailbox login
- overloading the transcript with full message bodies or full queue snapshots
- chatty assistant behavior that talks to fill silence
- client-side sync banners that suggest the phone is doing all the work

## Build Order
1. Build mailbox login and per-user persistent server state.
2. Sync only unread mail into the main queue, with configurable lookback and fetch cap.
3. Build a separate recent-history ingestion path for inbox plus sent mail over the last 7 days.
4. Add deterministic reply evidence from sent mail using thread match first, then subject-plus-recipient fallback.
5. Create the mobile unread queue UI with fast card actions and a lightweight detail view.
6. Add the Realtime voice sheet with auto-start, one-sentence opening brief, and compact tools.
7. Refresh live voice context from the unread queue and apply silent mailbox updates during an active session.
8. Add recent-history fallback for voice questions that cannot be answered from the current queue.
9. Add draft/rewrite/send hooks, still keeping read/send actions explicit.
10. Add debug timings and index stats so slow or broken history retrieval is visible immediately.

## Env
```env
OPENAI_API_KEY=
OPENAI_REALTIME_MODEL=gpt-realtime
OPENAI_REALTIME_VOICE=marin
OPENAI_RESPONSE_MODEL=gpt-5.4
MAIL_HISTORY_RETENTION_DAYS=7
MAIL_UNREAD_FETCH_LIMIT=50
MAIL_MIN_AGE_MINUTES=2
MAIL_SYNC_INTERVAL_MINUTES=2
MAIL_APP_DATA_DIR=/var/data
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
```

## Ports
- preferred: run the full app on the first open port from `3000+`
- fallback: keep scanning upward until a free port is found; never assume `3000` is available

## Files To Create
- `src/components/voice-assistant-sheet.tsx`
- `src/app/api/voice/realtime/config/route.ts`
- `src/app/api/voice/realtime/session/route.ts`
- `src/app/api/voice/history/route.ts`
- `src/app/api/messages/[id]/voice/route.ts`
- `src/lib/email-history.ts`
- `src/lib/sync-service.ts`
- `src/lib/imap.ts`
- `src/lib/gmail.ts`
- `src/lib/store.ts`
- `src/app/debug/page.tsx`

## Starter Commands
```bash
npm install
npm run dev
```

## Verification
- Sign in with a real mailbox and confirm the app lands on the unread queue without showing setup noise after refresh.
- Open voice and confirm it immediately speaks a one-sentence brief like `You have 6 unread. Top priority is Wells Fargo and Bobbie.`
- Ask `what's up`, `what's the latest priority`, and `read the one from <sender>` and confirm the answers are short and grounded in the unread queue.
- Ask about something outside the queue and confirm the assistant says `I need to check older email, one second.` before using recent history.
- Ask for something missing and confirm the answer is `Nothing found in the past week.`
- Confirm the assistant says when an email already appears to have a sent reply.
- Say `disconnect` or `hang up` and confirm the mic closes immediately.
- Leave the session idle and confirm it says `Anything else?` after 15 seconds, then shuts off 5 seconds later.
- While voice is open, inject new unread mail and confirm the queue updates immediately without restarting the conversation.

## Variants
- IMAP-first mailbox assistant: use when raw mailbox credentials are the main auth path
- Gmail hybrid assistant: use Gmail API for mailbox fetch and send, while keeping the same unread-first voice UX
- read-only assistant: use when voice can brief, summarize, and search history but should not draft or send

## Reuse From Other Templates
- `openai-realtime-voice-web`: reuse the WebRTC session setup, browser audio handling, and low-latency voice loop
- `mobile-design-best-practices`: reuse the mobile-first simplification rules and high-signal layout discipline
- `_template`: reuse the surrounding template structure and env/port defaults

## Notes
- Default history lookback should be 7 days, not 24 hours.
- Recent-history retrieval should read from the warm server index first; provider refresh belongs in the background, not on the blocking voice path.
- The assistant should prefer one or two short sentences max and should not ask a follow-up question unless it is actually blocked.
- If the user says `read it`, that means open or read aloud, not mark as read.
- Recent reply evidence should be passed into the voice prompt and current email context every time.

## Appendix (Optional)
- Good default assistant behavior:
  - open with a one-sentence queue brief
  - answer tersely
  - stay quiet after answering
  - only speak on live updates when the new email is meaningfully urgent
- Good fallback phrases:
  - `I need to check older email, one second.`
  - `Nothing found in the past week.`
  - `You already replied to that one.`
  - `Disconnecting.`

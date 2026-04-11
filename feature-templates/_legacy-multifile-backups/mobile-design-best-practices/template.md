# Mobile Design Best Practices

## Summary
Use this template when designing a mobile app, mobile-first web app, or phone-centric feature that must work under real mobile constraints: small screens, one-handed use, interruptions, low patience, and uneven network conditions.
This template is not about visual style trends. It is a reusable decision framework for making mobile products feel clear, tappable, fast, accessible, and native-feeling.
It is built from recurring guidance across Apple HIG, Material Design, NN/g mobile navigation research, W3C/WCAG accessibility principles, and broader mobile UX research.

## Use When
- You are creating a new phone-first product or feature.
- You are adapting an existing desktop flow for mobile and want to avoid “shrunk desktop” design.
- You need a strong first-pass checklist for mobile UX before implementation begins.
- You want product, design, and engineering aligned on core mobile principles.
- You need a reusable standard for evaluating whether a mobile design is actually good.

## Inputs
- primary user goal and top 1-3 tasks
- core context of use: on the go, distracted, one-handed, poor signal, bright light, short session, etc.
- target platform: iOS, Android, cross-platform native, PWA, or responsive web
- device scope: phone only, phone + tablet, phone + desktop
- risk level: casual, commerce, health, finance, communication, enterprise workflow, etc.
- user constraints: accessibility needs, language length, age range, connectivity, authentication burden
- product shape: utility, marketplace, content, chat, social, workflow, media, checkout, onboarding, etc.

## Defaults
- stack: mobile-first design system using platform conventions before custom UI invention
- model: none required unless generating research notes or UX copy; if used, keep model env-driven
- port: frontend first open from 3000+, prototypes/docs from 6000+
- auth: lowest-friction secure path appropriate to risk; prefer session continuity, autofill, passkeys, biometrics, or magic links when suitable
- data: optimistic local state, explicit saved state, and resilient sync/error recovery for unstable conditions

## Chris Preferences Applied
- build from the thinnest end-to-end user journey first
- optimize for fast comprehension, not design theater
- make mobile constraints shape the design from the start
- prefer familiar platform patterns over clever novelty
- use explicit hierarchy and obvious actions
- keep accessibility and performance in the first pass
- preserve only durable reusable guidance, not generic UX platitudes

## Best Patterns
- task-first flow design: identify the top job and remove everything that does not help complete it
- one obvious primary action: each screen should make the next step unmistakable
- ruthless content prioritization: small screens demand fewer choices and less simultaneous information
- strong information scent: labels, navigation names, and action language should tell users what happens next
- visible or hybrid navigation when possible: expose core destinations instead of hiding everything behind a menu
- visually salient hidden navigation when necessary: if using a menu, label it, separate it from branding, and make it look tappable
- thumb-friendly ergonomics: place key actions where real users can reach and tap reliably
- forgiving tap zones: size and spacing should tolerate imperfect fingers and imperfect attention
- progressive disclosure: reveal depth only after the primary decision is made
- input minimization: prefer defaults, autofill, pickers, remembered state, camera, voice, and biometrics over typing
- resumable flows: preserve progress, drafts, carts, and form state across interruptions and failures
- explicit system feedback: loading, saving, success, failure, and offline states should always be legible
- accessibility-first mobile UI: readable text, contrast, labels, focus states, semantic structure, and zoom/reflow resilience
- performance as trust: fast startup, stable layout, and responsive interactions are core UX, not implementation detail
- platform-aware adaptation: mobile-first does not mean mobile-only; adapt for larger screens without porting mobile compromises blindly

## Avoid
- compressing a desktop layout into a narrow viewport without rethinking priorities
- multiple competing CTAs on one screen
- tiny touch targets or clusters of adjacent actions with no breathing room
- unlabeled hamburger menus for critical navigation
- deep navigation stacks for common tasks
- gesture-only interactions without visible affordances or fallback UI
- long forms, repeated typing, and fragile input handling
- asking for permissions before the user understands the value exchange
- modal overload that blocks progress for secondary choices
- relying on perfect connectivity, perfect attention, or two-handed use
- inaccessible contrast, ambiguous icons, tiny text, or hidden focus state
- heavy animation or decorative complexity that slows comprehension
- blindly reusing mobile navigation/search patterns on desktop or tablet where they hurt discoverability

## Build Order
1. define the top mobile jobs-to-be-done and success criteria
2. describe the real mobile context: when, where, how, and under what constraints the feature is used
3. map the shortest complete journey from entry to successful outcome
4. rank all content and controls by importance; remove or defer anything nonessential
5. sketch the phone layout first with one obvious primary action per screen
6. choose platform-consistent navigation and interaction patterns
7. simplify onboarding, auth, permissions, and forms to minimize user effort
8. verify touch ergonomics, visual hierarchy, text readability, and affordance clarity
9. add loading, empty, error, offline, retry, and resumed-session states
10. test on small screens under realistic conditions, then adapt upward for tablet/desktop without copying mobile compromises
11. capture reusable decisions into docs/design system/template

## Env
```env
# Usually none required for this template.
# Optional if generating design research or UX copy artifacts with AI:
OPENAI_API_KEY=
OPENAI_MODEL=
```

## Ports
- preferred: app/prototype first open from 3000+, design docs/storybook from 6000+
- fallback: scan upward until a free port is found

## Files To Create
- docs/mobile-design-principles.md
- docs/mobile-context-of-use.md
- docs/mobile-user-flows.md
- docs/mobile-content-priority.md
- docs/mobile-navigation-decisions.md
- docs/mobile-input-friction-checklist.md
- docs/mobile-accessibility-checklist.md
- docs/mobile-state-handling.md
- designs/mobile-wireframes.fig or equivalent export

## Starter Commands
```bash
mkdir -p docs
printf "# Mobile Design Principles\n" > docs/mobile-design-principles.md
printf "# Mobile Context of Use\n" > docs/mobile-context-of-use.md
printf "# Mobile User Flows\n" > docs/mobile-user-flows.md
printf "# Mobile Navigation Decisions\n" > docs/mobile-navigation-decisions.md
printf "# Mobile Input Friction Checklist\n" > docs/mobile-input-friction-checklist.md
printf "# Mobile Accessibility Checklist\n" > docs/mobile-accessibility-checklist.md
printf "# Mobile State Handling\n" > docs/mobile-state-handling.md
```

## Verification
- the primary user task can be completed quickly on a small phone with one hand
- each screen has one obvious primary action
- core navigation is easy to discover and does not depend on guesswork
- important controls are easy to tap without accidental errors
- text remains readable in realistic conditions without zooming
- forms minimize typing, preserve entered data, and handle validation inline
- loading, empty, error, offline, retry, and success states are calm and explicit
- the experience remains understandable with assistive technologies and at high zoom/reflow
- the design feels native to the platform instead of custom for the sake of custom
- larger breakpoints do not inherit mobile compromises that hurt usability

## Variants
- consumer utility app: prioritize speed, clarity, and low-friction repeat actions
- commerce / checkout flow: emphasize trust, autofill, payment speed, address handling, and error recovery
- social / content app: optimize scan rhythm, creation friction, notification boundaries, and return-to-context
- messaging / communication app: focus on draft persistence, attachment ergonomics, timestamps, search, and interruption recovery
- enterprise / workflow app: prioritize predictable layout, search/filter utility, resumability, and low cognitive load under repetition
- onboarding / activation flow: aggressively reduce steps, delay permissions until value is clear, and prove usefulness before setup asks

## Reuse From Other Templates
- _template: base section structure and reusable template discipline
- openai-realtime-voice-web: borrow only if voice is a core interaction mode and mobile input reduction benefits from speech

## Notes
- This template is intentionally opinionated: clarity beats novelty, discoverability beats cleverness, and task completion beats visual flourish.
- Strong source themes: Apple HIG for platform feel and native expectations, Material for systems and adaptation thinking, NN/g for evidence on discoverability and navigation tradeoffs, IxDF for mobile context/task framing, W3C/WCAG for accessibility baselines.
- The recurring meta-rule: remove steps, reduce choices, preserve progress, and make the next action obvious.
- Mobile-first is good. Mobile-only thinking is not. Optimize for phone constraints without exporting those compromises to larger screens blindly.

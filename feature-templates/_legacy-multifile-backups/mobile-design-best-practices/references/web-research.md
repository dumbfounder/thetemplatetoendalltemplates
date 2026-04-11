# Mobile Design Best Practices — Deep Research Notes

This note captures the source sweep used to build and sharpen the `mobile-design-best-practices` template.

## Research approach

Goal: extract durable mobile design principles that hold across product categories, not one-off dribbble advice.

I prioritized:
- platform guidance from Apple and Google
- usability research from NN/g
- accessibility guidance from W3C / WCAG
- broader mobile UX synthesis from IxDF
- practical form and commerce considerations where fetchable

## Sources reviewed

### Platform guidance
- Apple Human Interface Guidelines  
  https://developer.apple.com/design/human-interface-guidelines
- Material Design 3  
  https://m3.material.io/
- Material Design — Applying layout / window size classes  
  https://m3.material.io/foundations/layout/applying-layout/window-size-classes
- Android core app quality / platform quality guidance  
  https://developer.android.com/docs/quality-guidelines/core-app-quality

### Usability research
- Nielsen Norman Group — Mobile First Is NOT Mobile Only  
  https://www.nngroup.com/articles/mobile-first-not-mobile-only/
- Nielsen Norman Group — How to Make Navigation (Even a Hamburger) Discoverable on Mobile  
  https://www.nngroup.com/articles/find-navigation-mobile-even-hamburger/

### Mobile UX synthesis
- Interaction Design Foundation — What is Mobile User Experience (UX) Design?  
  https://www.interaction-design.org/literature/topics/mobile-ux-design

### Accessibility guidance
- W3C WAI Mobile Accessibility Overview  
  https://www.w3.org/WAI/mobile/
- WCAG 2.2 understanding docs considered as anchor guidance for touch targets, focus visibility, and reflow  
  https://www.w3.org/WAI/WCAG22/

### Form / mobile-commerce angle
- Baymard mobile form usability article path was attempted but fetch quality was poor; retained as a domain/source family for future manual expansion  
  https://baymard.com/blog/mobile-form-usability

## What kept repeating across sources

## 1) Mobile context is fundamentally different from desktop context
This is the big one.

Across IxDF, Apple, Material, and NN/g, the recurring truth is: mobile is not just smaller. Users are distracted, interrupted, moving, one-handed, bandwidth-constrained, and impatient.

Implication for the template:
- design for short sessions
- prioritize top tasks hard
- assume interruptions and resumability matter
- reduce steps and memory burden

## 2) Task-first beats layout-first
A lot of weak mobile design starts with visual adaptation rather than job adaptation.

IxDF strongly reinforces task-oriented design. The template now pushes:
- identify the top 1–3 jobs first
- map the thinnest success path
- make every screen support one obvious next move

## 3) Information hierarchy must get ruthless on phones
Smaller viewports mean less room for ambiguity.

Repeated themes:
- minimize content
- use strong hierarchy
- keep one primary action per screen
- defer secondary detail
- reduce cognitive load

This is why the template leans hard on:
- one-primary-action guidance
- content priority docs
- visual dominance for the next step

## 4) Navigation should be shallow, discoverable, and visibly tappable
NN/g’s navigation material is some of the clearest non-hand-wavy evidence here.

Key takeaways:
- hidden nav hurts discoverability
- if nav must be hidden, make it visually salient
- label the menu, don’t rely on icon recognition alone
- visible or hybrid nav is often stronger when possible
- do not blindly port mobile nav patterns to desktop

Implication for the template:
- avoid burying core tasks
- make menus obvious and labeled
- keep architecture shallow
- treat responsive adaptation as platform-aware, not copy-paste

## 5) Touch ergonomics matter more than pixel-perfect polish
The sources differ in exact numbers, but agree on the underlying principle:
- touch targets need enough size and spacing
- reachability matters
- clustered controls create misses and frustration
- tappability requires signifiers, not wishful thinking

This led to stronger language in the template around:
- forgiving touch targets
- spacing between actions
- thumb-friendly placement
- visible affordances

## 6) Typing is expensive on mobile
IxDF and practical mobile design guidance consistently point to minimizing manual input.

Strong recurring principles:
- prefill where possible
- use defaults, pickers, remembered state
- lean on biometrics, autofill, camera, and voice when appropriate
- preserve entered data through failure states

The template now treats input minimization as a first-class design concern, not a form polish item.

## 7) Continuity is part of mobile quality
Users get interrupted. Apps get backgrounded. Networks fail. Attention shifts.

The template therefore emphasizes:
- saved state
- draft persistence
- resumability
- calm loading/error handling
- continuity across devices when relevant

## 8) Accessibility is not separate from mobile quality
W3C/WAI and WCAG framing makes this crystal clear.

On mobile, accessibility and baseline usability overlap heavily:
- readable text
- contrast
- focus visibility
- reflow / zoom resilience
- touch target size
- clear labels
- compatibility with assistive tech

So the template now treats accessibility as part of the definition of done.

## 9) Performance is UX, especially on mobile
This showed up across mobile UX syntheses and platform guidance.

Fast load, low visual instability, clear loading states, and graceful offline/error behavior are not engineering nice-to-haves. They affect trust and task completion directly.

The template therefore includes:
- performance as a core design pattern
- explicit verification for loading/offline/failure states

## 10) Mobile-first is useful; mobile-only thinking is dangerous
NN/g’s “Mobile First Is NOT Mobile Only” is the corrective here.

The lesson is not “don’t design for mobile first.”
The lesson is “do not lazily port mobile constraints onto larger screens where they damage usability.”

This is why the template says:
- mobile-first, yes
- platform-aware and breakpoint-aware, also yes
- compressed desktop-by-accident, no

## Category-specific implications worth keeping in mind

### Commerce / checkout
- payment and address entry magnify mobile friction fast
- trust signals, error handling, and autofill matter disproportionately
- long forms are poison

### Social / content
- feed scan rhythm matters
- creation flows must be low-friction
- interruptions and return-to-context are critical

### Utility / workflow
- repeat usage favors predictable placement and low cognitive load
- search, filters, and resumability often matter more than visual flourish

### Messaging / communication
- attachment, typing, drafts, and notification boundaries become part of UX quality

## What I changed after going deeper

Compared with the first fast pass, the template is now more explicit about:
- hidden navigation tradeoffs
- visible affordances and tappability
- interruption/resumability
- platform-aware adaptation rather than generic responsive design
- accessibility as definition-of-done
- mobile context-of-use instead of generic “small screen” advice

## Limits / honesty

- Some canonical sources were JS-heavy or partially blocked by fetch tooling.
- A few desirable pages returned thin or blocked content.
- Even so, the strongest principles repeated across enough credible sources that the final template is grounded rather than improvised.

## Best next expansion if needed

If we want an even harder-core version later, split this into subtemplates:
- mobile-navigation-patterns
- mobile-forms-and-input-friction
- mobile-onboarding-and-permissions
- mobile-accessibility-checklist
- mobile-performance-and-resiliency

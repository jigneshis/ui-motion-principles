# UX laws: detail and applications

## Contents
- Doherty threshold
- Fitts's law
- Hick's law
- Von Restorff effect
- Frequency of use
- Peak-end rule
- Resolving conflicts between principles

---

## Doherty threshold
Productivity rises sharply when the system and user interact in under roughly 400ms. Slower than that and the interaction stops feeling like a conversation.

Apply:
- Acknowledge input immediately (within ~100ms): pressed state, spinner, skeleton, optimistic update.
- If work takes longer than ~400ms, show progress, not a frozen screen. Skeleton screens and optimistic UI beat spinners for perceived speed.
- Animations count against the budget. A 600ms transition before content appears makes the app feel slow even if the data was ready. Let content render while the transition plays, not after it.

## Fitts's law
Time to reach a target depends on distance and target size. Big and close is fast; small and far is slow.

Apply:
- Make primary actions large. On touch, aim for at least 44x44px (iOS) or 48x48px (Material) hit areas, even if the visible icon is smaller. Extend the hit area with padding.
- Place related actions near where the pointer or thumb already is. Destructive actions go farther away from frequent ones.
- Screen edges and corners are effectively infinite-size targets on desktop (the pointer stops there). Good for persistent navigation.
- On mobile, keep primary actions within thumb reach (bottom of screen) rather than top corners.
- Don't shrink spacing between adjacent targets so far that mis-taps happen.

## Hick's law
Decision time increases with the number and complexity of choices.

Apply:
- Cut options. Then group them. Then reveal progressively (accordions, "more" menus, steps).
- Highlight a recommended default (pricing tables: mark one plan).
- Break long forms into steps with one decision per screen when the stakes are high or the audience is new.
- Don't take this to the extreme: hiding frequent actions behind menus hurts Fitts and frequency of use. Reduce choices, not capability.

## Von Restorff effect
The item that stands out from similar items is the one remembered and acted on.

Apply:
- One primary button per view, visually distinct (color, weight, size). If two things are loud, nothing is.
- Use accent color sparingly so it keeps meaning. Highlight a recommended plan, a new feature, or a critical warning, not everything.
- Contrast can come from color, size, shape, motion or spacing. Motion is the strongest; use it for one thing at a time.

## Frequency of use
The more often a user triggers something, the less decoration it should have. Repeated animation turns from delight into friction.

A quick scale:
- Many times a day (tab switch, hover, command palette, typing feedback, list row actions): no animation or under ~100ms, subtle.
- A few times per session (opening a menu, a modal, toggling a setting): 150 to 250ms, simple ease.
- Rarely or once (onboarding, first success, empty state, upgrade, completion): room for expressive motion, exaggeration, longer timing.

This principle wins any conflict with the motion principles. Ask "how often does this happen?" before adding a flourish.

## Peak-end rule
People remember an experience mostly by its most intense moment and how it ended, not the average.

Apply:
- Identify the peak (the moment the product delivers its value: report generated, payment done, first video shared) and the end (checkout confirmation, task completion, logout, error recovery). Spend design and motion effort there.
- Make errors and empty states graceful: a bad ending drags down the whole memory.
- Don't spend the delight budget on the middle of the flow.

## Resolving conflicts between principles
- Frequency of use beats exaggeration and follow through.
- Doherty threshold beats timing: if a nice animation pushes response past ~400ms, shorten it.
- Hick's law vs Fitts's law: reduce the count of choices first, then make the remaining important ones big.
- Von Restorff only works if there is a baseline of calm; reduce competing emphasis before adding more.
- Accessibility (reduced motion, contrast, hit size) beats all aesthetic principles.

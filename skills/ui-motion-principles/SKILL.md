---
name: ui-motion-principles
description: Audit and improve a website or app UI using classic animation principles and UX laws, then apply the fixes after the user approves. Use this skill whenever the user asks to review, audit, polish or improve a UI, make an interface feel smoother or more premium, add or fix animations, transitions, micro-interactions, hover or press states, modals, drawers, toasts, loading states, or evaluate navigation, buttons, forms and CTAs for click targets, number of choices, emphasis or response speed (Fitts's law, Hick's law, Doherty threshold, Von Restorff effect, peak-end rule). Also use it when the user says "ui-motion-principles", "UI Motion Principles", or asks to check their site's UI/UX. Trigger even if the user never names a principle.
license: MIT
compatibility: [claude-code, gemini-cli, cursor, codex, antigravity, windsurf, amp, cline]
metadata:
  version: "1.0.0"
  author: "jigneshis"
  homepage: "https://skills.sh/jigneshis/ui-motion-principles/ui-motion-principles"
  repository: "https://github.com/jigneshis/ui-motion-principles"
  categories: ["ui", "design", "animation", "ux", "frontend"]
  tags: ["ui-motion", "framer-motion", "css-transitions", "micro-interactions", "ux-laws", "doherty-threshold", "fitts-law", "peak-end-rule", "von-restorff", "staggering", "anticipation"]
---

# UI Motion Principles

20 principles that separate interfaces that merely work from interfaces that feel intentional: 13 animation principles adapted from classic animation, and 6 UX laws about how people perceive and decide (plus frequency of use, which governs both).

The goal is not more animation. It is making every motion and layout decision defensible. Motion should explain what happened (where something came from, what changed). UX laws decide size, placement, count and emphasis. If a principle doesn't improve clarity or feel for the element at hand, skip it.

## Workflow: audit, announce, approve, apply

Follow these four phases in order. The approval gate exists because changing a live codebase's look and feel is hard to undo and highly subjective; the user should see exactly what will change and where before any file is edited.

### 1. Audit

Look at the UI before judging it.

- **Code first.** Find the project's UI source (components, styles, Tailwind config, animation code). Read the actual components for the screens the user cares about. If the user didn't say which screens, start with the main entry flow (landing page, dashboard, primary CTA path) and say that you chose it.
- **Live URL if available.** If the user gave a URL and you have a browser tool, open it and look at real behavior (hover states, transitions, load feel). If you have no browser tool, say so in one line and continue with code only. Never claim to have seen a page you didn't open.
- Read `references/motion.md` for anything that moves or changes state, and `references/ux-laws.md` for layout, choices, speed and emphasis. Pick the 3 to 5 principles that matter per element, not all 20.
- Check **frequency of use** first for every animated element. It overrides the other motion principles.

### 2. Announce the plan

Present a numbered change list before touching anything. Each item must say:

- **Where:** file and component (or screen and element)
- **Problem:** what is wrong today, in plain words
- **Principle:** which principle it violates
- **Change:** the concrete fix with values (duration, easing, size, distance)

Format each item like: `I will apply [principle] to [place]: [change].` Group by impact, highest first. Be blunt; vague advice like "make it smoother" is useless. Also list anything you looked at and decided to leave alone, with the reason, so the user knows it was considered.

Keep the list to what is worth doing. A list of 40 trivial tweaks hides the 5 that matter.

### 3. Wait for approval

Stop after the plan and ask which items to apply (all, a subset, or changes to the plan). Do not edit files in this phase. If the user replies with something like "apply all" or "1, 3 and 5", proceed with exactly that.

### 4. Apply

Make the approved changes only. Keep the project's existing stack and conventions (if it uses Tailwind and Framer Motion, don't introduce another animation library). Add a short comment only where a principle drove a non-obvious choice, for example `// anticipation: 2px dip before the lift`. Then run the review checklist below, and finish with a short summary: what changed, what was skipped, and anything the user should eyeball in a browser, since motion quality can't be fully judged from code.

## The 20 principles at a glance

**Motion principles** (details and recipes in `references/motion.md`)

| Principle | One-line meaning |
|---|---|
| Origin awareness | Things animate from where they came from (the trigger), not from nowhere |
| Anticipation | A small preparatory movement before the main action signals what's about to happen |
| Squash and stretch | Deformation on press or impact conveys weight and responsiveness |
| Slow in, slow out | Ease in and out; nothing starts or stops at constant speed |
| Arcs | Natural movement follows curves, especially for larger moves |
| Timing | Duration communicates weight, importance and distance |
| Exaggeration | Push the key motion slightly past realistic so it reads, then restrain the rest |
| Follow through | Parts keep moving briefly after the main body stops (overshoot, settle) |
| Secondary action | Supporting motion that reinforces the main action without competing |
| Staggering | Offset groups of items so the eye can track them |
| Rubber banding | Resistance and elastic snap-back at limits |
| Interruptible motion | Animations can be cancelled or reversed mid-flight and follow the latest input |
| Solid drawing | Consistent depth, light, shadow and radii so elements feel like real objects |

**UX laws** (details in `references/ux-laws.md`)

| Law | One-line meaning |
|---|---|
| Doherty threshold | Respond within about 400ms; show feedback sooner |
| Fitts's law | Target time grows with distance and shrinks with size; make key targets big and close |
| Hick's law | Decision time grows with the number of choices; reduce, group, disclose progressively |
| Von Restorff effect | The item that differs from its peers is the one remembered; one primary thing stands out |
| Frequency of use | The more often something happens, the less (and faster) it should animate |
| Peak-end rule | People judge an experience by its peak and its end; invest there |

## Defaults worth remembering

Starting points, not laws. Adjust to the product's personality.

- Micro-interactions (press, hover, toggle): 100 to 200ms. Small panels, menus, tooltips: 150 to 250ms. Large surfaces, modals, page-level: 250 to 400ms. Above ~500ms needs a reason.
- Entering: ease-out. Leaving: ease-in, and shorter than the entrance. Moving on screen: ease-in-out.
- Animate `transform` and `opacity`; avoid animating layout properties when a transform will do.
- Honor `prefers-reduced-motion`: swap movement for a fade or an instant change; don't delete the feedback.
- Springs give follow-through and interruptibility almost for free; prefer them for gestures. Prefer CSS transitions for simple hover and color changes.

## Review checklist

1. Does each animated element have an origin?
2. Is anything animating that users trigger constantly? Cut or shorten it.
3. Can every animation be interrupted without a glitch or snap?
4. Are durations proportional to distance and importance, with exits faster than entrances?
5. Is there one visually dominant primary action per view, large and reachable?
6. Is the number of simultaneous choices small, or grouped and progressively disclosed?
7. Does every action give feedback within ~100ms and finish or show progress within ~400ms?
8. Did the key moments (first success, completion, error recovery) get care?
9. Is reduced motion handled?

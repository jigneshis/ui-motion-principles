# Motion principles: detail and recipes

Examples use CSS and Framer Motion (React) since those are the most common targets. The ideas carry over to any stack.

## Contents
- Origin awareness
- Anticipation
- Squash and stretch
- Slow in, slow out
- Arcs
- Timing
- Exaggeration
- Follow through
- Secondary action
- Staggering
- Rubber banding
- Interruptible motion
- Solid drawing

---

## Origin awareness
Elements should visually come from the thing that created them. A dropdown grows from its button, a popover from its anchor, a modal from the card that was clicked, a toast from the edge it docks to. This keeps the user's mental map intact.

- Set `transform-origin` to the trigger's position (for a menu under a button: `top left` or the button's center).
- Don't scale every popover from `center` by default; that is the most common giveaway of an unconsidered animation.
- For shared-element transitions use Framer Motion `layoutId` or the View Transitions API.

```css
.menu { transform-origin: top left; animation: menu-in 160ms cubic-bezier(.2,.8,.2,1); }
@keyframes menu-in { from { opacity: 0; transform: scale(.96); } }
```

## Anticipation
A short preparatory movement before the main one. In UI it should be tiny and quick, otherwise it reads as lag.

- Button press: scale to ~0.97 on `:active` before the action fires.
- Drawer that is about to open: 2 to 4px nudge in the opposite direction.
- Drag start: slight lift (scale 1.02 and a stronger shadow).

Skip anticipation on high-frequency actions.

## Squash and stretch
Deformation conveys weight and elasticity. On screens this is subtle: a pressed button compresses, a bouncing element stretches along its motion axis.

- Keep it under ~5 to 8% for functional UI; more for playful or brand moments.
- Compress on one axis, expand slightly on the other so the element doesn't look like it is shrinking.

## Slow in, slow out
Objects accelerate and decelerate. Linear easing looks mechanical except for continuous loops (spinners, progress shimmer).

- Entering: ease-out, e.g. `cubic-bezier(0.2, 0.8, 0.2, 1)` or `cubic-bezier(0.16, 1, 0.3, 1)`.
- Leaving: ease-in, e.g. `cubic-bezier(0.4, 0, 1, 1)`.
- On-screen movement: ease-in-out, e.g. `cubic-bezier(0.4, 0, 0.2, 1)`.
- The built-in CSS `ease-in` / `ease-out` curves are weak; custom curves feel noticeably better.

## Arcs
Natural motion curves. For small moves a straight line is fine. For larger moves (an item flying to a cart, a FAB expanding, a card moving across the screen) split x and y onto different easings or durations so the path bows.

```js
// Different easing on each axis produces a curved path
<motion.div animate={{ x: 300, y: -120 }}
  transition={{ x: { duration: .5, ease: "easeOut" }, y: { duration: .5, ease: "easeIn" } }} />
```

## Timing
Duration communicates weight and distance. Bigger, heavier, or farther things take longer. Scale duration with distance travelled, within the ranges in SKILL.md. The same element should always use the same duration for the same kind of change, so the product feels consistent. Define duration tokens (`--dur-fast: 120ms; --dur-base: 200ms; --dur-slow: 320ms`).

## Exaggeration
Push the key beat beyond realism so it is legible, then keep the rest restrained. Use for moments that deserve attention: success, an error shake, a first-time reward. The error shake is a good example: 3 to 4 oscillations of ~6 to 10px over ~300ms. Do not exaggerate routine interactions.

## Follow through
Things don't stop dead. After the main motion, loose parts overshoot slightly and settle. Springs do this naturally.

```js
transition={{ type: "spring", stiffness: 400, damping: 28 }}  // small overshoot, quick settle
```

Raise damping to reduce bounce for serious or dense interfaces. Lower it for playful ones.

## Secondary action
A supporting motion that reinforces the primary one without stealing focus: a checkmark that draws itself while the checkbox fills; an icon that rotates as a section expands; a counter that ticks as a card slides in. Rule: if you notice the secondary action before the primary one, tone it down.

## Staggering
When several items appear together, offset them 20 to 60ms each so the eye can follow. Cap the total (for example, stop staggering after ~8 items or keep total stagger under ~400ms) so long lists don't feel slow.

```js
<motion.ul variants={{ show: { transition: { staggerChildren: .04 } } }} initial="hidden" animate="show">
```

Stagger on entrance, usually not on exit.

## Rubber banding
At boundaries, resist rather than hard stop. Pull-to-refresh, overscroll, sliders and drag-to-dismiss sheets should move less than the finger once past the limit (a damping factor like 0.3 to 0.5) and spring back on release. In Framer Motion use `dragElastic` and `dragConstraints`. Hard clamps feel broken.

## Interruptible motion
Users change their mind mid-animation. Animations that run to completion before responding feel sluggish.

- Prefer CSS transitions (they retarget smoothly from the current value) over keyframe animations for state toggles.
- Prefer springs for gestures; they carry velocity into the new target.
- Never block input during an animation unless it is truly unsafe.
- Test: click a toggle rapidly 5 times. If it stutters or desyncs, fix it.

## Solid drawing
Elements should feel like consistent physical objects: one light source, consistent shadow direction and softness, elevation that matches importance (higher elevation means larger, softer shadow, and sits above in z-order), and consistent corner radii. A card that lifts on hover should gain a larger, softer shadow and move up, not just change color. Inconsistent shadows and radii are the usual reason a UI looks "off" without anyone knowing why.

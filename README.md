# UI Motion Principles

An agent skill that audits your website or app UI against 20 animation principles and UX laws, tells you exactly what it plans to change and where, waits for your approval, and then applies the fixes.

**Animation principles:** origin awareness, anticipation, squash and stretch, slow in slow out, arcs, timing, exaggeration, follow through, secondary action, staggering, rubber banding, interruptible motion, solid drawing.

**UX laws:** Doherty threshold, Fitts's law, Hick's law, Von Restorff effect, frequency of use, peak-end rule.

## How it works

1. **Audit:** reads your UI source code (and opens your live URL if the agent has a browser tool).
2. **Announce:** lists each change as "I will apply [principle] to [place]: [change]" with concrete values.
3. **Approve:** you choose which changes to apply. Nothing is edited before this.
4. **Apply:** makes only the approved changes, in your existing stack.

## Install

Using the [skills CLI](https://github.com/vercel-labs/skills) (works with Claude Code, Gemini CLI and many other agents):

```bash
npx skills add jigneshis/ui-motion-principles
```

Gemini CLI directly:

```bash
gemini skills install https://github.com/jigneshis/ui-motion-principles --path skills/ui-motion-principles
```

Manual: copy `skills/ui-motion-principles/` into your agent's skills folder (for example `~/.claude/skills/` for Claude Code or `~/.gemini/skills/` for Gemini CLI).

## Use

- **Claude Code:** type `/ui-motion-principles`, or just ask it to audit your UI.
- **Gemini CLI:** skills are activated by the model when your request matches the skill description. Say something like: "Use the ui-motion-principles skill to audit my site's UI." Gemini asks you to confirm before activating it.
- **Other agents:** ask it to use the `ui-motion-principles` skill; check your agent's docs for how skills are loaded.

Example prompts:

> Use ui-motion-principles to audit the landing page in `src/pages/Home.tsx`.
>
> Check https://example.com with ui-motion-principles and tell me what to fix.

## What's inside

```
skills/ui-motion-principles/
├── SKILL.md              # workflow, principle summary, defaults, checklist
└── references/
    ├── motion.md         # the 13 animation principles with CSS / Framer Motion recipes
    └── ux-laws.md        # the 6 UX laws and how to resolve conflicts between principles
```

## License

MIT

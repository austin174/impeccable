# Impeccable — Usage Guide for Rephlex Digital

**Version:** 3.0.7 | **Creator:** [pbakaus/impeccable](https://github.com/pbakaus/impeccable) | **Org Fork:** [Rephlex-Digital/impeccable](https://github.com/Rephlex-Digital/impeccable)

Impeccable is a frontend design skill for Claude Code. It gives Claude a structured design vocabulary — typography, color theory, spatial design, motion, interaction patterns, and UX writing — so that when you ask it to build or improve UI, the output is production-grade rather than generic.

Think of it as hiring a design-aware co-pilot. Instead of Claude producing cookie-cutter interfaces, impeccable forces it through a proper design process: understand the brand, shape the UX, then build with craft.

---

## Installation (For Other Org Members)

```bash
# 1. Clone the org fork
git clone https://github.com/Rephlex-Digital/impeccable.git

# 2. Install dependencies (needed for anti-pattern detection and context loading scripts)
cd impeccable && npm install

# 3. Symlink the skill into Claude Code
ln -s "$(pwd)/.claude/skills/impeccable" ~/.claude/skills/impeccable
```

After symlinking, restart Claude Code. The `/impeccable` command will appear in the skill list.

---

## First-Time Project Setup

Before impeccable can do useful work in any project, it needs two context files at the project root:

| File | Required? | What It Contains |
|------|-----------|-----------------|
| `PRODUCT.md` | Yes | Target users, brand personality, tone, anti-references, strategic design principles |
| `DESIGN.md` | Recommended | Colors, typography, elevation, spacing, component conventions |

**To create these**, run:

```
/impeccable teach
```

Claude will interview you about your product/brand and generate both files. This only needs to happen once per project — after that, every impeccable command reads these files automatically to stay on-brand.

If you skip this step, impeccable will prompt you to run `teach` before it does anything else.

---

## Command Reference

Impeccable has 23 commands organized into 6 categories. All are invoked as `/impeccable <command> [target]`.

### Build — Create New Things

| Command | What It Does | When to Use |
|---------|-------------|-------------|
| `craft [feature]` | Full end-to-end build: shapes the design, gets your approval, then writes production code | You want a complete feature built with design quality baked in |
| `shape [feature]` | Plans UX/UI and produces a design brief — no code written | You want to think through the design before committing to code |
| `teach` | Interactive setup that creates PRODUCT.md and DESIGN.md | First time using impeccable in a project, or updating brand context |
| `document` | Generates DESIGN.md by analyzing existing project code | You already have a styled project and want impeccable to learn from it |
| `extract [target]` | Pulls reusable tokens and components into a design system | You want to formalize repeated patterns into a token/component system |

### Evaluate — Assess What Exists

| Command | What It Does | When to Use |
|---------|-------------|-------------|
| `critique [target]` | UX design review with heuristic scoring (two independent assessments merged) | You want an honest design quality score and actionable feedback |
| `audit [target]` | Technical quality checks: accessibility, performance, responsive behavior | You want measurable, code-level issues documented (not design opinions) |

### Refine — Make It Better

| Command | What It Does | When to Use |
|---------|-------------|-------------|
| `polish [target]` | Final quality pass before shipping — catches rough edges | You're almost done and want a last sweep |
| `bolder [target]` | Amplifies safe or bland designs — adds confidence and contrast | Your UI feels generic or timid |
| `quieter [target]` | Tones down overstimulating designs — removes noise | Your UI feels busy, loud, or overwhelming |
| `distill [target]` | Strips to essence, removes unnecessary complexity | Your UI has feature creep or too many elements |
| `harden [target]` | Production-readies: error states, i18n, edge cases, loading states | You're shipping soon and need to handle real-world scenarios |
| `onboard [target]` | Designs first-run flows, empty states, activation sequences | You need to guide new users through initial experience |

### Enhance — Add Specific Qualities

| Command | What It Does | When to Use |
|---------|-------------|-------------|
| `animate [target]` | Adds purposeful animations and motion | Your UI feels static and needs life |
| `colorize [target]` | Adds strategic color to monochromatic UIs | Your UI is too gray/neutral and needs visual energy |
| `typeset [target]` | Improves typography hierarchy and font choices | Your text feels flat or hard to scan |
| `layout [target]` | Fixes spacing, rhythm, and visual hierarchy | Your layout feels cramped, monotonous, or unstructured |
| `delight [target]` | Adds personality and memorable touches | Your UI is functional but forgettable |
| `overdrive [target]` | Pushes past conventional limits — ambitious visual effects | You want something technically extraordinary |

### Fix — Solve Specific Problems

| Command | What It Does | When to Use |
|---------|-------------|-------------|
| `clarify [target]` | Improves UX copy, labels, error messages | Users are confused by your interface language |
| `adapt [target]` | Adapts for different devices and screen sizes | Your responsive behavior needs work |
| `optimize [target]` | Diagnoses and fixes UI performance issues | Your UI is slow or janky |

### Iterate — Live Browser Mode

| Command | What It Does | When to Use |
|---------|-------------|-------------|
| `live` | Visual variant mode: pick elements in the browser, generate alternatives in real-time | You want to iterate on specific elements visually, seeing changes live |

---

## Common Workflows

### "I'm building a new feature from scratch"

```
/impeccable craft login page
```

This is the most common workflow. `craft` runs the full pipeline: it shapes the design (producing a brief for your approval), then implements it in production code. You approve the design direction before any code is written.

### "I want to improve an existing page"

```
/impeccable critique src/pages/dashboard.tsx
```

Start with `critique` to get an honest assessment and score. Then use the specific refinement commands to address what it found:

```
/impeccable polish src/pages/dashboard.tsx
/impeccable typeset src/pages/dashboard.tsx
/impeccable layout src/pages/dashboard.tsx
```

### "My UI looks like every other AI-generated interface"

```
/impeccable bolder src/components/Hero.tsx
```

Impeccable has built-in "AI slop detection" — it actively avoids the generic patterns that make interfaces look AI-generated (identical card grids, gradient text, hero-metric templates, glassmorphism-by-default, etc.).

### "I need to ship and want a final check"

```
/impeccable audit src/pages/checkout.tsx
/impeccable harden src/pages/checkout.tsx
/impeccable polish src/pages/checkout.tsx
```

`audit` finds technical issues (a11y, perf). `harden` adds error handling, edge cases, and i18n. `polish` does the final visual sweep.

### "I want to iterate visually in the browser"

```
/impeccable live
```

Opens a live browser session where you can click on elements and get design variants generated in real-time.

---

## Design Principles Impeccable Enforces

These are always active — you don't need to remember them. Impeccable will follow these automatically:

- **OKLCH color space** — modern, perceptually uniform color. Never `#000` or `#fff`.
- **Intentional theming** — dark/light chosen by use context, not by category convention.
- **Typography hierarchy** — 65-75ch line length, 1.25+ ratio between scale steps.
- **Rhythmic spacing** — varied padding for visual interest, not uniform boxes.
- **Purposeful motion** — exponential ease-out curves, no layout property animation.
- **Anti-pattern bans** — no side-stripe borders, gradient text, decorative glassmorphism, hero-metric templates, identical card grids, or reflexive modals.

---

## Pin/Unpin Shortcuts

If you use a command frequently, you can create a top-level shortcut:

```
/impeccable pin critique
```

Now `/critique` works directly without the `/impeccable` prefix. To remove:

```
/impeccable unpin critique
```

---

## Relevance for Rephlex Digital

**Client web development projects** — When building or redesigning client sites (Arovia CRM, any new web builds), impeccable ensures the frontend output is production-grade from the start rather than needing manual design review after.

**Landing pages and marketing sites** — For Rephlex Digital's own web presence or client landing pages, the `brand` register ensures marketing-quality design with proper visual hierarchy and conversion-oriented layouts.

**Shopify theme work** — When doing custom Shopify development (Poppyseed Play, Aqion), use `critique` and `audit` to evaluate existing theme sections, then targeted commands like `typeset`, `layout`, or `colorize` to improve specific elements.

**Internal tools** — For tools like the ops dashboard or Amazon image agent UI, the `product` register keeps interfaces functional and clean without over-designing.

---

## Keeping Updated

Check for upstream changes from the creator:

```bash
cd internal/impeccable
git fetch creator
git log HEAD..creator/main --oneline
```

If updates exist:
```bash
git merge creator/main
git push upstream main   # push to org
git push origin main     # push to personal fork
```

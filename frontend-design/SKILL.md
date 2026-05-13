---
name: refactoring-ui-design
description: Apply the Refactoring UI design system to produce beautiful, consistent, professional-looking user interfaces. Use this skill whenever building, styling, or refining any frontend UI — web app, mobile app, dashboard, landing page, component, form, marketing site, or anything else with a visual interface. Trigger this skill even when the user does not explicitly ask for "good design" — any time the task involves writing HTML, CSS, Tailwind classes, React/Vue/Svelte components, or styling decisions, follow this skill so the output looks intentionally designed instead of generic. Especially trigger when the user mentions design quality, polish, "make it look nice", "make it pretty", hierarchy, spacing, typography, color, shadows, or visual consistency.
---

# Refactoring UI Design System

Principles distilled from *Refactoring UI* by Adam Wathan and Steve Schoger. This skill exists because most "ugly" UI is not the result of missing artistic talent — it is the result of a handful of specific, learnable mistakes. Avoid those mistakes and apply the principles below and the output will look intentionally designed.

The single most important meta-principle: **design with systems, not arbitrary values**. Every decision (font size, spacing, color shade, shadow) should come from a predefined small set, never picked one pixel at a time.

## How to use this skill

This SKILL.md gives you the core principles, the design tokens, and a build-time checklist. For each topic there is a deeper chapter in `references/` — read the relevant chapter before working on that area:

| Working on… | Read |
|---|---|
| Starting a new design from scratch / framing a feature | `references/01-process.md` |
| Making one element more important than another | `references/02-hierarchy.md` |
| Spacing, white space, grids, responsive sizing | `references/03-layout-spacing.md` |
| Font choice, font sizes, line-height, alignment, links | `references/04-typography.md` |
| Picking colors, building palettes, accessibility | `references/05-color.md` |
| Shadows, raised/inset elements, layering | `references/06-depth.md` |
| Photos, icons, screenshots, user-uploaded content | `references/07-images.md` |
| Polishing a design that feels almost-done-but-plain | `references/08-finishing.md` |
| Looking up concrete token values (scales, shadows, shades) | `references/design-tokens.md` |

If the user uploads a separate brand or design system, prefer their tokens over the defaults in `design-tokens.md`. The principles still apply.

## Core principles (the short version)

1. **Start with a feature, not a layout.** Design one real piece of functionality at a time. Don't begin with the navbar, container, or shell.
2. **Hierarchy is everything.** Every screen has a primary thing, secondary things, and tertiary things. Make that clear visually — don't give every element equal weight.
3. **Use font weight and color for emphasis, not just size.** Bumping up a font size to make something "stand out" is usually the wrong tool. Reach for weight (600/700) or a darker color first.
4. **De-emphasize, don't emphasize.** When something doesn't stand out enough, the fix is usually to tone down its neighbours, not to amp it up.
5. **Start with too much white space, then remove it.** Cramped is the default failure mode. Generous spacing reads as intentional.
6. **Define systems before picking values.** Spacing scale, type scale, color shades, shadow elevations — define them once, then only pick from them.
7. **Not everything needs to be a relative/percentage size.** Fixed widths with `max-width` beat percentage-grid columns for most components. A sidebar should have a sensible fixed width, not 25%.
8. **Light comes from above.** Raised elements have a lighter top edge and a shadow below. Inset elements have a shadow on top and a lighter bottom edge.
9. **Color: HSL beats hex.** You need 8–10 shades of grey, 5–10 shades of each primary, plus accents for state (success/warning/danger). True black and pure grey rarely look good — saturate slightly.
10. **Match weight with contrast.** Heavy elements (bold text, solid icons) need lower contrast colors to stay balanced; thin elements (1px borders, hairlines) need slightly heavier weight or they disappear.

## The build-time checklist

Before declaring any UI "done", walk this checklist. If the answer to any question is "no" or "I didn't think about it", revisit the relevant chapter.

**Hierarchy**
- Can you identify the single primary action on the screen, and does it look more important than every other action?
- Are secondary and tertiary content de-emphasized (smaller, lighter, softer color) — not just "the same"?
- Are you using at most ~3 text colors (primary, secondary, tertiary) and ~2 font weights for body UI?

**Spacing**
- Did every spacing value come from a scale (multiples of 4 or 8, with appropriately non-linear jumps at the top), not from arbitrary numbers like 13px or 27px?
- Inside a group of related elements (label + input, item + meta), is the internal spacing tighter than the spacing around the group? (Avoid ambiguous spacing.)
- Is there more white space than feels comfortable on a single element? In a full UI it will read as "just right".

**Typography**
- Did every font size come from a defined type scale, not from incrementing pixels?
- Is body text 14–18px and line-height 1.5–1.7? Headlines tighter (1.1–1.3)?
- Is the line length between 45 and 75 characters for any paragraph text?
- Is mixed-size text aligned by **baseline**, not by center?

**Color**
- Are you using HSL (not hex) so you can reason about shade relationships?
- Do you have grey shades 100–900 plus 5–10 shades of each color? (Never use 3 greys; you will run out.)
- Did you avoid pure black (`#000`) and pure neutral grey? Saturate slightly toward warm or cool.
- For colored backgrounds: did you hand-pick a tinted lighter color instead of using grey or white-with-opacity for the secondary text?
- Does every status-color usage (red/green/yellow) also have a non-color signal (icon, label, shape)?
- Does body text hit WCAG AA (4.5:1) contrast?

**Depth**
- For any raised element: lighter top edge + small dark shadow below?
- For any inset element: small dark inset shadow on top + lighter bottom edge?
- Did the shadow come from a defined elevation scale (5 levels is enough)?
- Higher elevation = larger blur + larger offset + softer overall, not just "darker shadow".

**Images**
- Are icons being used at or near their intended drawn size, not scaled up 3–4×?
- For any text-on-image: is there an overlay, a desaturation, or a text-shadow ensuring consistent contrast?
- User-uploaded images: are they wrapped in a fixed-aspect container with `object-fit: cover` and a subtle inner shadow to prevent background bleed?

**Polish**
- Is there at least one "supercharged default" — custom bullets, accent border, custom radio/checkbox, decorated heading?
- Have you designed the empty state, not just the populated state?
- Did you remove unnecessary borders in favour of background-color changes or spacing?

## Default design tokens

When the user has no brand system, use these as defaults. Full details and rationale in `references/design-tokens.md`.

**Spacing & sizing scale (px)** — all multiples of 4 below 16, all multiples of 16 above:
```
4, 8, 12, 16, 24, 32, 48, 64, 96, 128, 192, 256, 384, 512, 640, 768
```
Use the small end (4–24) for padding/gaps inside components, the middle (32–128) for spacing between components, the top (192–768) for layout widths and large vertical rhythm.

**Type scale (px)**:
```
12, 14, 16, 18, 20, 24, 30, 36, 48, 60, 72
```
Base body text 16px. UI body and labels 14px. Small captions/meta 12px. Section titles 18–24px. Page titles 30–48px. Hero headlines 60–72px.

**Font weights** — typically only two in UI work:
```
400 or 500 — normal text
600 or 700 — emphasis, headings, buttons
```
Avoid weights below 400 for UI text. Avoid using a third weight just to make things "different" — change color or size instead.

**Line height** — inversely proportional to font size:
```
1.0   for very large display (60–72px)
1.1–1.2  for headlines (30–48px)
1.3–1.4  for section headings (20–24px)
1.5–1.6  for body text (14–18px)
1.7      for long-form reading
```

**Border radius — pick one personality and stick with it**:
```
0px      formal / serious
4–8px    neutral, default for most apps
12–16px+ friendly / playful
9999px   pills, full-round for tags and chips
```
Don't mix radii — if your buttons are 6px-rounded, your cards and inputs should be too (or a consistent scaled-up version).

**Shadow elevation scale** (HSL preferred so you can tint):
```
xs:  0 1px 2px hsla(0, 0%, 0%, 0.05)
sm:  0 1px 3px hsla(0, 0%, 0%, 0.10), 0 1px 2px hsla(0, 0%, 0%, 0.06)
md:  0 4px 6px hsla(0, 0%, 0%, 0.10), 0 2px 4px hsla(0, 0%, 0%, 0.06)
lg:  0 10px 15px hsla(0, 0%, 0%, 0.10), 0 4px 6px hsla(0, 0%, 0%, 0.05)
xl:  0 20px 25px hsla(0, 0%, 0%, 0.10), 0 10px 10px hsla(0, 0%, 0%, 0.04)
2xl: 0 25px 50px hsla(0, 0%, 0%, 0.25)
```
Two-shadow construction (one larger/softer for the cast shadow, one tighter/darker for the contact shadow) looks more polished than a single shadow.

**Grey scale (HSL — slightly cool, suitable for most UIs)**:
```
50:  hsl(210, 20%, 98%)   /* page background tints */
100: hsl(210, 17%, 95%)
200: hsl(210, 16%, 90%)   /* hairlines, soft borders */
300: hsl(210, 14%, 83%)   /* disabled / placeholder text */
400: hsl(210, 14%, 65%)   /* tertiary text */
500: hsl(210, 12%, 50%)   /* secondary text */
600: hsl(210, 13%, 40%)
700: hsl(210, 15%, 30%)   /* body text */
800: hsl(210, 18%, 20%)
900: hsl(210, 22%, 12%)   /* headings, darkest text */
```
**Never use pure `#000` for "black".** It looks unnaturally heavy. Use shade 900.

**Color usage roles** — every palette needs:
- **Greys** (9 shades, as above) — text, borders, panels, backgrounds. ~80% of UI surface.
- **Primary brand colors** (1–2 hues, 5–9 shades each) — primary buttons, links, active states, brand moments.
- **Accent / semantic colors** — success (green), warning (yellow/amber), danger (red), info (blue). 3–5 shades each.

See `references/design-tokens.md` for full HSL palettes for the semantic colors.

## When the user gives you a brand or design system

If the user provides brand colors, fonts, or design tokens in the conversation, project files, or attached docs, those override everything in this skill. The principles (hierarchy, spacing systems, depth simulation, etc.) still apply — only the specific values change.

## When in doubt

- **It feels cluttered** → add white space first, remove borders second, reduce text weight/color third.
- **It feels boring** → supercharge a default (custom bullets, accent border, hand-styled checkboxes), or add depth with a subtle gradient or shadow.
- **It feels flat / amateur** → check hierarchy. Almost certainly everything has the same visual weight.
- **It looks "off" but you can't say why** → check alignment. Mixed-size text is probably centered when it should be baseline-aligned, or spacing within groups is the same as spacing between groups.
- **The color looks washed out** → you're probably using grey text on a colored background, or you reduced opacity instead of hand-picking a tinted color.

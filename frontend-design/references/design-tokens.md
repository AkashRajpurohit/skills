# Design Tokens Reference

A consolidated set of concrete values for all systems described in this skill. Use these defaults when the user has no brand or design system of their own. If the user provides their own tokens, use theirs and ignore this file.

These values are framework-agnostic. CSS custom properties are shown for use in vanilla CSS, Tailwind, CSS-in-JS, or any other system.

## Spacing scale

Use these and only these for `margin`, `padding`, `gap`, and `width`/`height` when sizing things by spacing units.

```
--space-1:   4px
--space-2:   8px
--space-3:   12px
--space-4:   16px       ← base unit
--space-6:   24px
--space-8:   32px
--space-12:  48px
--space-16:  64px
--space-24:  96px
--space-32:  128px
--space-48:  192px
--space-64:  256px
--space-96:  384px
--space-128: 512px
--space-160: 640px
--space-192: 768px
```

(Numbering follows "multiples of 4" convention: `--space-N = N × 4px`. Aligns with Tailwind's default scale.)

**Usage guide**:
- 4–24 (`--space-1` to `--space-6`) — inside components: button padding, gaps in tight groups, icon-text gap.
- 32–128 (`--space-8` to `--space-32`) — between sibling components, vertical rhythm.
- 192+ (`--space-48` upward) — layout-level widths and large section spacing.

## Type scale

```
--text-xs:    12px
--text-sm:    14px
--text-base:  16px       ← body default
--text-lg:    18px
--text-xl:    20px
--text-2xl:   24px
--text-3xl:   30px
--text-4xl:   36px
--text-5xl:   48px
--text-6xl:   60px
--text-7xl:   72px
```

**Usage**:
- 12px — captions, footnotes, meta (sparingly).
- 14px — UI labels, dense table content.
- 16px — body text.
- 18px — comfortable long-form reading.
- 20–24px — small headings, intro paragraphs.
- 30–36px — page titles.
- 48–60px — landing-page headlines.
- 60–72px — hero / display.

## Font weights

```
--weight-normal: 400
--weight-medium: 500
--weight-semibold: 600
--weight-bold:   700
```
For UI work, typically use only two of these (e.g., 400 + 600, or 500 + 700). Avoid weights below 400 for any text under ~30px.

## Line height

```
--leading-none:    1.0
--leading-tight:   1.1
--leading-snug:    1.25
--leading-normal:  1.4
--leading-relaxed: 1.5
--leading-loose:   1.7
```

| Font size | Line-height token |
|---|---|
| 60–72px (display) | `--leading-none` to `--leading-tight` |
| 30–48px (titles) | `--leading-tight` to `--leading-snug` |
| 20–24px (subheadings) | `--leading-snug` to `--leading-normal` |
| 14–18px (body) | `--leading-relaxed` |
| 12–14px (small) | `--leading-relaxed` to `--leading-loose` |

Body text on wider columns can go up to `--leading-loose`.

## Letter spacing

```
--tracking-tighter: -0.03em    /* large display text */
--tracking-tight:   -0.01em    /* large headlines */
--tracking-normal:   0          /* default body */
--tracking-wide:     0.025em   /* small labels */
--tracking-wider:    0.05em    /* small all-caps eyebrows */
--tracking-widest:   0.1em     /* large all-caps display */
```

Default: don't touch letter-spacing. Apply tighter values only on text 30px and above; apply wider values on all-caps text.

## Border radius

Pick ONE radius personality and use it consistently. Mixing radii in one UI almost always looks worse than committing.

```
--radius-none: 0       /* formal, serious */
--radius-sm:   2px
--radius:      4px
--radius-md:   6px     /* neutral default */
--radius-lg:   8px
--radius-xl:   12px    /* friendly */
--radius-2xl:  16px
--radius-3xl:  24px    /* playful */
--radius-full: 9999px  /* pills, full-round */
```

**Component-specific guidance**:
- Buttons, inputs, cards — same radius family.
- Pills, tags, badges — `--radius-full`.
- Avatars, icon circles — `--radius-full` (always).
- Modals — usually one size up from your card radius.

## Border width

```
--border-0: 0
--border:   1px        /* default */
--border-2: 2px
--border-4: 4px        /* accent strips */
--border-8: 8px        /* heavy accents */
```

For ordinary borders, 1px is correct. Reach for 2–4px when adding a colored accent stripe (chapter 8). Avoid 3px — it almost never looks right.

## Shadows (elevation scale)

Two-shadow construction (one cast + one contact) for the most polished result:

```css
--shadow-xs:  0 1px 2px hsla(0, 0%, 0%, 0.05);
--shadow-sm:  0 1px 3px hsla(0, 0%, 0%, 0.10),
              0 1px 2px hsla(0, 0%, 0%, 0.06);
--shadow-md:  0 4px 6px hsla(0, 0%, 0%, 0.10),
              0 2px 4px hsla(0, 0%, 0%, 0.06);
--shadow-lg:  0 10px 15px hsla(0, 0%, 0%, 0.10),
              0 4px 6px hsla(0, 0%, 0%, 0.05);
--shadow-xl:  0 20px 25px hsla(0, 0%, 0%, 0.10),
              0 10px 10px hsla(0, 0%, 0%, 0.04);
--shadow-2xl: 0 25px 50px hsla(0, 0%, 0%, 0.25);
--shadow-inner: inset 0 2px 4px hsla(0, 0%, 0%, 0.06);
```

**Elevation usage**:
- `--shadow-xs` — flat-aesthetic raises, subtle button definition.
- `--shadow-sm` — cards on a clearly-distinct background.
- `--shadow-md` — cards on a same-colored background; hover state for cards.
- `--shadow-lg` — dropdowns, popovers, tooltips.
- `--shadow-xl` — large floating panels, side-sheets.
- `--shadow-2xl` — modal dialogs.
- `--shadow-inner` — inset states (pressed buttons, well containers).

### Refactoring UI book's original simpler scale

If you want the book's exact scale (single shadows, all at 20% opacity):
```
0 1px 3px   hsla(0, 0%, 0%, 0.2)
0 4px 6px   hsla(0, 0%, 0%, 0.2)
0 5px 15px  hsla(0, 0%, 0%, 0.2)
0 10px 24px hsla(0, 0%, 0%, 0.2)
0 15px 35px hsla(0, 0%, 0%, 0.2)
```

## Color tokens

### Greys (cool — recommended default)

```
--grey-50:  hsl(210, 20%, 98%)
--grey-100: hsl(210, 17%, 95%)
--grey-200: hsl(210, 16%, 90%)
--grey-300: hsl(210, 14%, 83%)
--grey-400: hsl(210, 14%, 65%)
--grey-500: hsl(210, 12%, 50%)
--grey-600: hsl(210, 13%, 40%)
--grey-700: hsl(210, 15%, 30%)
--grey-800: hsl(210, 18%, 20%)
--grey-900: hsl(210, 22%, 12%)
```

**Usage**:
- 50–100: page backgrounds, subtle panel tints.
- 200: hairlines, dividers, soft borders.
- 300: disabled-state text, input placeholder.
- 400: tertiary text (low-priority meta).
- 500: secondary text (captions, byline).
- 600–700: body text.
- 800–900: headings, primary text.

**Never use `#000`.** Use `--grey-900`.

### Greys (warm — alternative)

For a friendlier feel, swap to warm greys:
```
--grey-50:  hsl(36, 20%, 98%)
--grey-100: hsl(36, 17%, 95%)
--grey-200: hsl(36, 14%, 88%)
--grey-300: hsl(36, 12%, 80%)
--grey-400: hsl(36, 10%, 62%)
--grey-500: hsl(36, 8%,  48%)
--grey-600: hsl(36, 9%,  38%)
--grey-700: hsl(36, 12%, 28%)
--grey-800: hsl(36, 16%, 18%)
--grey-900: hsl(36, 20%, 10%)
```

### Primary (blue — recommended default)

```
--primary-50:  hsl(214, 100%, 97%)
--primary-100: hsl(214, 95%,  93%)
--primary-200: hsl(213, 97%,  87%)
--primary-300: hsl(212, 96%,  78%)
--primary-400: hsl(213, 94%,  68%)
--primary-500: hsl(217, 91%,  60%)  ← base, default button color
--primary-600: hsl(221, 83%,  53%)
--primary-700: hsl(224, 76%,  48%)
--primary-800: hsl(226, 71%,  40%)
--primary-900: hsl(224, 64%,  33%)
```

**Usage**:
- 50–100: tinted backgrounds (alert backgrounds, hover tints).
- 500–600: primary buttons, links.
- 700–800: hover states for primary actions, text on light tinted backgrounds.

### Success (green)

```
--success-50:  hsl(138, 76%, 97%)
--success-100: hsl(141, 84%, 93%)
--success-200: hsl(141, 79%, 85%)
--success-300: hsl(142, 77%, 73%)
--success-400: hsl(142, 69%, 58%)
--success-500: hsl(142, 71%, 45%)
--success-600: hsl(142, 76%, 36%)
--success-700: hsl(142, 72%, 29%)
--success-800: hsl(143, 64%, 24%)
--success-900: hsl(144, 61%, 20%)
```

### Warning (amber)

```
--warning-50:  hsl(48, 100%, 96%)
--warning-100: hsl(48, 96%,  89%)
--warning-200: hsl(48, 97%,  77%)
--warning-300: hsl(46, 97%,  65%)
--warning-400: hsl(43, 96%,  56%)
--warning-500: hsl(38, 92%,  50%)
--warning-600: hsl(32, 95%,  44%)
--warning-700: hsl(26, 90%,  37%)
--warning-800: hsl(23, 83%,  31%)
--warning-900: hsl(22, 78%,  26%)
```

### Danger (red)

```
--danger-50:  hsl(0, 86%, 97%)
--danger-100: hsl(0, 93%, 94%)
--danger-200: hsl(0, 96%, 89%)
--danger-300: hsl(0, 94%, 82%)
--danger-400: hsl(0, 91%, 71%)
--danger-500: hsl(0, 84%, 60%)
--danger-600: hsl(0, 72%, 51%)
--danger-700: hsl(0, 74%, 42%)
--danger-800: hsl(0, 70%, 35%)
--danger-900: hsl(0, 63%, 31%)
```

### Info (lighter blue — distinct from primary)

If your primary is also blue, use the same primary palette for info messages. If your primary is a different hue, use:
```
--info-50:  hsl(204, 100%, 97%)
--info-100: hsl(204, 94%,  94%)
--info-500: hsl(199, 89%,  48%)
--info-700: hsl(201, 96%,  32%)
```

## Z-index scale

Defined named layers prevent the dreaded `z-index: 9999` war.

```
--z-base:     0
--z-dropdown: 10
--z-sticky:   20
--z-fixed:    30
--z-modal-backdrop: 40
--z-modal:    50
--z-popover:  60
--z-tooltip:  70
--z-toast:    80
```

## Transitions

```
--ease-out:    cubic-bezier(0, 0, 0.2, 1)
--ease-in:     cubic-bezier(0.4, 0, 1, 1)
--ease-in-out: cubic-bezier(0.4, 0, 0.2, 1)

--duration-75:  75ms
--duration-100: 100ms
--duration-150: 150ms       /* default UI feedback */
--duration-200: 200ms
--duration-300: 300ms       /* modals, drawers */
--duration-500: 500ms
```

Default UI transitions (hover, focus, button press):
```css
transition: all var(--duration-150) var(--ease-out);
```

## Putting it all together — CSS root example

```css
:root {
  /* spacing */
  --space-1: 4px;   --space-2: 8px;   --space-3: 12px;  --space-4: 16px;
  --space-6: 24px;  --space-8: 32px;  --space-12: 48px; --space-16: 64px;
  --space-24: 96px; --space-32: 128px;

  /* typography */
  --text-xs: 12px;  --text-sm: 14px;   --text-base: 16px; --text-lg: 18px;
  --text-xl: 20px;  --text-2xl: 24px;  --text-3xl: 30px;  --text-4xl: 36px;
  --text-5xl: 48px; --text-6xl: 60px;  --text-7xl: 72px;

  --weight-normal: 400; --weight-medium: 500;
  --weight-semibold: 600; --weight-bold: 700;

  --leading-tight: 1.1; --leading-snug: 1.25; --leading-normal: 1.4;
  --leading-relaxed: 1.5; --leading-loose: 1.7;

  /* radius */
  --radius: 6px; --radius-md: 6px; --radius-lg: 8px;
  --radius-xl: 12px; --radius-full: 9999px;

  /* shadows */
  --shadow-sm: 0 1px 3px hsla(0,0%,0%,0.10), 0 1px 2px hsla(0,0%,0%,0.06);
  --shadow-md: 0 4px 6px hsla(0,0%,0%,0.10), 0 2px 4px hsla(0,0%,0%,0.06);
  --shadow-lg: 0 10px 15px hsla(0,0%,0%,0.10), 0 4px 6px hsla(0,0%,0%,0.05);
  --shadow-xl: 0 20px 25px hsla(0,0%,0%,0.10), 0 10px 10px hsla(0,0%,0%,0.04);

  /* greys */
  --grey-50: hsl(210, 20%, 98%);
  --grey-100: hsl(210, 17%, 95%);
  --grey-200: hsl(210, 16%, 90%);
  --grey-300: hsl(210, 14%, 83%);
  --grey-400: hsl(210, 14%, 65%);
  --grey-500: hsl(210, 12%, 50%);
  --grey-600: hsl(210, 13%, 40%);
  --grey-700: hsl(210, 15%, 30%);
  --grey-800: hsl(210, 18%, 20%);
  --grey-900: hsl(210, 22%, 12%);

  /* colors */
  --primary-500: hsl(217, 91%, 60%);
  --primary-600: hsl(221, 83%, 53%);
  --primary-700: hsl(224, 76%, 48%);

  --success-500: hsl(142, 71%, 45%);
  --warning-500: hsl(38, 92%, 50%);
  --danger-500: hsl(0, 84%, 60%);

  /* semantic */
  --bg-page: white;
  --bg-surface: var(--grey-50);
  --text-primary: var(--grey-900);
  --text-secondary: var(--grey-600);
  --text-tertiary: var(--grey-400);
  --border-default: var(--grey-200);
}
```

This produces a coherent, professionally-tokenized starting point you can use immediately.

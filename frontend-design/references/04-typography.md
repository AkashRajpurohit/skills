# Chapter 4 — Designing Text (Typography)

Typography is more than picking a font. The font size scale, line length, line height, letter spacing, alignment, and link styling each have their own rules.

## Establish a type scale

Most interfaces use too many font sizes — it's common to find every value between 10px and 24px used somewhere without intention. This causes inconsistency and slows you down. Define a scale.

### A linear scale doesn't work (for type either)

Same logic as the spacing scale: small jumps are useful at small sizes, useless at large sizes. You don't want to choose between 46px and 48px for a headline.

### Modular scales vs. hand-crafted scales

A **modular scale** uses a ratio (4:5, perfect fifth 2:3, golden ratio 1:1.618) to generate sizes from a base. It looks mathematically elegant, but has two problems for UI work:
1. Fractional pixel values (31.25px, 39.063px, …). Browsers handle subpixel rounding inconsistently. If you use this approach, round every value yourself.
2. The gaps are often wrong for UI work — too sparse in the mid-range. You'll want a size between 16 and 21, and another between 21 and 28.

For interface design, a **hand-crafted scale** is more practical:
```
12, 14, 16, 18, 20, 24, 30, 36, 48, 60, 72
```
Constrained enough to speed up decisions, broad enough that you don't feel you're missing a size you need.

**How to assign sizes**:
- 12 — captions, footnotes, very small meta (use sparingly).
- 14 — UI labels, dense body text, table content.
- 16 — body text (the browser default for a reason).
- 18 — comfortable body for long-form reading.
- 20–24 — small section headings, important UI labels, intro paragraphs.
- 30–36 — page titles, prominent section headings.
- 48–60 — landing-page headlines.
- 60–72 — hero / display.

### Avoid `em` units in your scale

`em` is relative to the *current* font size, so nested elements compute to sizes that aren't in your scale. If a container is `1.25em` (20px from 16px base), then a child at `0.875em` inside it is `17.5px` — not a value in any scale you defined.

Use **`px` or `rem`** for the type scale itself. `rem` is relative only to the root, so it stays predictable.

## Use good fonts

Years of taste-building separate "obviously bad font" from "good font", but a few shortcuts:

1. **Play it safe with a neutral sans-serif** (Inter, Helvetica, system fonts). For UI, this is almost always defensible. The system font stack is fine: `-apple-system, "Segoe UI", Roboto, "Noto Sans", Ubuntu, Cantarell, "Helvetica Neue", sans-serif`.
2. **Filter out typefaces with fewer than 5 weights.** Fonts with many weights (and italic variants) tend to be designed with more care. On Google Fonts, filtering to 10+ styles removes ~85% of the catalog.
3. **Optimize for legibility at your intended size.** Fonts designed for headlines have tighter letter-spacing and shorter x-heights; fonts designed for body have wider spacing and taller lowercase letters. Don't use a condensed-display font for UI body text.
4. **Use popularity as a proxy.** Sort by popular on font directories — if many real designers chose it, it's probably good.
5. **Steal from designs you admire.** Inspect the font in DevTools. Real design teams pick well; you can ride on their work.

## Keep line length in check

The most common typography mistake is fitting paragraph text to the layout instead of to the reader. The result: lines that are too long, which are tiring to read.

**The rule**: 45–75 characters per line for body text. ~65 is the sweet spot.

On the web, easiest way: use a `max-width` in `ch` units (≈ 1 character), or `em` units (a width of 20–35em hits the right ballpark for typical body sizes):

```css
.prose {
  max-width: 65ch;
}
```

If you mix paragraph text with wider components (images, code blocks, tables), constrain *only the paragraphs* to readable widths, and let the wider components break out:

```css
.article > *      { max-width: 65ch; margin-inline: auto; }
.article > figure { max-width: 100%; }
```

## Baseline, not center

When you align text of different sizes side-by-side, **align by baseline**, not by vertical center. The baseline is the imaginary line that letters rest on — it's the alignment your eye already uses.

```css
.row {
  display: flex;
  align-items: baseline;  /* not 'center' */
}
```

Centering mixed-size text creates subtle misalignment that reads as "off" even when nothing's obviously wrong. Baseline alignment looks immediately cleaner. This matters most when sizes are close together (a 16px label next to a 24px value); large size jumps hide the problem.

## Line-height is proportional

The "1.5 line-height is good" advice is true on average and wrong in detail. Line-height depends on **font size** and **line length**.

### Inversely proportional to font size

- Small text needs **more** line spacing — your eyes need help finding the next line.
- Large text needs **less** — at headline sizes, your eyes don't lose their place.

| Font size | Line-height |
|---|---|
| 12–14px | 1.5–1.7 |
| 16–18px | 1.5–1.6 |
| 20–24px | 1.3–1.4 |
| 30–48px | 1.1–1.2 |
| 60–72px | 1.0–1.1 |

### Proportional to line length

Wider columns of text need taller line-height because your eye has to jump further horizontally to find the start of the next line. Narrow columns can get away with tighter line-height.

If body text is full-width on a wide screen, push line-height toward 1.7–2.0. If it's constrained to a comfortable 65ch, 1.5 is fine.

## Not every link needs a color

In paragraph text where almost everything is *not* a link, you need to make links stand out — colored underline is fine. But in interfaces where *almost everything* is a link (sidebars, navigation, cards), the same treatment becomes overwhelming.

**Quieter link styles**:
- Just a heavier font weight, no color shift.
- Just a slightly darker color than surrounding text.
- For really ancillary links: no styling at all by default, but add an underline or color shift on hover. They remain discoverable to anyone who hovers, without competing for attention.

The principle: **emphasis is relative**. If everything is emphasized, nothing is.

## Align with readability in mind

Text alignment is mostly: match the language direction. For English and most Western languages, that means **left-align by default**.

### Don't center long-form text

Center-aligned text is fine for headlines and short blocks (1–2 lines). For anything longer, **left-align**. Centered paragraphs force the eye to find a new starting point on every line, which hurts reading speed.

If you have a stack of centered headlines but one is too long and looks bad, the right fix is usually to **rewrite it shorter**, not to give up on the alignment.

### Right-align numbers in tables

When numerical values are stacked in a column, right-align them so decimal points line up. This makes scanning and comparison instant. Use `font-variant-numeric: tabular-nums` so digits have equal width.

### Hyphenate justified text

Justified text on the web creates ugly word-spacing gaps unless hyphenation is enabled:
```css
.justified-text {
  text-align: justify;
  hyphens: auto;
}
```
Justified text suits formal/print-style layouts (online magazines). Left-aligned works for almost everything else. Don't reach for justified text unless you have a specific reason.

## Use letter-spacing effectively

Default rule: **trust the type designer**. Don't tweak letter-spacing. But there are two situations where it helps:

### Tightening headlines

A typeface like Inter or Open Sans is designed for legibility at small sizes — its built-in letter-spacing is wide. Used for large headlines, it can look slightly loose. Decreasing letter-spacing slightly (`-0.01em` to `-0.03em`) gives big text a tighter, more polished look.

The reverse rarely works — a headline-optimized font (tight spacing, condensed) doesn't become a good body font by widening the letter-spacing.

### Improving all-caps legibility

Letter-spacing in most fonts is optimized for sentence-case text. All-caps text has uniform letter heights (no descenders, no ascenders), so the default spacing makes all-caps strings harder to scan.

For any all-caps text — especially labels, tags, section eyebrows — **increase letter-spacing**:
```css
.eyebrow {
  text-transform: uppercase;
  letter-spacing: 0.05em;  /* 0.05em–0.1em is the typical range */
  font-weight: 600;
  font-size: 12px;
}
```
This is a small change that makes a disproportionately large difference in polish.

# Chapter 5 — Working with Color

Color is where most designs visibly fail. The single biggest fix is: reason about color in HSL, not hex, and define more shades than you think you'll need.

## Ditch hex for HSL

Hex and RGB make colors that are visually related look unrelated in code. HSL describes color the way the human eye perceives it.

- **Hue** (0–360°) — position on the color wheel. 0° red, 120° green, 240° blue. Two reds at different saturations are still both "red."
- **Saturation** (0–100%) — colorfulness. 0% is pure grey; 100% is maximum intensity.
- **Lightness** (0–100%) — proximity to white or black. 0% pure black, 100% pure white, 50% the "pure" form of the hue.

Why it matters: in HSL you can create a darker version of a blue by lowering its lightness, or a more vivid version by raising its saturation, *without* a color picker. In hex, the same color family looks like unrelated 6-digit strings.

### HSL ≠ HSB

HSB (also called HSV) uses "brightness" instead of "lightness." In HSB, 100% brightness is white only when saturation is 0%. In HSL, 100% lightness is always white. Most design software uses HSB; **browsers only understand HSL**. For web work, use HSL.

CSS:
```css
color: hsl(210, 14%, 30%);
background: hsla(210, 14%, 30%, 0.8);
```

## You need more colors than you think

The five-hex-codes "perfect color scheme" pattern doesn't work for real interfaces. You can't build anything useful with five colors. A working palette has three categories:

### Greys (most of your UI)

Almost everything in an interface is grey: text, backgrounds, panels, form controls, borders, dividers. You need **8–10 shades** of grey, not 3.

Three shades sound like plenty but you'll quickly want "just a bit darker than #2 but lighter than #3." Build the range up front.

**Don't use pure black.** True black (`#000`) looks unnaturally heavy and synthetic. Use a very dark grey (around `hsl(210, 22%, 12%)`) for your darkest shade.

### Primary color(s)

One, occasionally two, hues that define the brand and are used for primary actions, active states, and the moments that should feel "branded." Like greys, you want **5–10 shades** of each primary, not one.

The shade range serves different purposes:
- **Lightest 1–2 shades** — tinted backgrounds for alerts, callouts, badges.
- **Mid 1–2 shades** — buttons, primary actions, links.
- **Darker 1–2 shades** — hover states, text on light tinted backgrounds.

### Accent / semantic colors

A few more hues for specific communicative jobs:
- **Success** — green
- **Warning** — yellow / amber
- **Danger / destructive** — red
- **Info** — blue (often different from your primary blue)
- **Highlight / eye-catcher** — sometimes a separate hue (teal, pink) used to flag new features.

Each accent also needs multiple shades (5–10) even though they're used sparingly. A red used for an error icon needs a darker shade for the error text and a light tinted background for the error message panel.

**Categorical color** (lines on graphs, calendar events, tag colors): you may need additional hues — sometimes as many as 8–10 — each with their own shades. Plan for it.

> A complex UI is not uncommon to need ~10 distinct hues × 5–10 shades each.

## Define your shades up front

Don't generate shades on the fly with CSS `lighten()` / `darken()` or with `color-mix()`. You'll end up with 35 nearly-identical blues that all look the same and none of which are actually consistent.

**Define a fixed palette** and reference shades by name.

### Picking a 9-shade scale

Use the convention **100–900** (100 = lightest, 500 = base, 900 = darkest). 9 shades divides into a useful structure.

1. **Pick the base (500) first.** This is the color that anchors the family — usually the color you'd use for a primary button background. There is no formula; trust your eye.
2. **Pick the extremes (100 and 900) next.** Think about where each will be used:
   - 900 is usually reserved for dark text on light backgrounds.
   - 100 is usually a very light tinted background — a soft surface for alerts or hover states.
   Match the hue to the base, then adjust saturation and lightness until each end looks right.
3. **Fill in 300 and 700** — the midpoints. Each should feel like the right halfway compromise between the shades on either side.
4. **Fill in 200, 400, 600, 800** — the remaining gaps, using the same method.

You end up with a balanced ladder of 9 shades that supports almost every practical UI need.

### Greys follow the same process

Pick the darkest grey (for darkest text) and the lightest grey (for off-white backgrounds), then fill in the middle.

### Don't over-rely on math

After you've built the shade ladder by eye, **trust your eye** for adjustments. You will inevitably want to nudge a saturation, or add a 250 between 200 and 300 for a specific use case. That's fine — just avoid adding shades constantly, or you'll end up with no system at all.

## Don't let lightness kill your saturation

In HSL, a color at 50% lightness looks more colorful than the same color at 90% lightness or 10% lightness, even though saturation is unchanged. Pure colors get washed out as you push lightness toward either extreme.

**To compensate**: as you move lightness away from 50%, *increase* the saturation. A lighter shade with saturation pushed up will still feel vibrant; without that bump it looks pastel-and-washed-out.

### Use perceived brightness

Different hues have different inherent brightness. Yellow at 100% saturation, 50% lightness looks much lighter than blue at the same values. The perceived-brightness curve has three local maxima (yellow, cyan, magenta around 60°/180°/300°) and three minima (red, green, blue around 0°/120°/240°).

This gives you another lever: **change apparent brightness by rotating the hue**.

- To make a color lighter without simply pushing lightness toward white, rotate the hue toward the nearest bright hue (60°, 180°, or 300°).
- To make a color darker, rotate the hue toward the nearest dark hue (0°, 120°, or 240°).

This produces richer, more interesting gradients in shade ladders. Yellow shaded purely by reducing lightness becomes muddy brown; yellow that gradually rotates toward orange as it darkens stays warm and rich.

**Don't overdo it** — keep hue shifts within ~20–30° across a shade ladder, or it stops feeling like the same color family.

## Greys don't have to be grey

True grey (saturation 0%) is rare in good UI. Most "greys" in well-designed interfaces have a slight saturation that tips them warm or cool.

- **Cool greys** — small amount of blue saturation (~10–20% saturation around hue 200–220°). Reads as professional, modern, technical.
- **Warm greys** — small amount of yellow/orange saturation (~10–20% saturation around hue 30–50°). Reads as friendly, organic, comfortable.

Pick one temperature and apply it consistently across the entire grey ladder. Keep saturation high enough at the lightest and darkest shades that they don't look washed out compared to mid-greys.

## Accessible doesn't have to mean ugly

**WCAG AA contrast targets**:
- 4.5:1 for normal text (under ~18px or under bold 14px)
- 3:1 for large text

White-text-on-color often requires the color to be surprisingly dark. That creates a hierarchy problem: dark colored backgrounds grab attention, which is wrong if the element isn't the primary focus.

### Flip the contrast

Instead of white text on a dark colored background, use **dark colored text on a light colored background**. Same accent color, much less visual weight. A "warning" banner with dark amber text on a pale amber background is accessible *and* doesn't hijack the page.

### Rotate the hue for accessible colored text on colored backgrounds

Colored text on colored backgrounds is hard. Adjusting only saturation and lightness, you usually have to push the text almost to white to hit 4.5:1 — but then it looks the same as your primary text.

Use the perceived-brightness trick: rotate the hue toward a brighter hue (cyan, magenta, yellow) to increase contrast without going pure white. The text stays colorful, the contrast goes up.

## Don't rely on color alone

Color-blind users (~8% of men, ~0.5% of women) can't distinguish certain color pairs. Any information communicated purely by color is inaccessible to them.

**Always pair color with another signal**:
- Status icons (✓ for success, ⚠ for warning, ✕ for error) alongside the color.
- Direction arrows (↑↓) on metric cards alongside green/red text.
- Text labels ("Active", "Paused") alongside dot colors.
- Underlines on links in body text alongside color.

For data viz (charts with multiple trend lines), don't just pick different hues — pick lines with different **luminance** (lightness) too. A colorblind viewer can still tell light from dark even when they can't tell red from green.

**The principle**: color enhances signals that the design is already making. Color is never the *only* signal.

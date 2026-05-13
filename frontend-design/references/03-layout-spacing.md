# Chapter 3 — Layout and Spacing

The fastest way to make a design look more "designed" is to give every element more room to breathe.

## Start with too much white space

Most designs are cramped because white space is *added* — you start with elements jammed together, then add margin/padding until things "stop looking bad." That process bottoms out at the minimum tolerable spacing, which is far from optimal.

**Better approach**: start with way too much white space, then *remove* until it feels right. What seems excessive on a single element usually reads as "just enough" inside a complete UI.

**Exception**: dense UIs (dashboards, trading interfaces, code editors) where information density is itself the goal. That's fine — but make it a deliberate decision, not the default. It's much more obvious when a dense UI needs more space than when a spacious UI needs less.

## Establish a spacing and sizing system

Don't agonize between 120px and 125px. Define a constrained scale in advance and only pick from it. Without a system, you'll waste time on micro-decisions and produce inconsistent results.

### A linear scale doesn't work

"Multiples of 4" is not enough. The relative jump matters more than the absolute jump:
- Going from 12px → 16px is a 33% increase — visually significant.
- Going from 500px → 520px is a 4% increase — basically invisible.

For a usable scale, **no two adjacent values should be closer than ~25%**. That means tight increments at the small end, wider gaps at the large end.

### The default scale (px)

Start with a base of 16 (browser default font size, divides nicely) and build outward:
```
4    (16 × 0.25)
8    (16 × 0.5)
12   (16 × 0.75)
16   (16 × 1)
24   (16 × 1.5)
32   (16 × 2)
48   (16 × 3)
64   (16 × 4)
96   (16 × 6)
128  (16 × 8)
192  (16 × 12)
256  (16 × 16)
384  (16 × 24)
512  (16 × 32)
640  (16 × 40)
768  (16 × 48)
```
Notice the increasing gaps — that's deliberate, and it's why a naive "multiples of 4" scale isn't good enough.

**How to use the scale**:
- 4–24: padding inside components (buttons, inputs, cards), gaps in tight groups.
- 32–128: spacing between sibling components, vertical rhythm in content blocks.
- 192–768: layout widths, large vertical sections in landing pages.

## You don't have to fill the whole screen

Your design tool gives you 1400px of canvas. That doesn't mean you should use 1400px. If a piece of UI only needs 600px, give it 600px. Stretching narrow content wide makes it harder to read — line lengths grow, eye-tracking gets harder, and the design looks unbalanced.

**Don't make every section full-width** just because the navbar is full-width. Each component should get the space *it* needs, not the space its container offers.

### Shrink the canvas

If you're struggling to design a small interface on a large screen, **shrink the design canvas**. Try starting at ~400px (mobile width) and design that first. Then expand to desktop and adjust only the things that genuinely benefit from more space. You usually don't have to change as much as you'd expect.

### Use columns instead of stretching

If a component (e.g., a narrow form) looks unbalanced in a wide layout, don't just widen it. Split it into columns:
- Form fields on the left
- Helpful supporting text on the right

This uses the available space without compromising the form's optimal width.

### Don't force it the other way either

If something genuinely needs a lot of space (a big data table, a multi-panel editor), give it the space. The principle is *don't fill space just because it's there* — not *always shrink*.

## Grids are overrated

Twelve-column grids are useful for some kinds of layout, but treating "must be on the grid" as religion does more harm than good. Most components shouldn't be percentage-sized at all.

### Not every element should be fluid

A grid system fundamentally gives elements percentage-based widths from a constrained set of percentages. That's appropriate for some things, not others.

**Classic anti-pattern**: a sidebar that is "3 columns (25%)" on a 12-column grid.
- On a wide screen: the sidebar gets too wide, eating space the main content could use.
- On a narrow screen: the sidebar shrinks below its readable width, causing text wrapping or truncation.

**The fix**: give the sidebar a **fixed width** optimized for its contents (e.g., 240px or 280px), and let the main content area flex to fill whatever's left.

The same applies inside components — don't use percentages to size something unless you actually want it to scale.

### Don't shrink an element until you need to

A login card looks bad if it stretches across an entire wide screen, but the answer isn't "6-column on desktop, 8-column on medium screens" — that produces a card that is bigger on medium screens than on large screens, which is absurd.

**The fix**: give it a `max-width` of its optimal size (say, 500px). It stays at 500px from huge desktops down to ~500px viewports, then becomes fluid only when the screen actually forces it smaller.

```css
.login-card {
  width: 100%;
  max-width: 500px;
  margin: 0 auto;
}
```

## Relative sizing doesn't scale

It's tempting to define every dimension in `em` units relative to a base font size — "the headline is 2.5em, so it scales when I change the body text." This breaks down across screen sizes.

**Why**: the *ratio* between headline and body changes at different sizes. On desktop, body 18px + headline 45px ≈ 2.5×. On mobile, you might drop body to 14px to keep line length under control; 2.5× of that is 35px, which is too big for a small screen — the right size is closer to 20–24px, a ratio of 1.5–1.7×. There is no fixed relationship.

**General rule**: large elements need to shrink *faster* than small elements when screens get smaller. The difference between small and large elements should be less extreme on small screens than on large screens.

### Within a single component, too

If a button has 16px text, 16px horizontal padding, and 12px vertical padding, it's tempting to define padding as `1em` and `0.75em` so resizing scales everything proportionally. That works mechanically — but a "large" button that just zooms the small button doesn't *feel* like a larger button; it feels like the same button at 120% zoom.

**Better**: at larger sizes, give the button **proportionally more** padding (it should feel more generous, not just bigger). At smaller sizes, give it **proportionally less** padding (it should feel more compact, not just tinier).

Use `px` or `rem` (not `em`) for component internals so you can fine-tune each size independently.

## Avoid ambiguous spacing

When elements are grouped without a visible separator (no box, no border), spacing alone has to communicate which elements belong together.

**The rule**: there must be more space *around* a group than *within* it.

Common violations:
- **Form labels and inputs**: if the margin below a label equals the margin below the input, you can't tell which label belongs to which input. Increase the space between form groups so each label is clearly tied to *its* input.
- **Article section headings**: a heading needs more space above it than below it, or it looks like it belongs to the section above instead of below.
- **Bulleted lists**: if the space between bullets equals the line-height within a bullet, multi-line bullets blend together.
- **Horizontal lists** (avatars + names, icon + label): the same rule applies sideways. The space inside a single name+avatar unit must be tighter than the space between two units.

This is one of the most reliable "this UI looks confusing and I don't know why" diagnostics — fix the spacing-around-vs-within-groups ratio first.

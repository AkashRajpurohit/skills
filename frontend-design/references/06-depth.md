# Chapter 6 — Creating Depth

Depth is what turns flat shapes into "things." It's built from one underlying principle (light comes from above) plus a consistent shadow elevation system.

## Emulate a light source

The fundamental rule: **light comes from above**. In the real world, our brains use this to interpret 3D shape from 2D images. To create the same sense of depth in a UI, mimic how an above-source light would interact with the element you're showing.

### Raised elements

For something that should appear to *protrude* from the surface (a button, a card on a page background):

1. **Lighter top edge.** The top face catches the light. Add a top border or inset shadow with a small positive offset, in a lighter version of the element's color.
2. **Shadow below.** The element blocks light from reaching directly beneath it. Add a small dark `box-shadow` with a slight vertical offset and a tight blur radius.

Example (CSS):
```css
.button {
  background: hsl(220, 90%, 56%);
  box-shadow:
    inset 0 1px 0 hsl(220, 90%, 66%),   /* lighter top edge */
    0 1px 2px hsla(0, 0%, 0%, 0.2);     /* shadow below */
}
```

**Pick the lighter top-edge color by hand** (slightly lighter version of the base color). Using semi-transparent white on top doesn't work the same way — it desaturates the color and looks washed out.

### Inset elements

For something that should appear *recessed* (a text input, a "well" panel, a checkbox):

1. **Shadow on top.** The lip above the recess blocks light from reaching the top of the inset. Add a small dark inset `box-shadow` with a slight positive vertical offset.
2. **Lighter bottom edge.** The bottom edge faces upward and catches the light. Add a bottom border or inset shadow with negative offset in a slightly lighter color.

Example:
```css
.input {
  background: white;
  border: 1px solid hsl(210, 14%, 83%);
  box-shadow:
    inset 0 1px 2px hsla(0, 0%, 0%, 0.08),  /* shadow on top */
    0 1px 0 white;                          /* faint light bottom (if on a tinted background) */
}
```

This same pattern works for checkboxes, radio buttons, recessed badges, and "well" containers.

### Don't get photorealistic

It's tempting to keep adding nuance until your button looks like an actual physical button. Stop early. A few px of shadow and a 1px lighter top edge is plenty — adding gradients, multiple inset highlights, etc. makes the UI busy and unclear. The goal is *suggestion* of depth, not simulation.

## Use shadows to convey elevation

Shadows are not decoration — they tell the user **how far above the page** an element sits on a virtual z-axis. The closer something is, the more attention it captures.

**Shadow size and softness correspond to elevation**:
- **Smaller blur + smaller offset** = element sits just slightly raised (buttons, cards on flat backgrounds).
- **Larger blur + larger offset + softer shadow** = element sits much closer to the viewer (modals, popovers, focused dropdowns).

Typical usage:
- **Buttons** — smallest shadow, or none. They're part of the page surface.
- **Cards** — small to medium shadow.
- **Dropdowns / popovers** — medium shadow. They sit clearly above the page.
- **Modal dialogs** — large shadow. They demand attention and feel "in front of" everything else.

## Establish an elevation system

Like every other system in this skill: define a fixed set of shadows and pick from them. Five levels is usually plenty.

**Default elevation scale**:
```
xs:  0 1px 2px hsla(0, 0%, 0%, 0.05)
sm:  0 1px 3px hsla(0, 0%, 0%, 0.10), 0 1px 2px hsla(0, 0%, 0%, 0.06)
md:  0 4px 6px hsla(0, 0%, 0%, 0.10), 0 2px 4px hsla(0, 0%, 0%, 0.06)
lg:  0 10px 15px hsla(0, 0%, 0%, 0.10), 0 4px 6px hsla(0, 0%, 0%, 0.05)
xl:  0 20px 25px hsla(0, 0%, 0%, 0.10), 0 10px 10px hsla(0, 0%, 0%, 0.04)
2xl: 0 25px 50px hsla(0, 0%, 0%, 0.25)
```

The book's original scale (single shadows, linear progression):
```
0 1px 3px hsla(0, 0%, 0%, 0.2)
0 4px 6px hsla(0, 0%, 0%, 0.2)
0 5px 15px hsla(0, 0%, 0%, 0.2)
0 10px 24px hsla(0, 0%, 0%, 0.2)
0 15px 35px hsla(0, 0%, 0%, 0.2)
```

Either works. Define your set, name them, and use named tokens (`shadow-md`, `shadow-lg`) — not raw values.

## Shadows can have two parts

A polished shadow is often two shadows stacked:

1. **The cast shadow** — large, soft, with significant vertical offset and large blur radius. Simulates the shadow thrown behind the element by direct lighting.
2. **The contact shadow** — tighter, darker, with a small offset and small blur. Simulates the area under the element where even ambient light has a hard time reaching.

```css
.card {
  box-shadow:
    0 10px 15px hsla(0, 0%, 0%, 0.10),   /* cast shadow */
    0 4px 6px hsla(0, 0%, 0%, 0.05);     /* contact shadow */
}
```

This is more controllable than one shadow — you keep the cast shadow soft and subtle while still defining the element's edge crisply.

### Account for elevation in the contact shadow

In the real world, the contact shadow disappears as an object lifts further from the surface. So:
- **Lower elevation** (button, small card) — keep the contact shadow distinct.
- **Higher elevation** (modal, floating panel) — make the contact shadow much more subtle, or remove it entirely. The element is "far" from the page; there's no contact line to imply.

## Even flat designs can have depth

"Flat design" usually means no shadows, no gradients, no skeuomorphism. But the best flat designs still communicate depth — they just do it differently.

### Use color for depth

In general, lighter elements feel closer; darker elements feel further away.

- To make an element feel **raised** above the background, make it *lighter* than the background.
- To make an element feel **inset** (like a well or input), make it *darker* than the background.

Example: a card on a light-grey page background uses a *white* card background → reads as raised. A search input on the same page uses a *slightly darker grey* background → reads as inset.

This works in non-flat designs too. Color is another tool in the depth toolbox.

### Solid offset shadows

A flat-friendly alternative to soft shadows: a short, vertically-offset shadow with **zero blur radius**.

```css
.flat-card {
  background: white;
  box-shadow: 0 4px 0 hsl(210, 18%, 20%);
  border-radius: 8px;
}
```

You get the sense of lift without breaking the flat aesthetic. Common in playful or illustration-heavy designs.

## Overlap elements to create layers

One of the simplest depth tricks: make components overlap visually instead of stacking neatly. Layering reads as 3D space.

**Patterns that work**:
- A card that crosses the boundary between two different background colors (so it sits in front of both).
- A component taller than its parent container, poking out the top and bottom.
- Carousel controls that overlap the carousel's edges.
- Profile avatars that overlap the cover banner above them.
- A hero image with text or a card sitting partly over it and partly below it.

### Overlapping images

When images overlap each other, they can clash visually — edges fight and the layering reads as mistake rather than design.

**The fix**: give each image an "invisible border" matching the background color (or a small white outline) so there's always a slim gap between them.

```css
.gallery img {
  border: 4px solid var(--page-bg);
  /* or: outline: 4px solid var(--page-bg); */
}
```

You still get the layered effect; the visual collisions go away.

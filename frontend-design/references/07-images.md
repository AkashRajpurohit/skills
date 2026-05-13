# Chapter 7 — Working with Images

Bad images ruin good designs. Even when the layout, typography, and colors are excellent, a low-quality photo, awkwardly-scaled icon, or wildly-shaped user upload destroys the result.

## Use good photos

If your design uses photography and you aren't a skilled photographer:

1. **Hire a professional** for specific brand needs. Good photography is about lighting, composition, and color — skills that take years to develop. An expensive camera does not solve this.
2. **Use high-quality stock photography.** Unsplash, Pexels, and paid stock libraries all have excellent images. For most use cases this is enough.

**Don't design with placeholder images** with the intention of swapping in your phone snapshots later. The visual quality of your hero image is load-bearing in the design — degrading it will break what works.

## Text needs consistent contrast

The classic mistake: drop a headline on a hero photo, and no matter what text color you try, parts of it are unreadable. Bright sky areas drown out white text; dark shadows drown out dark text.

The problem is the image, not the text. A dynamic photo has both very light and very dark areas, and no single text color works against all of them.

**Four strategies** for ensuring consistent text contrast over an image:

### 1. Add an overlay

Put a semi-transparent layer between the image and the text:
- **Dark overlay** + light text (most common). Tones down bright areas so white text stays readable across the whole image.
- **Light overlay** + dark text. Brightens dark areas so dark text stays readable.

```css
.hero {
  position: relative;
  background-image: url(...);
  background-size: cover;
}
.hero::after {
  content: "";
  position: absolute;
  inset: 0;
  background: hsla(0, 0%, 0%, 0.4);  /* dark overlay */
}
.hero-content {
  position: relative;
  z-index: 1;
  color: white;
}
```

### 2. Reduce the image's contrast

Lowering the contrast of the image itself flattens it (reduces the gap between its brightest and darkest pixels), making the dynamic range less aggressive. Compensate for the overall brightness shift afterward.

```css
.hero img {
  filter: contrast(0.85) brightness(0.95);
}
```

### 3. Colorize the image

Tint the entire image with a single brand color so the variation in contrast disappears:
1. Reduce the image's contrast.
2. Desaturate it (make it grayscale or near-grayscale).
3. Add a solid brand color on top with `mix-blend-mode: multiply`.

```css
.hero {
  background: var(--brand-color);
}
.hero img {
  filter: grayscale(1) contrast(0.85);
  mix-blend-mode: multiply;
}
```

This both fixes contrast and unifies the image with your brand.

### 4. Use a text-shadow

If you want to preserve image dynamics, a soft text-shadow can boost contrast only where the text needs it. It should look more like a glow than a hard shadow — use a large blur radius and **no offset**.

```css
.hero-title {
  color: white;
  text-shadow: 0 0 20px hsla(0, 0%, 0%, 0.5);
}
```

Combine this with mild image contrast reduction for the best result.

## Everything has an intended size

Scaling bitmap images larger than their original size makes them blurry — that's well-known. But the subtler rule is that **every image has a size it was *designed* for**, and pushing far from that size always degrades it, including for vector graphics.

### Don't scale up icons

Icons drawn at 16–24px look chunky and clumsy when you blow them up to 64px or 128px to use as feature illustrations. Even though they're vector and don't pixelate, they were drawn with the level of detail appropriate for tiny rendering — at large sizes that detail is missing.

**Fix**: don't scale the icon up. Put it inside another shape (a circle, square, or rounded square) and scale *that* up. The icon stays near its intended size; the container fills the larger space.

```html
<div class="feature-icon">
  <svg class="icon-16">…</svg>
</div>
```
```css
.feature-icon {
  width: 64px; height: 64px;
  background: var(--brand-100);
  color: var(--brand-600);
  border-radius: 50%;
  display: grid;
  place-items: center;
}
.icon-16 { width: 24px; height: 24px; }
```

### Don't scale down screenshots

Shrinking a 1440px screenshot to 400px crams way too much detail into too little space. The 16px text in the screenshot becomes 4–5px and is unreadable, but visitors still notice the texture and squint trying to read it.

**Three better options**:
1. **Take the screenshot at a smaller layout** (tablet or mobile size) so you don't have to shrink it as much.
2. **Take a partial screenshot** — show just one panel or feature, not the whole app.
3. **Draw a simplified mockup** — for the smallest sizes, replace fine details with simple lines and shapes. Communicates the structure without inviting the reader to scrutinize unreadable content.

### Don't scale down icons either

Icons drawn at large sizes (logos, illustrations) turn to mush when you shrink them to favicon-size (16×16). The browser tries to render every detail and ends up with a blurry blob.

**Fix**: redraw a simplified, lower-detail version at the target size. You control the compromises — which details to drop, what to emphasize — instead of letting the browser destroy the original.

## Beware user-uploaded content

When users upload images, you lose all control of size, aspect ratio, color, composition, and background. The defenses:

### Control shape and size

Don't render user images at their intrinsic aspect ratio — it will destroy your layout. Wrap them in a fixed-aspect container and use `object-fit: cover` (or `background-size: cover`) so they crop cleanly to a consistent shape.

```css
.user-avatar {
  width: 48px; height: 48px;
  border-radius: 50%;
  object-fit: cover;
}

.uploaded-cover {
  aspect-ratio: 16 / 9;
  width: 100%;
  object-fit: cover;
}
```

This ensures every user-uploaded image fills the same shape, regardless of what they uploaded.

### Prevent background bleed

When a user's image has a near-white (or near-page-color) background, the image edge dissolves into your UI — the image visually loses its shape.

**Don't fix this with a border** — a hard border clashes with the colors inside almost every image. Instead, use a **subtle inset box-shadow**, which most users won't consciously notice but which clearly defines the image's edge.

```css
.uploaded-image {
  box-shadow: inset 0 0 0 1px hsla(0, 0%, 0%, 0.1);
}
```

Alternative: a **semi-transparent inner border** for the same effect, if you don't like the slight "inset" feel of a shadow.

```css
.uploaded-image {
  /* render the image and overlay a semi-transparent border */
  border: 1px solid hsla(0, 0%, 0%, 0.05);
}
```

Either way, the image's edge is always visible and the design holds together regardless of what users upload.

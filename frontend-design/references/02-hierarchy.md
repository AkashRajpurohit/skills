# Chapter 2 — Hierarchy is Everything

Visual hierarchy is how important elements appear relative to each other. It's the single highest-leverage tool for making something feel "designed." A UI without hierarchy reads as a chaotic wall of equally-shouting elements; the same UI with strong hierarchy looks polished even when colors, fonts, and layout are unchanged.

## Not all elements are equal

Every screen has:
- a **primary** thing (1, occasionally 2)
- a few **secondary** things
- some **tertiary** things (labels, meta, copyright, helper text)

Decide which is which before styling anything. If everything in your design has the same color/size/weight, you have not yet made hierarchy decisions.

## Size isn't everything

Relying on font size alone for emphasis is a classic mistake — it produces primary content that is too large and secondary content that is too small to read comfortably.

**Better levers than size**:
- **Font weight** — bumping a heading from 500 to 700 conveys importance without forcing the font size up. Stay in the 400–700 range for UI work; weights below 400 are hard to read at body sizes.
- **Color contrast** — using a softer grey for supporting text emphasizes the main text without shrinking the secondary text to unreadable.

**Color count**: aim for ~3 text colors total in any given context:
- Dark color → primary content (headline, body text in articles)
- Mid-grey → secondary content (date, byline, meta)
- Lighter grey → tertiary content (footer, copyright, helper text)

**Weight count**: typically only 2 weights:
- 400 or 500 — most text
- 600 or 700 — emphasis, headings, buttons

## Don't use grey text on colored backgrounds

Grey-on-white works because grey reduces contrast against white. The same grey on a colored background does *not* reduce contrast — it just looks dull and washed-out, sometimes like the text is disabled. Worse, semi-transparent white over a colored background lets the background show through, which looks even worse over images or patterns.

**The fix**: hand-pick a tinted color. Take the background color's hue, then adjust the saturation and lightness until the text feels appropriately de-emphasized while still feeling vivid. Don't use opacity to fake it.

## Emphasize by de-emphasizing

When the "important" element doesn't stand out, the instinct is to push it harder — make it bigger, brighter, bolder. This usually fails because the surrounding elements are also fighting for attention.

The opposite move works better: **tone down the neighbours**. An active nav item doesn't need a colored background if the inactive items are pushed to a soft, low-contrast grey. A sidebar doesn't need a heavy background tint if the surrounding content is given room and contrast — let the sidebar sit on the page background.

This is a recurring move in well-designed UI: solve "X doesn't pop" by making "everything not-X" quieter.

## Labels are a last resort

When showing data (especially from a database), the lazy approach is `label: value` pairs:
```
Email: jane@example.com
Phone: (555) 123-4567
Status: Active
```
Every piece of data ends up with equal emphasis because the labels share the visual weight of the values.

**Often you don't need a label.** Format tells you the type: `jane@example.com` is obviously an email, `$19.99` is obviously a price, `(555) 123-4567` is obviously a phone number. Context tells you the rest: "Customer Support" below a person's name is obviously their department.

**Combine label and value into prose** where you can:
- ❌ "In stock: 12"   → ✅ "12 left in stock"
- ❌ "Bedrooms: 3"    → ✅ "3 bedrooms"

**When you really need labels**, treat them as supporting content:
- Smaller font size, lighter weight, or lower-contrast color than the value.
- Exception: in technical-specification tables (phone specs, ingredient lists), users *scan for the label name* ("depth", not "7.6mm"). In that case, emphasize the label and slightly de-emphasize the value.

## Separate visual hierarchy from document hierarchy

The browser's default `h1`-is-huge, `h6`-is-tiny mapping is good for articles and documentation; it's a trap for app UIs. An `h1` of "Manage Account" does not need to be 48px just because it's an `h1`. Section titles often act more like labels — supportive content — than headlines, and should usually be **small**.

**Rule**: pick the HTML element for semantic correctness; pick the visual style for hierarchy correctness. They're separate decisions. In extreme cases, semantic headings can even be visually hidden (`sr-only`) when the content speaks for itself.

## Balance weight and contrast

Bold text feels emphasized because more pixels are covered. The same effect appears with icons (especially solid icons) — they're visually heavy and naturally feel prominent next to regular text. You can't change an icon's stroke weight, so to balance it:

- **Heavy element + needs to feel quieter** → lower its contrast. A solid icon next to a label looks balanced if the icon is in a softer color than the label.
- **Light element + needs to feel present** → increase its weight. A 1px hairline border that disappears at low contrast can be made visible by increasing it to 2px instead of darkening it.

This is the underlying mechanic: weight and contrast are inversely-substitutable for emphasis. If you can't change one, change the other.

## Semantics are secondary (for buttons)

Buttons are often designed by semantic role alone — "delete is destructive, so it's red." But every action also sits in a hierarchy of importance, and the visual treatment should reflect *that* first.

**Action hierarchy**:
- **Primary action**: solid, high-contrast background. There is usually only one per screen.
- **Secondary action**: outline style, or solid with a much lower-contrast background.
- **Tertiary action**: styled as a link, no background.

**Destructive ≠ primary.** A "Delete" link on a list of items should usually be a tertiary action (link-style), not a big red button. Save the red-and-bold treatment for the confirmation step, where deleting really *is* the primary action.

This rule keeps the visual noise down: most rows of buttons should have at most one solid background, not three competing colored rectangles.

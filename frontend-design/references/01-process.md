# Chapter 1 — Starting from Scratch

How to begin a design without getting paralyzed.

## Start with a feature, not a layout

Don't begin by designing "the app." An app is a collection of features, and you cannot make sensible decisions about navigation, containers, or shell structure until you have designed a few real features.

**Wrong starting points**: top nav vs. sidebar, logo position, container width, "the homepage."
**Right starting point**: pick one real piece of functionality (e.g., "search for a flight") and design only what that feature requires — the input fields, the button, the result list. Add the surrounding shell later, once you know what it needs to support.

The Google homepage was good not because it had a clever layout, but because it shipped the feature (search box, button) and nothing else.

## Detail comes later

In early-stage design, do not get hung up on typefaces, shadows, icons, exact colors. They matter eventually; they do not matter at the start.

- **Design in grayscale first.** Forcing yourself to communicate hierarchy without color makes you use spacing, contrast, and size for the heavy lifting — which produces a stronger underlying structure that color can later enhance.
- **Don't over-invest in mockups.** Sketches and wireframes are disposable. Move to the real thing as soon as the rough structure is clear.

## Don't design too much

Don't try to design every feature and edge case up front. You are setting yourself up for frustration trying to figure out, in the abstract, "what should this screen look like with 2000 contacts?" or "where does the error go in this form?"

**Work in cycles**:
1. Design a simple version of the next feature.
2. Build it.
3. Find the real edge cases by using it.
4. Iterate on the working thing.
5. Go back to design mode for the next feature.

It is much easier to fix problems in an interface that exists than to imagine every problem in a static mockup.

## Be a pessimist about scope

Don't imply functionality in your designs that you aren't ready to build. If you put a file-attachments section in your comment design and attachments turn out to be three weeks of work, the whole comment feature sits on the shelf. A comment system without attachments still beats no comment system. Ship the smaller version; add the nice-to-have later.

## Choose a personality

Every design communicates a personality, and personality is shaped by a small number of concrete factors:

- **Typography.** Serif → elegant / classic / editorial. Rounded sans-serif → playful / friendly. Neutral sans-serif → plain, neutral, lets other elements carry the personality.
- **Color.** Blue → safe, professional, familiar. Gold → expensive, sophisticated. Pink → playful, not-so-serious. Choose by gut and by what fits the audience.
- **Border radius.** 0px → formal, serious. ~4–8px → neutral, doesn't say much. 12px+ → playful and friendly. Pick one personality and **stay consistent** — mixing sharp and rounded corners in the same UI almost always looks worse than committing.
- **Language.** Word choice (formal vs. casual) has as much impact as visual choices. "Sign out" vs. "See ya later" tells you something about the product before you see anything else.

If you don't have a gut feeling, study the sites your target audience already uses. Match their general personality. But don't borrow too literally from direct competitors — you'll look like a second-rate version.

## Limit your choices

The biggest source of frustration in design is not constraint — it is the absence of constraint. When you can pick any pixel value for a font size, any hex code for a color, any margin in the universe, decision-making becomes torture because there is no clear right answer.

**The fix**: define a constrained set of options in advance and pick from it.

- Don't reach for the color picker — pick from 8–10 predefined shades.
- Don't tweak font size one pixel at a time — pick from a defined type scale.
- Don't measure spacing in the abstract — pick from a spacing scale.

This is "design by process of elimination": when only 3 options exist (16px, 24px, 32px), it's easy to dismiss two and commit to the third. When any value is possible, every option is plausible and decision fatigue takes over.

## Systematize everything

Have a defined system for:
- font size
- font weight
- line height
- color (every hue, multiple shades each)
- margin / padding
- width / height (especially for components like avatars, icons, controls)
- box shadows (elevation scale)
- border radius
- border width
- opacity

You don't have to define all of this up front. The mindset is: any time you find yourself agonizing over a small numeric choice, that's a signal to define a new system covering that property, so you never have to make that decision twice.

## The pattern across the chapter

Less choice → faster decisions → more consistent output → looks more "designed". This idea recurs throughout every other chapter.

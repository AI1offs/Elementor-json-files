# Widgets, Layout, and Structural Patterns

This document defines how to build **structurally sound layouts** using Elementor’s basic widgets and layout tools.

It focuses on:

- Containers / Sections / Columns
- Common layout patterns (hero, grids, feature rows)
- Spacing and alignment
- How to choose basic widgets for structure

All rules here must be applied **together with**:

- `docs/core-rules.md`
- `docs/elementor-modes-free-vs-pro.md`

---

## 1. Layout Systems: Containers vs Sections/Columns

Elementor currently supports two layout systems:

- **Containers** (flexbox-based, current recommended system).
- **Sections + Columns** (legacy system, still widely used).

**Rule:**

- For each client, inspect existing templates under `clients/<client-slug>/templates/`:
  - If they primarily use **Containers**, generate new templates using Containers.
  - If they primarily use **Sections/Columns**, mirror that system for consistency.

Do not mix the two systems arbitrarily unless the client already does so in existing templates.

---

## 2. Common Structural Patterns

### 2.1 Hero Section (Above-the-Fold)

Typical structure:

- One **Container or Section** spanning full width.
- Inside it:
  - Option A: Single Column/Container with stacked content:
    - Page Title / H1 (or H2 if H1 is provided elsewhere).
    - Subheading (H2/H3) describing the offer.
    - Primary call-to-action button.
    - Optional secondary button or link.
  - Option B: Two Columns/Containers for split layout:
    - Left: Heading + text + buttons.
    - Right: Image or illustration (using `Image` widget or a background image on the Container/Section).

Rules:

- Use global typography and colors (no hardcoded values).
- Ensure hero content is clear and simple on **mobile first**, then enhanced for tablet/desktop.

### 2.2 Multi-Column Feature Rows

Examples: three-column list of services, feature cards, or benefits.

Structure:

- Container/Section.
- Inside: a row of **2–4 columns/child containers**.
- Each column/child container may contain:
  - Icon (`Icon` widget).
  - Heading (`Heading` widget).
  - Short description (Text Editor with plain structural text).
  - Optional button (e.g., “Learn more”).

Rules:

- On mobile, columns should typically **stack vertically**.
- Use consistent padding and spacing across all cards.
- Use Heading levels appropriate to the page structure (often H3 or H4 inside such cards).

### 2.3 Testimonial / Social Proof Section

Structure:

- Container/Section.
- Inside: grid or carousel of testimonials.

Widgets:

- In **Free mode**:
  - Use the `Testimonial` widget or simple combinations of `Image` + `Heading` + Text Editor.
- In **Pro mode**:
  - You may use `Testimonial Carousel` or more advanced widgets when helpful.

Rules:

- Maintain readable typography and contrast.
- Limit motion/animation to avoid distraction.

---

## 3. Spacing, Alignment, and Sizing

### 3.1 Spacing

- Use **padding** inside Containers/Sections/Columns to create internal breathing room.
- Use **margin** to separate different sections from each other.
- Keep spacing consistent across similar sections by:
  - Copying spacing values from existing client templates where possible.
  - Avoiding arbitrary variation between similar sections.

### 3.2 Alignment

- Use Elementor’s alignment controls rather than custom CSS:
  - Horizontal alignment (left, center, right).
  - Vertical alignment (top, middle, bottom) within containers.
- On mobile:
  - Center alignment is often preferable for hero text and CTAs.
  - For lists or multi-column content, left alignment is often better for readability.

### 3.3 Width and Max Width

- Respect the **1920 × 1080** maximum design width.
- Use Elementor’s **content width** / max-width controls rather than manual pixel math.

When in doubt, copy width/max-width patterns from existing templates for that client.

---

## 4. Basic Widgets for Structure

When building layouts, prefer these **basic widgets** for structure and content:

- `Heading` – for all headings.
- `Page Title` – for the main page title (H1, used once).
- `Text Editor` – for body text blocks (multi-paragraph, lists), with **no inline styling**.
- `Image` – for standalone images.
- `Button` – for calls to action.
- `Icon` / `Icon Box` / `Image Box` – for feature cards.
- `Divider` / `Spacer` – to fine-tune spacing when necessary.
- `Tabs` / `Accordion` / `Toggle` – for collapsible content.
- `Social Icons` – for social profiles.

**Do not** use complex Pro widgets (Forms, Posts, etc.) in **Free mode**.

---

## 5. Responsive Behavior (Mobile First)

All layouts should be designed **mobile first**:

1. Start from the mobile view:
   - Ensure all content is readable and well-structured on small screens.
   - Stack columns vertically as needed.
2. Move to tablet:
   - Adjust column counts (e.g., 2 columns instead of 3).
   - Tweak spacing and typography for comfortable reading.
3. Finally, adjust desktop:
   - Increase white space as needed.
   - Use multi-column layouts where appropriate.

Use only Elementor’s **default breakpoints** and do not add custom ones.

---

## 6. Copying Patterns from Existing Templates

Whenever possible, AI assistants should:

- Identify sections in existing client templates that are structurally close to the requested design.
- Copy the Container/Section/Column structure and adjust:
  - Headings and text content.
  - Images and icons.
  - Button labels and links.

Benefits:

- Preserves spacing, typography, and alignment choices already approved for the client.
- Reduces the risk of inconsistent spacing or misaligned content.

---

## 7. Examples of When to Use Section vs Page Templates

- Use a **section template** when:
  - Building a reusable hero, testimonial band, pricing row, or CTA strip.
  - The user wants a block that will be inserted into multiple pages.

- Use a **page template** when:
  - Designing an entire page layout from top to bottom.
  - Multiple sections together tell a complete page story (hero, features, testimonials, CTA, etc.).

AI assistants should clarify with the user when it is ambiguous whether a request refers to a full page or a single reusable section.

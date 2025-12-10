# Elementor JSON Templates – Structure and Workflow

This document describes how an AI assistant should **understand, modify, and generate** Elementor template JSON files.

It is intentionally **conceptual** because Elementor’s internal schema can change between versions. For exact field names and structures, always inspect real exports under:

- `clients/<client-slug>/templates/`

Those exported files are the **ultimate ground truth**.

---

## 1. Template Types in Phase 1

Phase 1 covers two template types only:

- **Page templates** – full layouts for a page (e.g., homepage, services, contact).
- **Section templates** – reusable sections (hero, testimonials, pricing rows, CTAs, etc.).

**Rules:**

- When the user asks for a full page design → generate a **page template**.
- When the user asks for a slice (hero, footer strip, testimonial band) → generate a **section template**.

Site Kits and theme-wide exports are **Phase 2** and should not be assumed yet.

---

## 2. High-Level Template JSON Shape (Conceptual)

A typical Elementor template export contains at least:

- **Template metadata** – title, type (page/section), export version, etc.
- **Content tree** – an ordered list of top-level elements (containers / sections), each with children.
- **Optional page-level settings** – layout and global settings for that template.

Because exact key names may differ, follow this workflow:

1. Export a known-good template of the desired type (page or section) for the project.
2. Use that JSON as a **base reference** when creating new templates.
3. Keep the **top-level structure and keys** the same, only changing:
   - The human-readable title.
   - The element tree for layout and widgets.
   - Only those settings you **fully understand** and intend to change.

Never invent new top-level keys that do not appear in existing exports for that Elementor version.

---

## 3. Element Tree: Containers, Sections, Columns, Widgets

The core of any Elementor template is an **element tree**.

Conceptually, each element has:

- An **element type**, such as:
  - Container (or Section in older layouts)
  - Column (if using Sections/Columns)
  - Widget
- An **ID** – unique string within the template.
- A **settings** object – configuration options for that element.
- A list of **child elements** (for containers/sections/columns) or an empty list (for leaf widgets).

### 3.1 Parent / Child Relationships

- **Containers / Sections** are usually at the top of the tree.
- **Columns** are children of Sections (if that layout system is used).
- **Widgets** are children of Containers, Sections, or Columns.

Rules:

- Do not place widgets directly at the root; always place them inside the correct structural parent (Container, Section, or Column) based on the patterns in existing exports.
- When unsure, mirror a similar element tree from a known-good template and adjust only the parts that need to change.

### 3.2 IDs

Every element has a unique **ID** string.

- When **cloning** or reusing structures from another template, ensure IDs are:
  - Unique within the new template.
  - Not reused from other templates loaded on the same page if imported together.

AI assistants should:

- Either generate new IDs that follow the pattern seen in existing exports, or
- Use a clone of an existing element tree and **systematically update IDs** so there are no collisions.

The exact ID format is not important as long as it is:

- A string.
- Unique within that template.

---

## 4. Element Settings (Conceptual)

Each element has a **settings** object with keys and values that control:

- Content (text, image URLs, links, query options, etc.).
- Layout (widths, alignment, padding, margin, gaps).
- Styling (colors, typography, backgrounds, borders, shadows).
- Responsive behavior (per-breakpoint overrides).

Because these keys are specific to Elementor and may change,

- **Do not guess** new setting keys or values.
- **Do not remove** settings you don’t understand from a copied structure.

Instead:

1. Find a **similar element** in an existing template (e.g., an existing Button or Posts widget).
2. Copy its settings object as a starting point.
3. Change only the fields needed for the new design:
   - For text: change the content fields.
   - For images: change URLs (e.g., to `https://placehold.co/...`).
   - For layout: carefully adjust known spacing/alignment options.

If a user asks for a behavior that is not clearly mappable to existing settings, explain the limitation instead of inventing arbitrary keys.

---

## 5. Content Rules for Text and Media

These rules extend `docs/core-rules.md` specifically for JSON content.

### 5.1 Text Content

- **Language:** English (US).
- **Headings:**
  - Use `Heading` or `Page Title` widgets for headings, not Text Editor.
  - Respect the heading hierarchy rules from `core-rules.md` (H1 only for page title, etc.).
- **Body copy:**
  - Use Text Editor widget for **multi-paragraph** content or lists.
  - Do not apply inline styles inside Text Editor HTML.
  - Keep content semantic (paragraphs, lists, emphasis) and let global styles handle appearance.

### 5.2 Placeholder Text

- Use standard **Lorem ipsum** placeholders for text when real copy is not given.
- Do not mix placeholder text with real client brand names unless explicitly requested.

### 5.3 Images

- Use `https://placehold.co` for placeholder images.
  - Example: `https://placehold.co/800x600` for a medium landscape image.
- Choose sizes that broadly match the intended visual role:
  - Hero background: larger sizes (e.g., `1600x900`).
  - Icons or small images: smaller sizes (e.g., `200x200`).

If a client-brand asset is available under `clients/<client-slug>/branding/`, prefer that over a generic placeholder.

---

## 6. Respecting Global Styles and Core Rules

When setting typography, colors, spacing, and other styling in JSON:

- **Always prefer global styles** (Elementor’s global colors and typography) over hardcoded values.
- Do **not** insert hex colors directly in settings if a global color is available.
- Follow all rules from `docs/core-rules.md`:
  - No inline CSS or HTML styles unless explicitly required.
  - No custom breakpoints beyond Elementor defaults.
  - Mobile-first adjustments for responsive values.

When you see a setting in existing JSON that references a global token (e.g., a handle that maps to a global color or typography style), preserve that pattern.

---

## 7. Workflow for Creating a New Template JSON

When an AI assistant needs to create a **new** Elementor template JSON file:

1. **Determine the mode:**
   - Free or Pro, using `docs/elementor-modes-free-vs-pro.md` and `schema/ai-config.global.json`.

2. **Choose a base template:**
   - Find a template in `clients/<client-slug>/templates/` that is:
     - Of the same **type** (page or section).
     - Structurally similar to what is needed (e.g., a hero layout, a grid of cards).

3. **Copy the overall JSON structure:**
   - Keep the top-level object shape and keys.
   - Duplicate the content tree as a starting point.

4. **Adjust template-level metadata:**
   - Update the template title following the naming conventions in `core-rules.md`.
   - Set the type correctly (`page` vs `section`).

5. **Modify the element tree:**
   - Add, remove, or rearrange Containers/Sections/Columns/Widgets to match the requested layout.
   - Ensure parent/child relationships are valid and consistent with the base template.

6. **Update IDs:**
   - Ensure each element has a unique ID.
   - Avoid reusing IDs from unrelated templates.

7. **Update content and basic settings:**
   - Replace placeholder texts and image URLs as requested.
   - Adjust simple layout properties (like column widths, alignment) based on known-good patterns.

8. **Validate widget choices against the mode:**
   - In **Free mode**, ensure **no Pro/Theme/WooCommerce widgets** are used.
   - In **Pro mode**, Pro widgets are allowed but should be used only when helpful.

9. **Final pass for rules compliance:**
   - Check headings, colors, Text Editor usage, breakpoints, and other rules from `core-rules.md`.

---

## 8. Modifying an Existing Template JSON

When updating an existing template:

1. **Load the full JSON.**
2. Identify the specific section/element subtree to change.
3. Make minimal, targeted edits:
   - Try not to disturb unrelated elements.
4. Preserve:
   - Template-level metadata.
   - Element IDs (unless you are duplicating elements).
   - Any settings you do not fully understand.

If a requested change would require a major structural overhaul, it may be safer to:

- Start from a simpler base template, or
- Rebuild the element tree in a controlled way rather than patching a highly complex existing structure.

---

## 9. Phase 2 Considerations (Site Kits – Future)

For now, **do not** assume Site Kit-level structure. When Phase 2 begins, additional docs will define:

- How multiple templates are grouped into a kit.
- How global site settings are represented in exports.
- How to safely modify and regenerate kits.

Until then, focus on reliable, rule-compliant **page and section template JSON**.

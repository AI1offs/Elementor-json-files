# Core Rules for Elementor JSON Templates

This document defines **global rules and constraints** for generating Elementor JSON templates in this repository. All AI assistants must follow these rules unless a **client-specific doc** explicitly overrides them.

---

## 1. Scope and Phases

- **Phase 1 (current):**
  - **Template types:**
    - Single **page templates**
    - **Section templates**
  - Target: JSON templates that can be imported into Elementor’s Template Library.

- **Phase 2 (future):**
  - **Site Kits** (collections of templates + settings).
  - Not yet implemented; do **not** assume Site Kit behavior unless docs explicitly say so.

---

## 2. Theme and Platform Assumptions

- **Theme:** `Hello Elementor`.
- **Platform:** WordPress with Elementor at the **latest stable version**.
- **Addons:** Third-party addons may be present but are **not assumed** by default.

When a client uses additional addons, capture that in `clients/<client-slug>/docs/` and only then generate templates that depend on those addons.

---

## 3. Layout, Breakpoints, and Responsiveness

- **Max design width:** `1920 × 1080`.
- **Breakpoints:** Use **only Elementor’s default breakpoints**.
  - Do **not** introduce custom breakpoints.
- **Mobile-first approach:**
  - Think and plan layouts **mobile-first**.
  - When setting responsive values (padding, margin, font sizes, etc.):
    - Start with **mobile** values.
    - Then adjust for **tablet**.
    - Then adjust for **desktop**.
- **Containers / Sections / Columns:**
  - Prefer Elementor’s **current recommended layout system** (Containers) when possible.
  - If a client’s existing templates use classic **Sections + Columns**, follow the **existing pattern** in that client’s templates for consistency.

When unsure, mirror the structure of existing templates in `clients/<client-slug>/templates/`.

---

## 4. Typography and Heading Hierarchy

- **WordPress Page Title = H1:**
  - The WordPress page title is the **only H1** on the page.
  - If using the Elementor **Page Title** widget, ensure that **no other element** is set as H1.

- **Heading hierarchy:**
  - Use a proper semantic hierarchy:
    - `H1` – Page title only.
    - `H2` – Top-level section headings.
    - `H3` – Sub-sections inside an H2.
    - `H4` and below – Only if genuinely needed, do not overuse.
  - Do **not** use headings purely for visual styling; they must reflect content structure.

- **Global typography:**
  - Always use **Elementor global typography settings** where possible.
  - Do **not** hardcode font families, sizes, or weights inline unless absolutely required by a spec and documented.

---

## 5. Colors and Styling

- **No hardcoded colors:**
  - Do **not** hardcode any color values (e.g., hex codes) in templates.
  - Always use **Elementor global colors**.

- **Global styling only:**
  - Prefer to control colors, typography, and basic spacing through **global styles** and theme design settings.
  - Per-widget styling is allowed **only** when necessary and should still reference global tokens where possible.

- **Inline styling:**
  - Avoid inline CSS and inline HTML styles (e.g., `style="color: #ff0000"`).
  - Exceptions are allowed **only when explicitly required** by a project spec and must be minimal.

---

## 6. Text Editor Widget Usage

The Text Editor widget is **allowed but restricted**.

- **Default preference:**
  - Prefer other widgets when possible:
    - `Heading`
    - `Title` / `Page Title`
    - Other purpose-built widgets (e.g., `Button`, `Icon List`, etc.).

- **When to use Text Editor:**
  - For longer blocks of **body copy** where multiple paragraphs or basic inline formatting (bold, italic, links, lists) are needed.

- **Strict rule – No styling inside Text Editor content:**
  - Do **not** apply visual styling within the Text Editor’s content area that overrides global styles:
    - No inline styles (`<span style="...">`).
    - No custom colors applied directly in the editor.
    - No fake headings (e.g., using `<strong>` or `<b>` to simulate headings instead of real `H2/H3` widgets).
  - Keep Text Editor content **structural only**:
    - Paragraphs (`<p>`)
    - Lists (`<ul>`, `<ol>`)
    - Links (`<a>`) with no inline styling
    - Basic emphasis (`<strong>`, `<em>`) is acceptable for semantics, not for layout.

- **Styling for Text Editor:**
  - Typography, colors, line-height, and spacing should be controlled via **global styles or widget Style tab**, not via inline HTML.

---

## 7. CSS and Advanced Styling

- **No inline CSS by default:**
  - Do **not** add inline CSS to widgets or sections unless a spec explicitly requires it.

- **Custom CSS (Pro feature):**
  - If Elementor Pro Custom CSS is used, keep it **minimal, documented, and scoped**.
  - Prefer solving layout and styling needs with **built-in controls** first.

- **Animations and motion effects:**
  - Use motion effects (e.g., scroll animations, hover effects) sparingly and purposefully.
  - Ensure accessibility and readability are not harmed.

---

## 8. Placeholder Content and Media

- **Language:** English.
- **Region:** US.
- **Placeholder text:**
  - Use standard **Lorem ipsum** text when real copy is not provided.

- **Placeholder images:**
  - Use `https://placehold.co` for image URLs.
  - Choose appropriate sizes (e.g., `https://placehold.co/800x600`) based on design needs.

- **Dates and times:**
  - Use US formatting when examples are needed:
    - Dates: `May 21, 2025` or `05/21/2025`.
    - Times: `3:45 PM`.

---

## 9. Template Naming Conventions

To keep templates organized and predictable, use this naming pattern:

- **Pattern:** `client-slug-page-purpose` or `client-slug-section-purpose`.
  - Examples:
    - `acme-homepage-hero-section`
    - `acme-services-overview-page`
    - `acme-blog-listing-section`

Guidelines:

- Use **lowercase**, words separated by **hyphens**.
- Include the client slug at the start for clarity.
- Indicate whether it is a **page** or **section** in the name when helpful.

---

## 10. Client Folder Structure

Each client (website project) should live in its own folder under `clients/`:

- `clients/<client-slug>/branding/`
  - Logos, brand colors, typography notes, and any brand guides.

- `clients/<client-slug>/templates/`
  - Exported Elementor JSON templates for that client.
  - Treat these as the **canonical reference** when generating new templates:
    - Match structural patterns (Containers vs Sections/Columns).
    - Mirror typical spacing, layout density, and use of global styles.

- `clients/<client-slug>/docs/`
  - Client-specific overrides and instructions, such as:
    - Whether Elementor Pro is available (`mode: free` or `mode: pro`).
    - Any deviations from global rules.
    - Specific SEO or content rules.

When client-specific docs conflict with global rules in this file, **client-specific docs win**.

---

## 11. Modes: Free vs Pro (Overview)

- **Free mode (Elementor Core):**
  - Use only widgets and features available in the free plugin.
  - Do **not** rely on Theme Builder, Popup Builder, WooCommerce widgets, or other Pro-only features.

- **Pro mode (Elementor Pro):**
  - All Free mode capabilities plus:
    - Pro-only widgets (e.g., Posts, Forms, Nav Menu, Gallery, etc.).
    - Theme Builder widgets (Post Title, Archive templates, etc.).
    - WooCommerce widgets (Product Title, Add to Cart, etc.).

See `docs/elementor-modes-free-vs-pro.md` for **detailed widget lists and rules**.

---

## 12. General Principles

- **Match existing patterns:**
  - Always inspect and match the structural style of the client’s existing templates when available.

- **Keep JSON minimal and valid:**
  - Only include fields that are required or clearly understood.
  - Do **not** invent arbitrary properties.

- **Accessibility and SEO:**
  - Maintain semantic structure (headings, lists, links).
  - Avoid designs that rely solely on color to convey information.
  - Always provide meaningful `alt` text for brand and content images when the context is known (e.g., logo, product shot). When context is unknown, use a short neutral description or leave alt empty for purely decorative images, following project SEO/ADA guidance.
  - Respect the rules in `clients/<client-slug>/docs/seo.json` (when present) about which SEO plugin is active (e.g., Rank Math, Yoast) and which schema types they handle.
  - Do **not** add raw JSON-LD schema blocks inside Elementor templates unless a client-specific SEO doc explicitly requires it.
  - When FAQ or similar structured content is requested and the SEO plugin is not configured to generate FAQ schema, prefer Elementor widgets that provide built-in FAQ/Accordion markup and schema support, if available for the site’s Elementor version.

These rules are the foundation. All other docs in `docs/` and JSON configs in `schema/` **build on top of** these constraints.

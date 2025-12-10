# Posts and Loop-Based Templates (Pro Mode)

This document explains how to think about Elementor **Posts** and **Loop-based** widgets when designing JSON templates.

These features are **Pro-only** and should only be used in **Pro mode** (see `docs/elementor-modes-free-vs-pro.md`).

---

## 1. When to Use Posts / Loop-Based Layouts

Use Posts and Loop-based layouts when a design needs to show:

- A list or grid of **blog posts**.
- A list of **custom post types** (e.g., portfolio items, case studies) when configured.
- Dynamic lists that should automatically update when new content is published.

Avoid manually duplicating static cards for each post when a dynamic Posts/Loop layout is possible and Elementor Pro is available.

---

## 2. Posts Widget (Conceptual)

The **Posts** widget (Pro) displays a dynamic list of posts based on a query.

Key conceptual settings:

- **Query:** what posts to show (post type, categories, tags, authors, etc.).
- **Layout:** grid, list, masonry (depending on Elementor version/settings).
- **Pagination:** none, numbers, load more, infinite scroll, etc.
- **Card structure:** thumbnail, title, meta info, excerpt, read more.

AI assistants should:

1. Look for an existing Posts widget in the client’s templates.
2. Copy its settings as a starting point.
3. Adjust only what is requested (e.g., number of posts, categories, layout style).

In **Free mode**, do not use the Posts widget. Build a static layout instead, or explain that full dynamic behavior requires Pro.

---

## 3. Loop Grid and Loop Carousel (Conceptual)

The **Loop Grid** and **Loop Carousel** (Pro) separate:

- A **loop item template** (design of a single card).
- The **grid or carousel container** that repeats that item.

Conceptually:

- The loop item is usually a separate template that defines how each post/card looks.
- The grid or carousel widget references that template and controls query and layout.

For JSON-level work:

- Treat loop item templates similar to **section or page templates**, but dedicated to a single card.
- When requested to adjust a loop card design, modify the template used as the loop item, not the grid widget’s repetition logic.

Loop-based features should only be used in **Pro mode** and when the project actually uses them.

---

## 4. SEO and Structure Considerations

When designing Posts or Loop-based layouts:

- Ensure that:
  - Each post card has a clear **title heading** (usually H2 or H3, not H1).
  - Meta information (date, author, categories) is present or omitted intentionally.
  - Excerpts are kept concise and readable.

Do not create multiple H1 headings in cards; the page’s main H1 is still the page title.

---

## 5. Free vs Pro Behavior Summary

- **Free mode:**
  - Do **not** use Posts, Loop Grid, or Loop Carousel widgets.
  - If the user asks for a blog grid and Elementor Pro is not available:
    - Build a static layout using repeated Containers/Sections/Columns and basic widgets.
    - Explain that the grid will not update automatically when new posts are published.

- **Pro mode:**
  - Prefer Posts/Loop-based layouts for dynamic content.
  - Keep configuration as close as possible to existing client templates for consistency.

---

## 6. Workflow for AI When Using Posts / Loop Widgets

1. Confirm that the current project is in **Pro mode**.
2. Search existing templates for a Posts or Loop-based widget.
3. Copy the relevant element’s settings into the new design.
4. Adjust:
   - Query filters (categories, tags, etc.).
   - Number of posts.
   - Layout style (grid/list).
5. Ensure the rest of the page structure and styling obeys:
   - `docs/core-rules.md`
   - `docs/widgets-basic-and-layout.md`

If requested behavior cannot be clearly mapped to known settings, prefer a simpler, known-good configuration and document any limitations.

# Elementor Modes: Free vs Pro

This document defines how an AI assistant should behave when generating Elementor JSON templates for:

- **Free mode** – Elementor Core only.
- **Pro mode** – Elementor Pro is active.

It also lists **which widgets belong to which mode**, based primarily on Elementor’s official widget listings.

---

## 1. Mode Selection Rules

Before generating or modifying any JSON template, the AI must determine the **mode**:

- **Free mode (`mode = "free"`):**
  - Elementor Pro is **not** available.
  - Only **Basic widgets** (Elementor Core) may be used.

- **Pro mode (`mode = "pro"`):**
  - Elementor Pro is active.
  - Basic widgets **plus** Pro, Theme, and WooCommerce widgets may be used.

### 1.1 How to Choose the Mode

1. **If the client or project docs specify a mode:**
   - Use that mode (e.g., `clients/<client-slug>/docs/config.json`).

2. **If the user explicitly states the mode in a request:**
   - Use the user-provided mode.

3. **If the mode is unknown:**
   - Default to **Free mode** for compatibility and safety.
   - Clearly note in any explanation that Pro features were avoided due to unknown mode.

---

## 2. Widget Groups Overview

For clarity, widgets are grouped as follows:

- **Basic Widgets (Free / Core):** available in both Free and Pro installs.
- **Pro Widgets:** require Elementor Pro.
- **Theme Elements (Theme Builder):** require Elementor Pro.
- **WooCommerce Widgets:** require Elementor Pro + WooCommerce.

These groups are also encoded in `schema/ai-config.global.json`.

---

## 3. Basic Widgets (Elementor Free / Core)

These widgets are available in **Free mode** and **Pro mode**.

- **Layout & structure**
  - Inner Section
  - Container
  - Columns (classic sections/columns, if enabled in a project)

- **Content & media**
  - Heading
  - Image
  - Text Editor
  - Video
  - Button
  - Star Rating
  - Divider
  - Icon
  - Image Box
  - Icon Box
  - Basic Gallery
  - Image Carousel
  - Testimonial
  - Tabs
  - Accordion
  - Toggle
  - Social Icons
  - Progress Bar
  - Counter
  - Spacer
  - Text Path

- **Integrations / embeds**
  - Google Maps
  - Sound Cloud
  - Shortcode
  - HTML
  - Sidebar

- **Utility**
  - Menu Anchor
  - Alert
  - Link in Bio

**Rules in Free mode:**

- You may use **any** of the Basic widgets.
- You must also respect **core rules** from `docs/core-rules.md` (e.g., restricted Text Editor usage, global styles, etc.).

---

## 4. Pro Widgets (Elementor Pro)

These widgets require Elementor Pro and are available **only in Pro mode**.

- **Content & layout enhancers**
  - Posts
  - Portfolio
  - Slides
  - Gallery (advanced gallery, distinct from Basic Gallery)
  - Media Carousel
  - Flip Box
  - Call to Action
  - Testimonial Carousel
  - Nested Carousel
  - Loop Carousel
  - Table Of Content
  - Countdown
  - Blockquote
  - Reviews
  - Hotspot
  - Progress Tracker
  - Video Playlist

- **Marketing & interaction**
  - Form
  - Login
  - Share Buttons
  - Facebook Page
  - Facebook Button
  - Facebook Embed
  - Facebook Comments
  - PayPal Button
  - Stripe Button

- **Typography & visual effects**
  - Animated Headline
  - Lottie Widget
  - Code Highlight

- **Navigation & templates**
  - Nav Menu
  - Template
  - Mega Menu
  - Off-Canvas

**Rules in Pro mode:**

- You may use any **Basic** widgets **plus** these Pro widgets.
- Use Pro widgets when they provide a **clear structural or UX benefit**, but do not overcomplicate simple layouts.

---

## 5. Theme Elements (Theme Builder – Pro Only)

These widgets are used for **Theme Builder** templates (headers, footers, singles, archives, etc.) and require Elementor Pro.

- Post Title
- Post Excerpt
- Post Content
- Featured Image
- Author Box
- Post Comments
- Post Navigation
- Post Info
- Site Logo
- Site Title
- Page Title
- Search Bar
- Breadcrumbs
- Sitemap
- Loop Grid

**Rules:**

- These widgets appear mainly in **Theme Builder templates** (e.g., single post, archives, global header/footer).
- In **Phase 1**, focus is on **page** and **section** templates, but these widgets may still appear when building templates that act as single/loop building blocks.
- When using **Page Title**:
  - Ensure it represents the **only H1** on the page (see `core-rules.md`).

---

## 6. WooCommerce Widgets (Pro + WooCommerce)

These widgets require **Elementor Pro** and an active **WooCommerce** installation.

- Product Breadcrumbs
- Product Title
- Product Images
- Product Price
- Add To Cart
- Product Rating
- Product Stock
- Product Meta
- Product Content
- Short Description
- Product Data Tabs
- Additional Information
- Product Related
- Upsells
- Products
- Custom Add To Cart
- WooCommerce Pages
- Product Categories
- Menu Cart
- Cart
- Checkout
- My Account
- Purchase Summary
- WooCommerce Notices

**Rules:**

- Only use these widgets when:
  - The project explicitly uses **WooCommerce**, and
  - The mode is **Pro**.
- In purely non-eCommerce projects, do **not** include WooCommerce widgets in new templates.

---

## 7. Behavior by Mode

### 7.1 Free Mode

In **Free mode**:

- Allowed widgets:
  - All widgets listed under **Basic Widgets** above.
- Forbidden widgets:
  - All widgets listed under **Pro Widgets**, **Theme Elements**, and **WooCommerce Widgets**.

When a requested design would normally benefit from a Pro widget (e.g., Posts widget):

- Either:
  - Build a **static approximation** using Basic widgets (e.g., manual cards for blog previews), or
  - Explain that a fully dynamic solution requires Elementor Pro.

### 7.2 Pro Mode

In **Pro mode**:

- Allowed widgets:
  - **Basic Widgets**
  - **Pro Widgets**
  - **Theme Elements**
  - **WooCommerce Widgets** (if WooCommerce is in use)

Guidelines:

- Prefer using:
  - **Posts / Loop Grid** for post listings instead of manually duplicating post cards.
  - **Form** widget for lead capture instead of third-party shortcodes, unless the client specifies otherwise.
  - **Nav Menu** and **Mega Menu** for navigation.
- Always follow the structural and styling rules from `core-rules.md` (headings, colors, Text Editor rules, etc.).

---

## 8. JSON Encoding of Modes and Widgets

A machine-readable view of these modes and widget groups is provided in:

- `schema/ai-config.global.json`

AI assistants should:

- Use that JSON file to **validate** that chosen widgets are allowed in the current mode.
- Use this Markdown file for **human-readable explanations** and clarification.

---

## 9. Future Extensions

- As Elementor adds or renames widgets, this file and `schema/ai-config.global.json` should be updated.
- If a client relies on additional **third-party widgets**, they should be documented under:
  - `clients/<client-slug>/docs/third-party-widgets.md` (or similar),
  - Including which mode(s) they are allowed in.

In the absence of explicit documentation, assume that only the widgets listed in this file and in Elementor’s official documentation are available.

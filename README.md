# 🧠 Elementor JSON Template Docs – AI Assistant

[![Elementor](https://img.shields.io/badge/Built_for-Elementor_JSON-92003B?logo=elementor&logoColor=white)](https://elementor.com/)
[![Platform WordPress](https://img.shields.io/badge/Platform-WordPress-21759B?logo=wordpress&logoColor=white)](https://wordpress.org/)

> ⚙️ **Opinionated JSON blueprint for Elementor-powered AI assistants.**

**Scope:** JSON templates · **Theme:** Hello Elementor · **Modes:** Free & Pro · **Locale:** en-US

> 💡 **For AI assistants**  
> This repo is written primarily for AI agents and tools. Follow the steps below in order, respect client-specific overrides, and always output valid JSON.

This repository is a **knowledge base for AI assistants** that generate Elementor JSON templates for WordPress sites built with the **Hello Elementor** theme.

Phase 1 focuses on:

- **Single page templates**
- **Section templates**

Phase 2 will extend this to **Site Kits**.

All documentation is written in **Markdown** plus a small set of **JSON configuration files** that encode machine-friendly rules.

---

## 📚 Table of Contents

- [🤖 How an AI Assistant Should Use This Repo](#how-an-ai-assistant-should-use-this-repo)
- [🗂️ Repository Structure](#repository-structure)
- [🎚️ Elementor Mode Selection (High Level)](#elementor-mode-selection-high-level)
- [🧭 Phase 1 vs Phase 2](#phase-1-vs-phase-2)
- [🎨 Hello Elementor Theme Assumption](#hello-elementor-theme-assumption)
- [🌐 Language, Region, and Formatting](#language-region-and-formatting)
- [🚀 Where to Go Next](#where-to-go-next)
- [🔗 Official Elementor Resources](#official-elementor-resources)
- [🧩 Trusted Elementor Kits & Template Resources](#trusted-elementor-kits--template-resources)

---

## 🤖 How an AI Assistant Should Use This Repo

1. **Determine the Elementor mode (Free vs Pro).**
   - If the project/client configuration specifies a mode, follow it.
   - If the mode is unknown, **default to Free mode for safety**, and/or ask the user.
   - See `docs/elementor-modes-free-vs-pro.md` and `schema/ai-config.global.json`.

2. **Load global rules and constraints.**
   - Read `docs/core-rules.md`.
   - Read `schema/ai-config.global.json` for machine-readable constraints.

3. **Understand Elementor template JSON structure.**
   - Read `docs/elementor-json-templates.md`.
   - Use **existing exported templates** under `clients/<client>/templates/` as the canonical reference for exact field names and structures.
   - If no client templates exist yet, use the base container examples in `examples/` as safe starting points for structure.

4. **Plan the layout and widgets.**
   - Use `docs/widgets-basic-and-layout.md` for containers/sections, columns, spacing, and responsive behavior.
   - Use `docs/elementor-modes-free-vs-pro.md` to choose widgets that are allowed in the current mode.
   - Use `docs/posts-and-loop-templates.md` when working with Posts/Loop-based layouts (Pro mode only).

5. **Generate or modify JSON templates.**
   - Always produce **valid JSON** (no comments inside JSON).
   - Reuse and adapt structures from existing templates in the relevant client folder.
   - Respect all constraints from `docs/core-rules.md` and the current mode (Free or Pro).

In a **multi-agent setup**, the "AI assistant" is typically an orchestrator or project manager that **delegates these steps** to specialized agents defined in `docs/ai-agent-team.md`. Each step above may be handled by a different agent (e.g., mode analyst, layout architect, UI/UX designer, JSON engineer, validator), but all must still follow the same rules and workflow.

6. **Phase 2 (future): Site Kits.**
   - Once Site Kits are in scope, additional docs will be added under `docs/site-kits/` (or similar) and referenced from here.

---

## 🗂️ Repository Structure

Top-level structure:

- 📄 `README.md` – This navigation and overview for the AI assistant.
- 📁 `docs/`
  - 📄 `core-rules.md`
  - 📄 `elementor-modes-free-vs-pro.md`
  - 📄 `elementor-json-templates.md`
  - 📄 `widgets-basic-and-layout.md`
  - 📄 `posts-and-loop-templates.md`
  - (future docs may be added as needed)
- 📁 `schema/`
  - 📄 `ai-config.global.json` – machine-readable global rules and mode definitions.
- 📁 `examples/`
  - Container-based Elementor JSON template examples for reference and testing (importable into Elementor).
- 📁 `clients/`
  - One folder **per client / per website project**.
  - Sample client folders already present: `clients/Bob/` and `clients/Tom/`.

Client folder convention (recommended):

- `clients/<client-slug>/branding/`
  - Logos, brand guidelines, font choices, color palettes, etc.
- `clients/<client-slug>/templates/`
  - Exported Elementor JSON templates for this client.
  - These are the **primary structural examples** that new templates should follow.
- `clients/<client-slug>/docs/`
  - Client-specific notes and overrides for the global rules.
  - For example, whether Elementor Pro is available, special layout rules, or SEO/content requirements.

The AI assistant should always:

- Prefer **client-specific docs** over general rules when they conflict.
- Fall back to **global docs** (`docs/*.md` and `schema/*.json`) when client docs are missing or incomplete.

---

## 🎚️ Elementor Mode Selection (High Level)

- **Free mode (Elementor Core only):**
  - Use only **Basic widgets** listed in `docs/elementor-modes-free-vs-pro.md`.
  - **Do not** use Pro-only widgets, Theme Builder widgets, or WooCommerce widgets.
  - Use structural/layout patterns that do not rely on Pro features.

- **Pro mode (Elementor Pro active):**
  - All Free mode capabilities **plus** Pro widgets, Theme widgets, and WooCommerce widgets.
  - Use Pro widgets where they provide a clear structural or UX advantage (e.g., Posts, Forms, Nav Menu, Gallery, WooCommerce templates), as long as they align with the project’s needs.

Detailed lists and rules are in `docs/elementor-modes-free-vs-pro.md` and mirrored in `schema/ai-config.global.json`.

---

## 🧭 Phase 1 vs Phase 2

- **Phase 1 (current):**
  - Scope: **single page templates** and **section templates**.
  - Goal: Allow an AI assistant to reliably **read, modify, and generate** Elementor JSON templates that can be directly imported into Elementor.

- **Phase 2 (future):**
  - Scope: **Site Kits** (collections of templates + settings exported as a kit).
  - Additional docs will define:
    - Kit-level structure.
    - Relationships between templates (e.g., header/footer + single + archive).
    - Export/import workflows.

---

## 🎨 Hello Elementor Theme Assumption

All examples and rules assume:

- The site uses the **Hello Elementor** theme.
- Elementor is kept at the **latest stable version**.

If a project uses a different theme or heavily modifies the Hello theme, client-specific docs should capture those differences under `clients/<client-slug>/docs/`.

---

## 🌐 Language, Region, and Formatting

- **Language:** English
- **Locale / Region:** US
- **Dates and times:** US formatting (e.g., `January 15, 2025`, `05/21/2025`, `3:45 PM`).

Placeholder text should typically use **Lorem ipsum** in English, and placeholder images should use **https://placehold.co**.

---

## 🚀 Where to Go Next

For any AI assistant:

1. Read `docs/core-rules.md` **first**.
2. Read `docs/elementor-modes-free-vs-pro.md` and determine the mode.
3. Read `docs/elementor-json-templates.md` to understand the JSON structure.
4. Use widget and layout guidance from:
   - `docs/widgets-basic-and-layout.md`
   - `docs/posts-and-loop-templates.md` (when working with Posts/Loop layouts in Pro mode).
5. Inspect any existing templates in `clients/<client-slug>/templates/` before generating new ones.

---

## 🔗 Official Elementor Resources

- **Elementor Help Center (knowledge base)**  
  https://elementor.com/help/
- **Elementor Website Kits documentation**  
  https://elementor.com/help/learn-what-are-site-kits/
- **Working with Elementor Site Kits**  
  https://elementor.com/help/working-with-elementor-site-kits/
- **Elementor Academy – guides and tutorials**  
  https://elementor.com/academy/guides-and-tutorials/
- **Elementor Developers documentation**  
  https://developers.elementor.com/

---

## 🧩 Trusted Elementor Kits & Template Resources

- **Envato Elements – Elementor Template Kits**  
  https://elements.envato.com/wordpress/template-kits
- **Envato Elements – Elementor-compatible items library**  
  https://elements.envato.com/wordpress/compatible-with-elementor
- **ThemeForest – Elementor Template Kits marketplace**  
  https://themeforest.net/category/wordpress/elementor-kits
- **Templately – cloud templates & packs for Elementor**  
  https://templately.com/
- **Crocoblock – JetPlugins & dynamic templates for Elementor**  
  https://crocoblock.com/
- **Katka Template Pack – curated Elementor sections & pages**  
  https://wpbuilt.co/elementor-katka/


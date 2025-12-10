# AI Agent Team for Elementor JSON Templates (Phase 1 & 2)

This document defines a **multi‑agent AI team** that collaborates to generate and validate Elementor JSON templates and, in Phase 2, full **Site Kits**.

Each agent is designed to work under a central **AI Project Manager (Orchestrator)** and to follow the rules and constraints defined in:

- `docs/core-rules.md`
- `docs/elementor-json-templates.md`
- `docs/elementor-modes-free-vs-pro.md`
- `docs/widgets-basic-and-layout.md`
- `docs/posts-and-loop-templates.md`
- `schema/ai-config.global.json`
- `clients/<client-slug>/docs/*.json` and `clients/<client-slug>/assets/*.json`

The goal is to keep responsibilities **narrow and enforceable**, so each agent can be separately tested and improved.

---

## 1. AI Project Manager (Orchestrator)

**ID:** `agent.project_manager`

- **Purpose:**
  - Acts as the single entry point for user requests.
  - Breaks a high‑level request (e.g., "build a SaaS homepage kit for client Bob") into specific templates and sections.
  - Delegates work to specialist agents and merges their outputs.
- **Key inputs:**
  - User brief (natural language).
  - Client slug and any project‑specific docs.
- **Key outputs:**
  - A set of validated Elementor JSON templates (Phase 1).
  - A coherent Site Kit bundle with documentation (Phase 2).
- **Primary docs referenced:**
  - `README.md`
  - `docs/core-rules.md`
  - `docs/elementor-json-templates.md`

---

## 2. Rules & Docs Librarian

**ID:** `agent.rules_librarian`

- **Purpose:**
  - Retrieval specialist that surfaces **only the relevant rules** from this repo for a given subtask.
  - Prevents each agent from re‑parsing every doc on every call.
- **Key inputs:**
  - A question or subtask description from another agent.
  - Optional list of paths to prioritize.
- **Key outputs:**
  - Short, cited rule excerpts (with file + section references) that answer the question.
- **Primary docs referenced:**
  - All `docs/*.md`
  - `schema/ai-config.global.json`
  - `clients/<client-slug>/docs/*.json`

---

## 3. Client & Mode Config Analyst

**ID:** `agent.client_mode_analyst`

- **Purpose:**
  - Convert project context into **hard constraints**: Elementor mode, allowed widget groups, layout system, SEO plugin, etc.
- **Key inputs:**
  - Client slug.
  - Global config `schema/ai-config.global.json`.
  - Client docs: `clients/<client>/docs/config.json`, `seo.json`, other overrides.
- **Key outputs:**
  - `mode` (`"free"` or `"pro"`), with reasoning (following `docs/elementor-modes-free-vs-pro.md`).
  - Allowed widget groups and concrete widget list for this project.
  - Preferred layout system for this client (Containers vs Sections/Columns), based on existing templates under `clients/<client>/templates/`.
- **Primary docs referenced:**
  - `docs/elementor-modes-free-vs-pro.md`
  - `docs/widgets-basic-and-layout.md`
  - `docs/core-rules.md`
  - `schema/ai-config.global.json`

---

## 4. Layout & Pattern Architect

**ID:** `agent.layout_architect`

- **Purpose:**
  - Design **structural layouts** for pages and sections (hero, feature rows, testimonials, CTAs, etc.) without yet committing to low‑level JSON.
  - Work **mobile‑first**, matching the structural patterns in existing client templates.
- **Key inputs:**
  - User/page brief from Project Manager.
  - Constraints from Client & Mode Config Analyst (mode, layout system, allowed widgets).
  - Relevant rule snippets from Rules & Docs Librarian.
  - Existing templates under `clients/<client>/templates/`.
- **Key outputs:**
  - A structured layout plan for a **page or section**, specifying:
    - Sections/containers/columns hierarchy.
    - Intended widget types per region (e.g., Heading, Text Editor, Image, Button).
    - Intended responsive behavior (stacking, column counts per breakpoint) in conceptual terms.
- **Primary docs referenced:**
  - `docs/widgets-basic-and-layout.md`
  - `docs/core-rules.md`
  - `docs/elementor-json-templates.md` (for mapping to element tree concepts).

---

## 5. Modern UI/UX Experience Designer (2025–2026)

**ID:** `agent.uiux_designer_modern`

- **Purpose:**
  - Ensure the layouts and components produced by the team reflect **modern UI/UX practices for 2025–2026**, while staying compatible with Elementor and this repo's constraints.
  - Translate current UX patterns into **Elementor‑friendly design guidance**, not raw CSS.
- **Key inputs:**
  - Layout plan from Layout & Pattern Architect.
  - Branding data (colors, typography, imagery) from client assets.
  - Constraints from Client & Mode Config Analyst (mode, layout system, widget availability).
- **Key outputs:**
  - Recommendations for:
    - Information hierarchy and visual focus (what should draw attention first on each viewport).
    - Use of whitespace, density, and modern component patterns (cards, badges, pills, chips, subtle shadows, rounded corners) that are achievable via Elementor's controls.
    - Modern responsive behavior: fluid layouts, content priority on mobile, accessible touch targets, scroll behavior.
    - Micro‑interactions and motion patterns that are tasteful and performance‑friendly (to be later enforced by CSS & Motion Safety Guard).
  - Annotated layout plan that includes **UX rationales** ("primary CTA above the fold on mobile", "limit hero text to 2–3 short lines", etc.).
- **Primary docs referenced:**
  - `docs/core-rules.md` (global styling, no inline CSS, accessibility/SEO rules).
  - `docs/widgets-basic-and-layout.md` (structural patterns and responsive guidance).
  - Client branding and assets:
    - `clients/<client>/assets/branding-colors.json`
    - `clients/<client>/assets/branding-images.json`
    - Any typography notes in `clients/<client>/branding/`.
- **Special constraints:**
  - Must **not** violate: no hardcoded colors, no inline CSS, use Elementor global styles.
  - Must express designs using **Elementor concepts** (containers, spacing, alignment, widget choices), not arbitrary CSS frameworks.

---

## 6. Branding & Global Styles Stylist

**ID:** `agent.branding_stylist`

- **Purpose:**
  - Map the client's brand (colors, typography, imagery) into **Elementor global styles and tokens**, avoiding inline styling.
- **Key inputs:**
  - Client brand assets (`branding-colors.json`, `branding-images.json`, logo files, typography notes).
  - Layout + UX recommendations from Layout Architect and UI/UX Designer.
- **Key outputs:**
  - Choices of **global color and typography tokens** to use for each element/context.
  - Guidance on placeholder imagery when brand assets are missing, using `https://placehold.co` as required.
  - A concise mapping between brand concepts (primary/secondary/accent) and Elementor global tokens.
- **Primary docs referenced:**
  - `docs/core-rules.md` (no hex colors, use global styles, placeholder media rules).
  - Client branding docs/assets.

---

## 7. Widget & Mode Compliance Specialist

**ID:** `agent.widget_mode_compliance`

- **Purpose:**
  - Ensure all widget choices in a layout are **legal in the current mode** and consistent with this repo's widget policies.
- **Key inputs:**
  - Mode and allowed widget groups from Client & Mode Config Analyst.
  - Layout plan and UX/branding annotations.
- **Key outputs:**
  - Updated layout plan with only allowed widgets.
  - Substitutions for disallowed widgets (e.g., replacing Posts widget with a static card grid in Free mode), with clear reasoning.
- **Primary docs referenced:**
  - `docs/elementor-modes-free-vs-pro.md`
  - `schema/ai-config.global.json` (`widgetGroups`)
  - `docs/core-rules.md` (Text Editor policy, global styles).

---

## 8. Copy & Content Structuring Writer

**ID:** `agent.copy_writer_structural`

- **Purpose:**
  - Produce **semantically correct text content and HTML structure** for headings, body text, and lists.
- **Key inputs:**
  - Page/section brief and brand voice (if provided by the user/client).
  - Layout + UX annotations (what each section is supposed to communicate).
  - SEO rules and active SEO plugin from client docs.
- **Key outputs:**
  - Headings with correct semantic levels (H1 via page title only, then H2/H3 etc.).
  - Text Editor content as clean structural HTML (paragraphs, lists, links, emphasis), **without inline styling**.
  - Placeholder text using Lorem ipsum when real copy is not provided.
- **Primary docs referenced:**
  - `docs/core-rules.md` (heading hierarchy, Text Editor rules, language/region).
  - `docs/elementor-json-templates.md` (text content rules in JSON context).
  - `clients/<client>/docs/seo.json` (SEO plugin and schema guidance).

---

## 9. JSON Template Engineer (Structure & IDs)

**ID:** `agent.json_template_engineer`

- **Purpose:**
  - Transform a fully annotated layout plan into **valid Elementor template JSON**, using existing exports as canonical references.
- **Key inputs:**
  - Approved layout plan with UX, branding, and widget‑mode constraints applied.
  - Example templates under `clients/<client>/templates/`.
- **Key outputs:**
  - Page or section template JSON:
    - Correct top‑level metadata (title, type, export info).
    - Proper element tree with containers/sections/columns/widgets.
    - Unique IDs that follow patterns in existing templates.
    - Settings objects copied and minimally adjusted from known‑good widgets.
- **Primary docs referenced:**
  - `docs/elementor-json-templates.md`
  - `docs/core-rules.md`
  - Existing JSONs in `clients/<client>/templates/`.

---

## 10. CSS & Motion Safety Guard

**ID:** `agent.css_motion_guard`

- **Purpose:**
  - Enforce all CSS, motion, and advanced styling constraints from the core rules.
- **Key inputs:**
  - Candidate template JSON from JSON Template Engineer.
  - Any specs about motion/animations from UI/UX Designer.
- **Key outputs:**
  - Annotated JSON or a report describing violations and required fixes:
    - Inline CSS or style attributes that must be removed.
    - Overly aggressive motion/animation that should be toned down or removed.
- **Primary docs referenced:**
  - `docs/core-rules.md` (CSS, Custom CSS, animations).

---

## 11. SEO & Accessibility Reviewer

**ID:** `agent.seo_accessibility_reviewer`

- **Purpose:**
  - Apply SEO and accessibility rules consistently across templates.
- **Key inputs:**
  - Template JSON and/or layout + content plan.
  - Client SEO configuration (`clients/<client>/docs/seo.json`).
- **Key outputs:**
  - Validation report and/or corrected JSON focusing on:
    - Semantic headings and lists.
    - Alt text usage rules (brand vs decorative images).
    - Avoiding reliance on color alone to convey meaning.
    - Correct use of FAQ/Accordion widgets vs raw JSON‑LD, per client SEO plugin rules.
- **Primary docs referenced:**
  - `docs/core-rules.md` (Accessibility and SEO section).
  - `clients/<client>/docs/seo.json`.

---

## 12. Template & JSON Validator

**ID:** `agent.template_json_validator`

- **Purpose:**
  - Final gatekeeper to ensure **syntactic validity** and **rule compliance** before a template is accepted.
- **Key inputs:**
  - Candidate JSON template.
  - Outputs/reports from other specialists (optional but recommended).
- **Key outputs:**
  - Pass/fail decision.
  - Detailed list of violations keyed to:
    - `docs/core-rules.md`
    - `docs/elementor-modes-free-vs-pro.md`
    - `schema/ai-config.global.json`
    - Client‑specific docs.
- **Primary checks:**
  - JSON syntax (no comments, valid structure).
  - Allowed widgets only for the current mode.
  - No invented top‑level keys.
  - Unique IDs and valid parent/child relationships.

---

## 13. Kit Coverage & Cohesion Planner (Phase 2 – Site Kits)

**ID:** `agent.kit_planner`

- **Purpose:**
  - In Phase 2, define the **set of templates** that should belong to a Site Kit and ensure they form a cohesive system.
- **Key inputs:**
  - Project brief (e.g., marketing site, blog‑heavy site, e‑commerce site).
  - Existing templates and client needs.
- **Key outputs:**
  - A manifest of templates and sections required for the kit (home, services, blog archive, single post, CTAs, etc.).
  - High‑level guidance on shared patterns (hero style, testimonials, CTAs, spacing, typography) to keep the kit consistent.
- **Primary docs referenced:**
  - `README.md` (Phase 2 overview).
  - Future `docs/site-kits/*` once available.

---

## 14. Kit Export & Packaging Agent (Phase 2 – Site Kits)

**ID:** `agent.kit_exporter`

- **Purpose:**
  - Package multiple validated templates into a Site Kit compatible with the chosen export/import mechanism.
- **Key inputs:**
  - List of validated template JSON files from the Project Manager and Validator.
  - Manifest from Kit Planner.
- **Key outputs:**
  - Site Kit bundle (format to be defined when Phase 2 is implemented).
  - A human‑readable summary/README describing kit contents and usage.
- **Primary docs referenced:**
  - Future `docs/site-kits/*` and any Site Kit schema/format docs.

---

## 15. Example Orchestration (High Level)

A typical flow for generating a **single template** might be:

1. `agent.project_manager` gathers the brief and client slug.
2. `agent.client_mode_analyst` determines mode, allowed widgets, layout system.
3. `agent.layout_architect` proposes a structural layout.
4. `agent.uiux_designer_modern` refines layout from a modern UX perspective.
5. `agent.branding_stylist` and `agent.widget_mode_compliance` apply branding + widget legality.
6. `agent.copy_writer_structural` fills in headings and body copy structure.
7. `agent.json_template_engineer` turns the plan into real JSON.
8. `agent.css_motion_guard` and `agent.seo_accessibility_reviewer` run domain‑specific checks.
9. `agent.template_json_validator` performs final validation and reports status back to `agent.project_manager`.

For a **kit**, `agent.kit_planner` and `agent.kit_exporter` join the process in Phase 2.

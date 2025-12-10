# How to Use This Repo – Basics

**Who this is for:** You’ve been building WordPress sites for a few months, you just got **Elementor Pro**, and you want a simple way to **save and reuse templates**.

This repo is like a **template toolbox** that you (and an AI helper) can use to build Elementor sites faster.

---

## 1. What This Repo Is For

- **Stores Elementor templates as JSON files.**  
  These JSON files can be **imported into Elementor** to create pages, sections, headers, etc.
- **Teaches an AI assistant how to build for you.**  
  The docs here explain the rules, layout patterns, and which widgets are allowed.
- **Keeps each client organized.**  
  Every client/website gets its **own folder** with branding, templates, and notes.

You don’t have to understand every JSON detail. You mainly need to know **where things go** and **how to import/export** templates.

---

## 2. What You Need Before You Start

Make sure you have:

- A **WordPress site** you can log into.
- The **Hello Elementor** theme (recommended for this repo).
- **Elementor Pro** installed and activated.
- Access to this GitHub repo (downloaded to your computer or viewed online).

If all that’s good, you’re ready.

---

## 3. Quick Tour of the Folders

At the top level you’ll see folders like this:

- `docs/` – Rules and explanations for how templates should be built.
- `schema/` – Machine-readable rules (mainly for AI).
- `examples/` – Sample Elementor JSON templates you can import and learn from.
- `clients/` – One folder **per client/website**.

Inside `clients/your-client/` you’ll usually see:

- `branding/` – Logos, colors, fonts, brand notes.
- `templates/` – JSON exports of Elementor templates for that client.
- `docs/` – Extra notes just for that client (special rules, layout preferences, etc.).

You’ll spend most of your time with **`clients/`** and **`examples/`**.

---

## 4. How to Import a Template Into Elementor

Let’s say you want to try one of the JSON examples in `examples/` or a client template.

1. **Get the JSON file to your computer.**  
   - From GitHub: click the file → `Raw` → save it as `something.json`.
   - Or, if the repo is on your machine already, just find the `.json` file.
2. **Log into your WordPress dashboard.**
3. In the left menu, go to:
   - `Templates → Saved Templates` **or** `Templates → Theme Builder` (for headers/footers, etc.).
4. Click **Import Templates**.
5. Choose the `.json` file you saved and upload it.
6. After it imports, click **Edit with Elementor** to open it and look around.

You can now **learn from the template**, tweak it, and save your own version.

---

## 5. How to Export Your Own Template Back Into This Repo

Once you design something in Elementor that you like, you can save it into this repo.

1. In Elementor, open the page/section you want to save.
2. Click the **arrow next to the Update button** (bottom left), then choose **Save as Template**.
3. Give it a clear name, like:
   - `home-hero-v1`
   - `pricing-section-dark`
4. Go to `Templates → Saved Templates` in WordPress.
5. Find your template in the list and click **Export**.
6. This downloads a `.json` file to your computer.
7. Move that `.json` file into this repo, under:
   - `clients/<client-slug>/templates/`

Now the template is **backed up** in version control, and the AI assistant can use it as a reference.

---

## 6. How the AI Assistant Uses This Repo (Simple View)

You don’t have to memorize every doc, but here’s the basic idea:

1. **Global rules first**  
   The AI reads `docs/core-rules.md` to understand the general “do this, don’t do that” rules.
2. **Mode: Free vs Pro**  
   It checks `docs/elementor-modes-free-vs-pro.md` to see which widgets are allowed.
3. **Template structure**  
   It looks at `docs/elementor-json-templates.md` and `examples/` to see how JSON templates are built.
4. **Client-specific details**  
   It checks `clients/<client-slug>/docs/` and `clients/<client-slug>/branding/` for brand colors, fonts, and special rules.
5. **Generate or adjust JSON**  
   Based on all that, it generates or edits JSON in `clients/<client-slug>/templates/` that you can import into Elementor.

When you talk to the AI, you can say things like:

- "Use the **Bob** client and make a new homepage hero like the example in `clients/Bob/templates/hero-v1.json`, but with a big call-to-action button."  
- "We’re in **Pro mode**, so it’s okay to use the Posts widget and Theme Builder features."

---

## 7. Common Mistakes & Quick Fixes

- **Imported template looks broken**  
  - Make sure the site is using **Hello Elementor** (or at least compatible settings).
  - Check that Elementor and Elementor Pro are **up to date**.

- **JSON won’t import**  
  - Confirm the file ends in `.json` and wasn’t edited in a way that broke the format.
  - Redownload from GitHub if needed.

- **AI output won’t import**  
  - Ask the AI to "validate the JSON" and make sure there are **no comments** inside the JSON.
  - Compare it to a working template in `examples/` to spot differences.

---

## 8. Where to Go Next

If you’re comfortable importing and exporting templates, you can:

- Explore the **`examples/`** folder and see how different layouts are built.
- Look at **`clients/Bob/`** or **`clients/Tom/`** as simple client setups.
- Skim the main README and follow the **"Where to Go Next"** steps.

You don’t have to learn everything at once. Start by **importing a template**, poking around in Elementor, and then exporting your own version back into this repo.

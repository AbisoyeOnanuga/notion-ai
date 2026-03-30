# Hub page — build recipe (copy-paste)

For **Life-OS · Household** when your data lives in **`groceries_db` (kitchen)** and **`appliances_spaces`** (assets, repair, projects-style tags). Your child pages (**Repair**, **Appliances & spaces**, **Groceries**, **Projects**) hold the deep views; the **hub** is the **front door**: orientation, principles, links, and a **small set** of embedded views so the page feels alive without duplicating everything.

---

## 1. Page chrome (30 seconds)

| Setting | Suggestion |
|---------|------------|
| **Title** | `Life-OS · Household` or `Household hub` |
| **Icon** | 🏠 (or 🧭) |
| **Cover** | Unsplash search: `minimal home` or `kitchen light` |

---

## 2. Block order — top to bottom

Build **in this order** (Notion flows top-down). Type `/` to insert each block type.

### A. Heading 1

```text
Household command center
```

### B. One-sentence intro (paragraph)

```text
This workspace is the single source of truth for our home: what we own, what needs fixing, what we’re running low on, and what we’re planning to replace. *If it matters for the house, it lives here — not in chat threads or memory.*
```

(Add **bold** on “single source of truth” if you like.)

### C. Callout #1 — icon 💡 (idea / purpose)

**How to add:** `/callout` → choose icon 💡 → paste:

```text
Life-OS uses this Notion workspace as ground truth for demos and agents (e.g. Notion MCP). Keep dates and stock counts current so searches and automations stay trustworthy.
```

### D. Callout #2 — icon ⚠️ (guardrail)

```text
Agents can read and update pages you can access. Don’t paste passwords, full account numbers, or photos of IDs here — use placeholders or a password manager.
```

### E. Heading 2

```text
How we use this hub
```

### F. Toggle (parent block)

**How to add:** `/toggle` → title line:

```text
Open for navigation and rules
```

**Inside the toggle**, add **bullets** (press Enter after the toggle title, then Tab to nest):

```text
• Repair & dates → subpage **Repair** (calendar + table from `appliances_spaces`).
• Inventory & rooms → **Appliances & spaces** (tables, gallery by room, board by type).
• Pantry & restock → **Groceries** (`groceries_db` consumables).
• Replace / upgrade pipeline → **Projects** (filtered list: condition or tag = replace).
• The databases are canonical; these pages are *views* — edit rows in any linked view, not duplicate lists elsewhere.
```

(Replace `**Repair**` with your exact page titles, or use `@` page mentions in Notion instead of bold names.)

### G. Toggle #2 — “Principles”

Title:

```text
Household principles (short)
```

Inside:

```text
• Stock and warranties beat guesswork — update after every big shop or service call.
• One row per asset or consumable; use properties instead of free-floating notes when possible.
• “Replace” items stay visible in Projects until they’re done, not forgotten in a message.
```

### H. Divider

`/divider`

### I. Heading 2

```text
This week at a glance
```

### J. Two columns

**How:** `/columns` → choose 2 columns.

**Column left — Heading 3** `Repairs & dates`

Under it, **one short paragraph** (not empty):

```text
Next service windows and anything overdue show up on **Repair**. Skim the calendar before the weekend.
```

Then: **Link to page** `@Repair` (or your exact page name).

**Optional:** Embed **one** linked database view here — e.g. `appliances_spaces` filtered to **Due / next service** in the next 14 days OR **Status** = overdue (adjust to your property names). Keep it **narrow** (5–10 rows max).

**Column right — Heading 3** `Groceries & restock`

```text
Check **Groceries** before a store run. Anything below par level or nearing “good till” should be visible in the consumables table.
```

Link: `@Groceries`.

**Optional:** Embed a **linked view** of `groceries_db`: filter **Stock** low or **Good till** within 7 days (if those properties exist).

### K. Divider

### L. Heading 2

```text
Jump to areas
```

### M. Bulleted list of page links

Use **@ mentions** so they become links:

```text
→ Repair — calendar + full table for `appliances_spaces`
→ Appliances & spaces — gallery by room, board by type
→ Groceries — kitchen consumables (`groceries_db`)
→ Projects — replace pipeline (filtered `appliances_spaces`)
```

### N. Divider

### O. Heading 2

```text
Databases (source of truth)
```

### P. Short paragraph + inline code

```text
Rows live in two databases: `groceries_db` and `appliances_spaces`. Child pages only show filtered views — edit here or there, same data.
```

### Q. Embedded linked views (hub quality bar)

Embed **2–4** **small** linked views (not full duplicates of every subpage):

| # | Source | Suggested view | Why on hub |
|---|--------|----------------|------------|
| 1 | `appliances_spaces` | **Table**: 5 rows, sorted by next repair/service date; hide rarely used columns | Agent can answer “what’s next?” |
| 2 | `groceries_db` | **Table** or **Board** by `Where` (pantry / fridge) | Shows breadth |
| 3 | `appliances_spaces` | **Board** by Type OR **Gallery** by room — pick **one** mini view | Visual variety |
| 4 | Optional | Link only to **Projects** page instead of a third embed if the hub feels crowded | Clarity |

**Rule:** If the hub scrolls forever, **remove** embeds and keep **links + one** “at a glance” embed per column section.

---

## 3. Subpages you still add (high impact, low effort)

| Subpage | Purpose | Minimum content |
|---------|---------|-----------------|
| **Ops · Runbook** (or **Home ops**) | Procedures MCP can fetch | 3× **Heading 2**: Emergency shutoffs · Who to call · Seasonal checklist. Under each, a **toggle** with 2–3 bullets (can be placeholders). |
| **Reference · Utilities** (optional) | Links-only | Simple table: Utility · Portal URL · “Billing day” column with `—` |

Add **both** under the hub: `/` → **Sub-page** from hub, or create pages and drag under hub in sidebar.

**Link from hub:** In “Jump to areas” or a new **Heading 2** `Docs`, add one line:

```text
Ops runbook — procedures and contacts (not in the databases).
```

---

## 4. What not to put on the hub

- **Long tables** that duplicate **Repair** or **Groceries** — link + thin embed only.
- **Every** gallery/board — those belong on **Appliances & spaces**; hub gets **one** teaser view.
- **Raw seed data dumps** — keep seed data in DB rows; hub stays **interpretive**.

---

## 5. Winning bar checklist (aligned with STRATEGY)

- [ ] Hub has **2+ callouts**, **2+ toggles**, **columns**, **dividers**, **@ page links**.
- [ ] **Intro** states purpose in one breath; **principles** tie behavior to data quality (good for MCP demos).
- [ ] **Embedded linked views** (at least 2) from `groceries_db` / `appliances_spaces`.
- [ ] At least **one** subpage with **non-database** text (**Ops · Runbook**) so `notion-fetch` returns prose + structure.
- [ ] Property names stable — agent updates **Due**, **Stock**, **Condition**, not shadow copies.

---

## 6. If something still feels empty

Add a **Quote** block under the intro (fake “house rule”):

```text
“We don’t argue about whether the filter was changed — we check Notion.”
```

Or a **to-do** block (3 items) for **human** weekly rituals:

```text
☐ Skim Repair calendar for the next 7 days  
☐ Update grocery stock after shopping  
☐ Move one “replace” item forward in Projects  
```

That gives the hub **action** without new databases.

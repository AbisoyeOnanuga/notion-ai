# Life-OS · Household — Notion ground-truth blueprint

Use this as a **build recipe** in your workspace. Notion has no “import this file as pages” from here—you recreate the hierarchy, then paste blocks where noted.

**Goal:** Rich, realistic household data: **databases** (with relations), a **hub page** with varied blocks (headers, callouts, toggles, columns, dividers), and **detail pages** that prove formatting depth.

---

## Tutorials and templates (start here if you prefer video / duplicate)

| Resource | What it is |
|----------|------------|
| [How to build a Notion system for home maintenance and repairs](https://createwithnotion.com/how-to-build-a-notion-system-for-tracking-your-home-maintenance-tasks-and-repairs/) | Step-by-step article: rooms, checklists, due dates, structure. |
| [How to create a maintenance dashboard in Notion](https://www.thebricks.com/resources/how-to-create-a-maintenance-dashboard-in-notion) | Dashboard-style setup and dynamic views. |
| [Notion — Home Maintenance Tracker (template)](https://www.notion.com/templates/home-maintenance-tracker-543) | Marketplace template you can duplicate and **reshape** to match our schema. |
| [Notion — Household Maintenance (template)](https://www.notion.com/templates/household-maintenance) | Another marketplace starting point. |
| [Notion — Databases](https://www.notion.com/help/intro-to-databases) | Official: views, properties, relations (reference while building). |

Duplicating a marketplace template, then **deleting extras** and **renaming** to match the schema below is often faster than a blank page.

---

## 1. Page tree (top level)

Create a **teamspace or private parent** (your choice), then:

```text
Life-OS · Household                    ← Hub (document + linked views)
├── Ops · Runbook                      ← Long-form doc (procedures, contacts)
├── Reference · Home & vendors         ← Wiki-style subpages OK
└── [Databases live here or as children]
    ├── DB · Assets (equipment & spaces)
    ├── DB · Maintenance & chores
    ├── DB · Consumables & restock
    └── DB · Projects & seasonal
```

**Tip:** In the hub, use a **large emoji** page icon (e.g. 🏠) and optionally a **cover** (Unsplash: “home interior” or “tools”) so the page looks intentional, not default.

---

## 2. Hub page (`Life-OS · Household`) — block mix (not bland text)

**Step-by-step copy, toggles, columns, and embed rules (your 2-DB setup):** [HUB_PAGE_BUILD.md](./HUB_PAGE_BUILD.md).

Build the hub with **several Notion block types**:

| Block type | Where / why |
|------------|----------------|
| **Heading 1** | Title feel: “Household command center” |
| **Callout** (💡 or ⚠️) | One line: “Source of truth for Life-OS MCP demos — edit dates to stay current.” |
| **Columns** (2 cols) | Left: “This week”; Right: “Quick links” |
| **Bulleted list** | 3–5 principles (“If it’s not in Notion, it doesn’t exist”) |
| **Toggle** | “How we use this hub” → nested bullets |
| **Divider** | Between narrative and databases |
| **Synced block** (optional) | Repeat a warning on another page |
| **Link to page** | To `Ops · Runbook` |
| **Linked database views** | See §4 — embed **4 filtered views** (not one giant table) |

Add **bold**, *italic*, and `inline code` for one or two terms (e.g. `warranty`, `RMA`) so paragraphs aren’t uniform.

---

## 3. Document: `Ops · Runbook` (depth without a database)

**What it is vs your DBs, and full copy-paste sections:** [OPS_RUNBOOK.md](./OPS_RUNBOOK.md).

Purpose: **Procedures and narrative** MCP can quote or summarize.

Suggested sections (use **Heading 2** + **Toggle** per section):

1. **Emergency shutoffs** — water, gas, breaker panel locations (placeholder addresses OK).
2. **Vendor playbook** — “When HVAC acts up → check filter → then call …”
3. **Seasonal rhythm** — Q1–Q4 bullets (even if high-level).

**Formatting variety:**

- **Numbered list** for ordered steps.
- **To-do** checkboxes for “annual tasks” (leave some unchecked).
- **Quote** block for a fake note from a home inspector.
- **Table** (simple block table): Column A “System”, Column B “Last serviced”, Column C “Next due”.

---

## 4. Databases — schemas (property types)

Use **consistent Status options** across DBs where it makes sense: `Idea` · `Planned` · `In progress` · `Done` · `Blocked`.

### 4.1 `DB · Assets (equipment & spaces)`

| Property | Type | Example values |
|----------|------|----------------|
| Name | Title | “HVAC — main unit”, “Water heater”, “Garage” |
| Type | Select | `Appliance` · `System` · `Room/zone` · `Vehicle` |
| Location | Text | “Basement”, “Roof” |
| Install / purchase date | Date | |
| Warranty expires | Date | |
| Manual / receipt | URL or Files | link to Drive or empty |
| Notes | Text | |
| **Related maintenance** | Relation → `DB · Maintenance & chores` | |
| **Related consumables** | Relation → `DB · Consumables & restock` | optional |

**Views:** Table (all), **Gallery** filtered to `Type = Room/zone` (visual variety), **Board** by `Type`.

### 4.2 `DB · Maintenance & chores`

| Property | Type | Example values |
|----------|------|----------------|
| Task | Title | “Replace HVAC filter”, “Clean dryer vent” |
| Status | Status | see above |
| Priority | Select | `P1` · `P2` · `P3` |
| Due | Date | |
| Recurrence | Text | “Every 90 days” (Notion recurring reminders if on your plan) |
| Category | Multi-select | `HVAC` · `Plumbing` · `Safety` · `Exterior` · `Seasonal` |
| Est. cost | Number (USD) | |
| Owner | Person | you |
| **Asset** | Relation → Assets | |
| Last completed | Date | |
| Evidence | URL | photo link placeholder |

**Views:** **Calendar** (by Due), **Board** (by Status), filtered **Table** “Overdue” (Due < today AND Status ≠ Done).

### 4.3 `DB · Consumables & restock`

| Property | Type |
|----------|------|
| Item | Title |
| Where stored | Select | `Pantry` · `Garage` · `Laundry` |
| Par level | Number |
| On hand | Number |
| Reorder link | URL |
| **Linked asset** | Relation → Assets (optional) |

**View:** **Table** sorted by “On hand” ascending (simulate “running low”).

### 4.4 `DB · Projects & seasonal` (complexity / narrative)

| Property | Type |
|----------|------|
| Project | Title |
| Window | Select | `Spring 2026` · `Summer 2026` · Ad-hoc |
| Status | Status | |
| Budget | Number | |
| Scope | Text | multi-line OK |

Embed **one timeline** view if available in your plan, else **Board** by `Window`.

---

## 5. Seed data (realistic, MCP-friendly)

Add **at least:**

- **8–12** maintenance rows spanning categories (HVAC, safety, exterior, appliances).
- **4–6** assets (mix of appliance + one “Garage” zone + vehicle if you use it).
- **5+** consumables with **unequal** on-hand vs par (so “low stock” is real).
- **2–3** projects (e.g. “Deck stain”, “Gutter guards”, “Pantry reorganize”).

Use **specific titles** (“Replace MERV-13 filter — furnace”) not “Task 1”.

---

## 6. `Reference · Home & vendors` (optional wiki depth)

Subpages or toggles:

- **Utilities** — account numbers as `***` placeholders; table of provider / portal URL.
- **Warranty drawer** — list of brands + support URLs.

This gives **link-rich** pages for `notion-search` / `notion-fetch` tests.

---

## 7. What “done” looks like for Phase 1

- [ ] Hub page uses **multiple block types** + **linked DB views**.
- [ ] At least **two** databases related (**Assets** ↔ **Maintenance**).
- [ ] **Calendar** or **Board** view** exists and looks populated.
- [ ] **Ops · Runbook** has structured sections (not a single paragraph).
- [ ] Seed data is **specific enough** that an agent can answer “what’s due next week?” from properties.

---

## 8. After you build

1. Run through [Notion MCP supported tools](https://developers.notion.com/guides/mcp/mcp-supported-tools): **search** for “HVAC”, **fetch** the hub page, **update** one `Due` date.
2. Adjust property names if MCP examples in your client expect certain wording—**keep names stable** after Gemini integration starts.

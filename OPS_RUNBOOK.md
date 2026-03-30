# Ops · Runbook — what it is (and what it is not)

## What it is

An **Ops runbook** is **procedural memory**: *what to do when something happens*, *who to call*, *where critical things are*, and *how we run the household* — in **sentences and checklists**, not database rows.

| Your **databases & views** | **Runbook** |
|----------------------------|-------------|
| **State:** this asset, this due date, this stock count | **Process:** “Filter won’t reset → try A, then B, then call …” |
| **Repair** page / calendar | **When to escalate** vs DIY, and **numbers** you don’t want in every DB row |
| **Appliances & spaces** | **Room-by-room quirks** (breaker label, shutoff valve) |
| **Groceries** | **Food safety rule of thumb** (optional 5 lines), not your item list |

**Why judges / MCP care:** `notion-fetch` on a DB returns rows; fetch on a **runbook page** returns **structured prose** — good for “summarize our emergency plan” or “what do we do before calling a tech?” demos.

---

## Glossary — steps, policy, short ops, habit (how we use them here)

Use these **labels mentally** when you write; you don’t have to put the word “policy” in the Notion title.

| Label | Meaning | Example in this runbook |
|-------|---------|---------------------------|
| **Steps** | Ordered **do this, then this** — best as a **numbered list** | “Before you call a tech” — 1… 2… 3… |
| **Policy** | **When we decide X vs Y** — rules, thresholds, escalation | “If breaker trips twice, stop forcing resets.” “If power out > 4h, assume perishables at risk.” |
| **Short ops** | **Standing rules** for a zone (kitchen) — **bullets**, not your grocery rows | “Restock decisions use Groceries DB; this page doesn’t list SKUs.” |
| **Habit** | **Recurring human ritual** — **checkbox to-dos** or seasonal list | “Before heating season: check filter” (same idea yearly) |

**Mapping to your sections (suggested):**

| Section | Primary type |
|---------|----------------|
| Before you call a tech | **Steps** (+ a little **policy** in one line) |
| Emergency shutoffs | **Steps** inside toggles (location lines are facts; flood/gas lines are **policy**) |
| Vendor contacts | Reference table (not steps) |
| Kitchen & food | **Short ops** |
| Seasonal rhythm | **Habit** (checkboxes) |
| How this ties to Life-OS | One **policy** paragraph linking DB vs runbook |

---

## What it is not

- **Not** a second inventory — that stays in `appliances_spaces` and `groceries_db`.
- **Not** a duplicate of **Repair** — Repair is *what’s scheduled*; runbook is *how we behave when something breaks or alarms*.
- **Not** required to be long — **one page**, **4–6 sections**, enough to feel real.

---

## Build in Notion

1. Create subpage under hub: **`Ops · Runbook`** (or `Home ops`).
2. Icon 🔧 or 📋. Optional cover (tools / notebook).
3. Paste the blocks below top-down. Use **Heading 2** for each section; use **Toggle** inside a section if you want collapsible detail.

---

## Copy-paste content (edit placeholders)

### Opening paragraph (normal text)

```text
This page is how we *act*: emergencies, vendors, and recurring rituals. Numbers for assets and due dates live in the databases — this is the playbook when something goes wrong or it’s time for a seasonal pass.
```

---

### Heading 2 — `Before you call a tech`

```text
Before you call a tech
```

**Intro line** (paragraph under the heading):

```text
Follow these **steps** in order. Goal: fix the safe/obvious stuff first, or gather facts so the first hour of a service call isn’t wasted.
```

**Numbered list** (`/numbered` in Notion — these are **steps**):

```text
1. Open the matching row in **appliances_spaces** and confirm **make / model / location** (don’t re-type it here).
2. **Safety first:** sparking, burning smell, or gas odor → skip DIY; go to *Emergency shutoffs & safety* below.
3. **Power path:** find the right **breaker** or **GFCI**. Reset **once**. If it trips again immediately, **stop** — unplug obvious loads on that circuit and call a tech.
4. **Simple checks** (only if safe): plugged in, door closed, HVAC **filter access**, dryer **lint trap**, washer **supply valves on**.
5. **Evidence for the ticket:** photo of **nameplate**, **error code** or blink pattern, one-line **symptom** (“runs 2 min then stops”).
6. **Book the visit** — paste **confirmation #** into the asset row or Repair notes when you have it.
```

**Callout** (optional, 💡) — one-line **policy**:

```text
Policy: we don’t pay emergency rates for things a filter change or breaker check could fix — but we never risk injury to save money.
```

---

### Heading 2 — `Emergency shutoffs & safety`

```text
Emergency shutoffs & safety
```

**Intro line** (paragraph):

```text
**Policy:** if unsure, prioritize **people** over **stuff**. When in doubt, leave and call **emergency services** or the **utility** per local guidance.
```

**Toggle** title: `Water`

Inside toggle (numbered **steps** + your location):

```text
1. **Main house shutoff** (where water enters — often basement/crawl/utility wall): turn **clockwise** until firm; don’t over-torque.
2. **Single fixture:** under-sink or toilet **angle stops** — clockwise to close.
3. **Flooding:** shut main → if safe, cut **breaker** to wet areas → contain → photo for insurance → plumber.
4. **Our main shutoff:** [e.g. basement east wall — or **TBD, label after next walkthrough**].
```

**Toggle** title: `Power`

```text
1. **Main panel:** [e.g. garage / basement — or **TBD**].
2. **Policy:** breaker trips **twice** after reset → treat as faulted; don’t keep resetting — unplug loads on that circuit, then electrician.
3. **Kitchen:** know which **GFCI** protects counter outlets (often one button resets several plugs).
4. **Long outage:** see *Kitchen & food* for fridge; add a **Repair** note if you suspect surge damage.
```

**Toggle** title: `Gas` — use **only if you have gas**

```text
1. **Shutoff location:** [TBD — only operate if you know it’s correct].
2. **Policy:** **smell gas** → no switches, no fans; leave → call **utility emergency** or **911** from outside.
3. After gas work: **CO detectors** near sleeping areas — test seasonally.
```

**Toggle** title: `No gas` — use **instead of Gas** if all-electric

```text
All electric — water and electricity still don’t mix; don’t stand in water to touch the panel.
```

---

### Heading 2 — `Vendor & service contacts`

```text
Vendor & service contacts
```

**Simple table** (Notion table block):

| Role | Who | Phone / portal |
|------|-----|----------------|
| HVAC | [Company or TBD] | [number or “see email”] |
| Plumbing | … | … |
| Appliance warranty | [brand portal] | URL only |
| Landlord / HOA | … | if relevant |

**One line under table:**

```text
Prefer booking through the same channels we already use; paste **confirmation #** into the relevant `appliances_spaces` row or Repair notes, not only here.
```

---

### Heading 2 — `Kitchen & food (ops only)`

*(Type = **short ops** — standing rules; the **Groceries** page holds rows.)*

```text
Kitchen & food (ops only)
```

```text
• **Restock rhythm:** decisions use what’s low or expiring in **Groceries** — this section never duplicates the item list.
• **Policy (fridge / freezer):** power out **> 4 hours** → assume spoilage risk for perishables; after a purge, **update stock** in `groceries_db`.
• **Policy (smoke/CO):** test detectors when **DST** changes; note battery swaps in **Repair** if you track them there.
```

---

### Heading 2 — `Seasonal rhythm (household)`

*(Type = **habit** — recurring checkboxes you run the same way each year.)*

```text
Seasonal rhythm (household)
```

**To-do block** (checkboxes):

```text
☐ Spring: exterior visual pass (roof line, gutters) — file follow-ups in Repair / Projects  
☐ Before heating season: replace / check furnace filter (see `appliances_spaces` HVAC row)  
☐ Before cooling season: clear outdoor unit clearance  
☐ Year-end: skim **Projects** for stalled “replace” items  
```

---

### Heading 2 — `How this ties to Life-OS`

```text
How this ties to Life-OS
```

```text
**Databases** = inventory and schedules. **This page** = judgment under pressure and habits. Agents using Notion MCP should read databases for facts and this page for *what we do with those facts*.
```

---

## Link from hub

On the hub, add under “Jump to areas” or a small **Docs** line:

```text
Ops · Runbook — emergencies, shutoffs, vendors, seasonal habits (procedures, not inventory).
```

---

## Done when

- [ ] Runbook is **one page** of prose + toggles + one table + optional to-dos.
- [ ] **No** duplicate of full appliance or grocery lists.
- [ ] **Before you call a tech** uses a **numbered list** (steps), not only loose bullets.
- [ ] **Emergency shutoffs** has **Water / Power / Gas or No gas** toggles with **policy** in the intro line.
- [ ] **Kitchen** = short ops bullets; **Seasonal** = habit checkboxes.
- [ ] At least **Emergency** + **Before tech** + **Vendors** filled (`TBD` placeholders OK).

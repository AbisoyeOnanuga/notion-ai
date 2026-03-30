# Notion × MLH - MCP challenge

Work in progress: scope, requirements, and the concrete problem to solve are still being defined.

## The problem

Your work is scattered: code in an editor, plans in docs, tasks in messages, email, and calendar.

Most AI tools sit outside all of it, guessing what you actually want. There is a better approach: when AI can use your context and run across the tools you use every day—like Notion.

## The challenge

[Notion](https://www.notion.so/) is partnering with [Major League Hacking](https://mlh.io/) to challenge hackers around the globe:

**Build the most impressive system or process using Notion MCP.**

It can span any field: engineering, sales, finance, and more. The goal is strong integrations—not a one-off script only you would use.

### Inspiration (from the brief)

1. Build an iMessage assistant that has access to your Notion workspace.
2. Automate a task in your browser, using a Notion page.
3. Track your feature backlog in Notion, and let an agent take the first pass at it.

## This repository

**Life-OS** — a Notion-backed agent for scattered life admin, demonstrated first on a **household** wedge (maintenance, rhythm, home ops). **Team:** MCP-master. The build is meant to serve the **Notion ecosystem** broadly, not a one-off personal script.

**Start here after Notion is built:** [STEP_BY_STEP.md](./STEP_BY_STEP.md) — install Gemini CLI, connect Notion MCP, OAuth, verification prompts, demo workflows.

**Strategy** (judging, roadmap): [STRATEGY.md](./STRATEGY.md).

**MCP + agent** (background + links): [MCP_AGENT_SETUP.md](./MCP_AGENT_SETUP.md).

### Demo video vs Part D / Part E

| Piece | What it is | Use in video? |
|--------|------------|----------------|
| **Part D** ([STEP_BY_STEP.md](./STEP_BY_STEP.md)) | Smoke test: search, fetch, one write — proves MCP works. | Optional clip or skip if time is tight; you already proved it. |
| **Part E** | Life-OS workflows (weekend prep + groceries) with `prompts/LIFE_OS_SYSTEM.md` — **this is the product**. | **Yes — lead with this.** Show Gemini CLI calling Notion tools, then **switch to Notion** so the viewer sees real pages/DBs. |

**Interface:** The challenge does **not** require a custom web or mobile UI. **Gemini CLI + Notion MCP** is a valid submission: the “agent” is Gemini using MCP tools against your workspace. A separate UI is optional polish, not required to win.

### README / submission checklist

- [ ] **One-liner:** what Life-OS is (Notion as ground truth + Gemini via MCP for household ops).
- [ ] **How to run:** Node 20+, `npm install -g @google/gemini-cli`, clone repo, `cd` into repo (uses [`.gemini/settings.json`](./.gemini/settings.json)), `gemini` → `/mcp auth notion`.
- [ ] **Link** [STEP_BY_STEP.md](./STEP_BY_STEP.md) for full setup.
- [ ] **Demo script (3–5 min):** problem (scattered life admin) → CLI: one **Part E** workflow → Notion browser: show updated comment or data.
- [ ] **Team:** MCP-master; optional: embed or link screen recording.

---

*Challenge context: Notion MCP + MLH hackathon.*

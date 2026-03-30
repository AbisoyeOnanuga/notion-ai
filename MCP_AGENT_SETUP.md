# Phase 2 — Notion MCP, Gemini, and Life-OS agent

**Prerequisite:** Notion household hub, databases, runbook, and seed data are done ([STRATEGY.md](./STRATEGY.md) Phase 1).

This doc is the execution order after that: **connect MCP → verify tools → define agent behavior → optional second integration.**

---

## 1. What you are wiring

| Layer | Role |
|--------|------|
| **Notion workspace** | Ground truth (pages + DBs). |
| **Notion MCP** (`https://mcp.notion.com/mcp`) | Hosted tools: search, fetch, create/update pages, etc. ([supported tools](https://developers.notion.com/guides/mcp/mcp-supported-tools)). |
| **Gemini** | MCP **client** that invokes those tools and reasons over results. |
| **Life-OS “agent”** | Your **prompts + policies + optional scripts** that tell Gemini *when* to call which tools (household workflows). |

Notion MCP uses **OAuth** as your user — same visibility as you in Notion ([get started](https://developers.notion.com/guides/mcp/get-started-with-mcp), [FAQ](https://developers.notion.com/guides/mcp/get-started-with-mcp)).

---

## 2. Connect Notion MCP (workspace + OAuth)

Do **both** if your client allows: register intent in Notion, then connect from the client.

1. In **Notion** (desktop or web): **Settings** → **Connections** → **Notion MCP** — pick your tool and complete OAuth if prompted ([Notion Help](https://www.notion.com/help/notion-mcp)).
2. In your **Gemini surface** (see §3), add the server URL **`https://mcp.notion.com/mcp`** (Streamable HTTP) and complete OAuth when the client opens the flow.

**Official endpoint reference:** [Connecting to Notion MCP](https://developers.notion.com/guides/mcp/get-started-with-mcp).

**Security:** [MCP security best practices](https://developers.notion.com/guides/mcp/mcp-security-best-practices).

---

## 3. Gemini — pick a surface and attach MCP

Not every Gemini UI exposes MCP the same way. Use **one** path that your environment actually supports; verify tools appear before you script demos.

| Surface | What to do |
|---------|------------|
| **Gemini CLI** | Configure remote MCP with **`httpUrl`**. Official doc: [MCP servers with the Gemini CLI](https://google-gemini.github.io/gemini-cli/docs/tools/mcp-server.html). Add to your Gemini CLI `settings.json` under `mcpServers` (user or project scope per CLI docs). Example shape: |

```json
{
  "mcpServers": {
    "notion": {
      "httpUrl": "https://mcp.notion.com/mcp"
    }
  }
}
```

Restart the CLI; complete OAuth when prompted. Set `"trust": true` only if you understand the CLI’s trust model for that server.

| **Google Antigravity** | Notion docs recommend a **custom** MCP server URL (not deprecated packages): same URL `https://mcp.notion.com/mcp` — follow [Antigravity custom MCP](https://developers.notion.com/guides/mcp/get-started-with-mcp) (linked from Notion’s get-started page). |
| **Gemini in browser / other** | If MCP is not available, use **Gemini CLI** or **Cursor + Notion MCP** for development/demo and state that in the README — still valid for the hackathon if Notion MCP is clearly the integration under test. |

**Custom client builders:** [Build an MCP client (Notion)](https://developers.notion.com/guides/mcp/build-mcp-client) (OAuth details).

---

## 4. Verify MCP (before “agent”)

Run these in order; all should touch **your** Life-OS content.

| # | Goal | Example instruction to the model |
|---|------|-------------------------------------|
| 1 | **Search** | “Search Notion for `Life-OS` or `household` and list matching page titles.” |
| 2 | **Fetch** | “Fetch the household hub page by URL” (paste your page URL) **or** by ID from search results. |
| 3 | **Fetch DB** | “Fetch the `appliances_spaces` database (or groceries DB) and summarize its schema / columns.” |
| 4 | **Read runbook** | “Fetch **Ops · Runbook** and summarize the emergency water steps in one paragraph.” |
| 5 | **Write (controlled)** | “Add a short comment on the hub page: `MCP verification [date]`” **or** update a non-critical property on a **test** row — then confirm in Notion UI. |

If step 5 is scary, use a **dedicated test page** or test row labeled `MCP_TEST`.

**Rate limits:** avoid parallel search spam ([supported tools](https://developers.notion.com/guides/mcp/mcp-supported-tools)).

---

## 5. Life-OS agent = behavior on top of verified tools

The “agent” is **not** a separate binary unless you build one. For the hackathon, it is usually:

1. **System instructions** (persistent): “You are Life-OS. Notion is source of truth. Prefer `notion-search` then `notion-fetch`; confirm destructive updates with the user.”
2. **Workflow prompts** (saved / scripted demo):

| Demo | Flow |
|------|------|
| **Weekend prep** | Search appliances due in next 7 days → list → offer to add a comment or status on the row. |
| **Pantry check** | Query groceries DB (via fetch + schema) → list items below par or expiring soon → suggest shopping bullets as a **temporary** block (or comment) for human copy. |
| **Replace pipeline** | Search Projects / replace filter context → summarize stalled items from fetched pages. |

3. **Human in the loop:** Hosted MCP is user-OAuth — keep approval for bulk updates ([get started FAQ](https://developers.notion.com/guides/mcp/get-started-with-mcp)).

Optional: save prompts in this repo as `prompts/` (e.g. `weekend-prep.md`) for reproducible judging.

---

## 6. After MCP works — Phase 3 (from STRATEGY)

| Order | Task |
|-------|------|
| 1 | **Second integration** (optional): e.g. Gmail or Calendar → summarize into Notion — only if one end-to-end path is demoable. |
| 2 | **Demo script**: 3–5 minutes, screen recording: problem → Gemini + Notion MCP → visible Notion change. |
| 3 | **README / submission**: embed links to Notion template gallery or describe duplication steps if you publish a template. |

---

## 7. Checklist

- [ ] OAuth completed; MCP tools visible in the chosen Gemini (or fallback) client.
- [ ] Search + fetch + one write verified against Life-OS pages/DBs.
- [ ] At least **three** saved agent prompts or one system prompt + three one-shot demos documented.
- [ ] Rate limits and destructive actions acknowledged (confirm before bulk edits).

---

## Links (quick)

| Topic | URL |
|--------|-----|
| Notion MCP get started | https://developers.notion.com/guides/mcp/get-started-with-mcp |
| Supported tools | https://developers.notion.com/guides/mcp/mcp-supported-tools |
| Gemini CLI MCP | https://google-gemini.github.io/gemini-cli/docs/tools/mcp-server.html |
| Notion MCP (Help) | https://www.notion.com/help/notion-mcp |

# Phase 2 — Notion MCP, Gemini, and Life-OS agent

**Prerequisite:** Notion household hub, databases, runbook, and seed data are done ([STRATEGY.md](./STRATEGY.md) Phase 1).

**Linear checklist (do this in order):** [STEP_BY_STEP.md](./STEP_BY_STEP.md).

This doc is background and links: **connect MCP → verify tools → define agent behavior → optional second integration.**

---

## How this maps to the challenge (MLH × Notion)

The challenge is to build an **impressive system or process using Notion MCP** — i.e. your **workspace stays the source of truth**, and an AI **uses Notion’s hosted MCP tools** (search, fetch, update, etc.) to read and change that workspace, not to guess from a blank chat.

That implies three pieces:

1. **Notion** — your Life-OS data (you already built this).
2. **Notion MCP server** — hosted by Notion at **`https://mcp.notion.com/mcp`** ([Connecting to Notion MCP](https://developers.notion.com/guides/mcp/get-started-with-mcp)).
3. **An MCP client** — something that speaks the MCP protocol, runs **Gemini**, and **calls those tools** when the model decides to.

Gemini is **not** “wrong” because it is not in Notion’s one-click gallery. The gallery highlights Cursor, Claude, ChatGPT, etc. ([get started](https://developers.notion.com/guides/mcp/get-started-with-mcp)); **any compliant MCP client** can connect to the same URL. Your submission stays valid if you clearly show **Gemini (via Gemini CLI or another supported path) + Notion MCP + your Life-OS workflow.**

```text
[ You ] → [ Gemini — model + tool caller ]
              ↓ MCP (OAuth)
         [ https://mcp.notion.com/mcp ] → [ Your Notion workspace ]
```

---

## 1. What you are wiring

| Layer | Role |
|--------|------|
| **Notion workspace** | Ground truth (pages + DBs). |
| **Notion MCP** (`https://mcp.notion.com/mcp`) | Hosted tools: search, fetch, create/update pages, etc. ([supported tools](https://developers.notion.com/guides/mcp/mcp-supported-tools)). |
| **Gemini** | The **model** inside an MCP-capable **client** (recommended: **Gemini CLI**) that invokes those tools and reasons over results. |
| **Life-OS “agent”** | Your **prompts + policies** that tell Gemini *when* to call which tools (household workflows). |

Notion MCP uses **OAuth** as your user — same visibility as you in Notion ([get started FAQ](https://developers.notion.com/guides/mcp/get-started-with-mcp)).

---

## 2. Connect Notion MCP (workspace + OAuth)

1. In **Notion**: **Settings** → **Connections** → **Notion MCP** — complete any connection flow if your client is listed ([Notion Help — Notion MCP](https://www.notion.com/help/notion-mcp)).
2. In your **MCP client** (Gemini CLI): point at **`https://mcp.notion.com/mcp`** and complete OAuth when the client opens the browser flow (see §3).

**Security:** [MCP security best practices](https://developers.notion.com/guides/mcp/mcp-security-best-practices).

---

## 3. Gemini + Notion MCP — supported ways (from official docs)

### Why this feels “custom”

Notion documents **first-class** setup for tools like Cursor and Claude ([Connecting to Notion MCP](https://developers.notion.com/guides/mcp/get-started-with-mcp)). **Gemini** is not listed there as a one-click connector today, but **Google’s own Gemini CLI** is an MCP client that supports **remote** servers over **Streamable HTTP** via **`httpUrl`**.

**Official references:**

| Topic | Documentation |
|--------|----------------|
| **Gemini CLI — MCP servers** (transport types, `httpUrl`, OAuth) | [MCP servers with the Gemini CLI](https://google-gemini.github.io/gemini-cli/docs/tools/mcp-server.html) · [Source on GitHub](https://github.com/google-gemini/gemini-cli/blob/main/docs/tools/mcp-server.md) |
| **Notion — hosted MCP URL + OAuth expectations** | [Connecting to Notion MCP](https://developers.notion.com/guides/mcp/get-started-with-mcp) |
| **Notion — build your own MCP client** (if you outgrow the CLI) | [Integrating your own MCP client](https://developers.notion.com/guides/mcp/build-mcp-client) |
| **Gemini CLI — configuration file location** | [Gemini CLI configuration](https://google-gemini.github.io/gemini-cli/docs/get-started/configuration.html) |

### Path A (recommended): Gemini CLI + `httpUrl` + Notion OAuth

1. Install and use **[Gemini CLI](https://google-gemini.github.io/gemini-cli/)** (terminal).
2. Edit **`settings.json`** and add under `mcpServers` (per [MCP servers doc](https://google-gemini.github.io/gemini-cli/docs/tools/mcp-server.html)):

```json
{
  "mcpServers": {
    "notion": {
      "httpUrl": "https://mcp.notion.com/mcp"
    }
  }
}
```

3. **OAuth:** The CLI supports **OAuth 2.0 for remote MCP servers** over SSE or HTTP. For servers that support discovery, it can detect **401**, discover endpoints, open a **browser**, and store tokens (see **“OAuth support for remote MCP servers”** in the same doc). Requirements include a local browser and redirect on **`http://localhost:7777/oauth/callback`** (documented there — headless SSH-only environments may not work).
4. In the CLI, use **`/mcp auth`** to list servers needing auth and authenticate — e.g. `/mcp auth notion` (see **“Managing OAuth authentication”** in [MCP servers with the Gemini CLI](https://google-gemini.github.io/gemini-cli/docs/tools/mcp-server.html)).
5. Use **`/mcp`** to confirm Notion tools are listed.

Set `"trust": true` only if you understand the CLI’s trust model; default is to confirm tool calls.

### Path B: Google Antigravity (if you use it)

Notion’s [get started](https://developers.notion.com/guides/mcp/get-started-with-mcp) mentions **Antigravity** with a **custom** MCP URL (`https://mcp.notion.com/mcp`), not the deprecated `notion-mcp-server` package. Follow Google’s Antigravity MCP instructions and paste the same URL.

### Path C: Truly custom (code)

If you need a **small app** (e.g. web UI + Gemini API + MCP): implement an MCP client that completes **OAuth 2.0 Authorization Code with PKCE** against Notion’s MCP, as in [Integrating your own MCP client](https://developers.notion.com/guides/mcp/build-mcp-client). That is more work than Path A but is the “by the book” integration pattern.

### What usually does *not* work as-is

- **gemini.google.com** chat in the browser — there is **no** universal “paste Notion MCP URL” in standard consumer Gemini UI comparable to Cursor’s MCP panel. Use **Gemini CLI** (or Path C) for a demoable Notion MCP + Gemini stack.

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

**If the model says it cannot write because `notion-update-page` needs `properties`:** that usually means it mixed up **property** updates (database columns) with **body** or **note** updates. For additive lists or notes, use **`notion-create-comment`**. For body edits, use the **content** command shape for `notion-update-page` after **`notion-fetch`**. Details: `prompts/LIFE_OS_SYSTEM.md`.

---

## 5. Life-OS agent = behavior on top of verified tools

The “agent” is **not** a separate binary unless you build one. For the hackathon, it is usually:

1. **System instructions** (persistent): load **`prompts/LIFE_OS_SYSTEM.md`** (Life-OS rules, tool routing for writes, no manual copy-paste fallbacks).
2. **Workflow prompts** (saved / scripted demo):

| Demo | Flow |
|------|------|
| **Weekend prep** | Search appliances due in next 7 days → list → offer to add a comment or status on the row. |
| **Pantry check** | Query groceries DB (via fetch + schema) → list items below par or expiring soon → write shopping bullets with **`notion-create-comment`** on the hub or a target page (do not fall back to “copy manually”; see `prompts/LIFE_OS_SYSTEM.md`). |
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
| Notion — integrate your own MCP client (OAuth, PKCE) | https://developers.notion.com/guides/mcp/build-mcp-client |
| Supported tools | https://developers.notion.com/guides/mcp/mcp-supported-tools |
| Gemini CLI MCP | https://google-gemini.github.io/gemini-cli/docs/tools/mcp-server.html |
| Gemini CLI configuration (`settings.json`) | https://google-gemini.github.io/gemini-cli/docs/get-started/configuration.html |
| Gemini CLI (GitHub) | https://github.com/google-gemini/gemini-cli |
| Notion MCP (Help) | https://www.notion.com/help/notion-mcp |

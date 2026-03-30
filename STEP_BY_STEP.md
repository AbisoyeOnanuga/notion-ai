# Step-by-step: Notion MCP + Gemini (Life-OS) — from zero to demo

You already finished **Notion** (hub, DBs, runbook). This is the **exact order** to set up **Notion MCP** and **Gemini as the agent** for a strong hackathon story.

**Official references:** [Connecting to Notion MCP](https://developers.notion.com/guides/mcp/get-started-with-mcp) · [MCP servers with the Gemini CLI](https://google-gemini.github.io/gemini-cli/docs/tools/mcp-server.html) · [Gemini CLI configuration](https://google-gemini.github.io/gemini-cli/docs/get-started/configuration.html)

---

## Part A — Prerequisites (5 minutes)

| Step | Action |
|------|--------|
| A1 | **Node.js 20+** installed. Check: `node -v` (should be v20 or higher). If not: [nodejs.org](https://nodejs.org/) LTS. |
| A2 | **Default browser** works (OAuth opens a browser window). |
| A3 | **Notion** logged into the **same workspace** where Life-OS lives. |
| A4 | Optional: copy **one page URL** from your hub (you will paste it in a test prompt). |

---

## Part B — Install Gemini CLI (10 minutes)

Gemini in the **web chat** does not plug in Notion MCP the way this project needs. Use **Gemini CLI**: it is the documented MCP client for Gemini.

| Step | Action |
|------|--------|
| B1 | Open PowerShell or Terminal **as your normal user**. |
| B2 | Install globally (from [npm](https://www.npmjs.com/package/@google/gemini-cli)): `npm install -g @google/gemini-cli` |
| B3 | Verify: `gemini --version` (or `npx @google/gemini-cli --version` if you skip global install). |
| B4 | **Sign in to Gemini** per CLI prompts the first time you run `gemini`, **or** set `GEMINI_API_KEY` / `GOOGLE_API_KEY` as described in [Gemini CLI authentication](https://google-gemini.github.io/gemini-cli/docs/get-started/authentication.html). |

---

## Part C — Add Notion MCP to Gemini CLI (10 minutes)

| Step | Action |
|------|--------|
| C1 | This repo includes **`.gemini/settings.json`** with the Notion server. **OR** merge the same block into your **user** file: `%USERPROFILE%\.gemini\settings.json` (Windows) — see [configuration layers](https://google-gemini.github.io/gemini-cli/docs/get-started/configuration.html). |
| C2 | Confirm the server block matches (Streamable HTTP): `"httpUrl": "https://mcp.notion.com/mcp"` |
| C3 | From the **`notion-ai` project folder** (where `.gemini/settings.json` lives), run: `gemini` |
| C4 | In the CLI, run: `/mcp` — you should see MCP-related output; if Notion is not connected yet, continue to C5. |
| C5 | Authenticate Notion: `/mcp auth notion` (or `/mcp auth` and pick **notion**). Complete **OAuth** in the browser (Notion may ask which workspace). Per [Gemini CLI MCP docs](https://google-gemini.github.io/gemini-cli/docs/tools/mcp-server.html), OAuth uses a local redirect (e.g. `http://localhost:7777/oauth/callback`). |
| C6 | In **Notion** (optional but helpful): **Settings → Connections → Notion MCP** and confirm your environment is connected — [Notion Help](https://www.notion.com/help/notion-mcp). |

**If auth fails:** Close CLI, check firewall, retry `/mcp auth notion`. Read the **OAuth / browser** section in [MCP servers with the Gemini CLI](https://google-gemini.github.io/gemini-cli/docs/tools/mcp-server.html).

---

## Part D — Prove tools work (15 minutes) — “winner” bar

Do these **in order**. Approve tool calls when the CLI asks (keep `trust: false` until you understand the risk).

| Step | You type (natural language in Gemini CLI) | Pass criteria |
|------|-------------------------------------------|----------------|
| D1 | “Use Notion search to find pages about **Life-OS** or **household**. List titles.” | You see **notion-search** (or equivalent) run and real page titles from your workspace. |
| D2 | “Fetch my household hub page by this URL: [paste your hub URL].” | **notion-fetch** returns content from **your** page. |
| D3 | “Fetch the **Ops · Runbook** page and summarize the water emergency steps in 3 bullets.” | Answer matches **your** runbook text. |
| D4 | “Fetch the appliances database (or name your `appliances_spaces` DB) and list property names.” | Schema/properties appear — proves DB access. |
| D5 | **One safe write:** “Add a **comment** on the hub page: `MCP OK — [today’s date]`” **or** update a **test** row’s non-critical property. | You see the change in the **Notion** UI. |

**Rate limits:** do not fire dozens of searches at once ([Notion MCP supported tools](https://developers.notion.com/guides/mcp/mcp-supported-tools)).

---

## Part E — Define the “agent” (30 minutes)

The **agent** is **Gemini + your instructions**, not a second app.

| Step | Action |
|------|--------|
| E1 | Copy `prompts/LIFE_OS_SYSTEM.md` (in this repo) into the CLI as a **first message** or add it to CLI context if you use `GEMINI.md` / project context ([configuration](https://google-gemini.github.io/gemini-cli/docs/get-started/configuration.html)). |
| E2 | Run **Workflow 1 — Weekend prep:** “Using only Notion MCP: list maintenance or repair items due in the next 14 days from my databases; then suggest one **comment** I could add to the highest-priority row.” |
| E3 | Run **Workflow 2 — Groceries:** “Using Notion MCP: identify consumables that are low or near expiry from my groceries database and output a **shopping shortlist** in chat (do not invent items not in Notion).” |
| E4 | Save **screenshots or a short terminal transcript** for the submission / demo. |

---

## Part F — What makes the submission look “complete”

| Deliverable | Why judges care |
|-------------|-----------------|
| **Visible Notion change** in recording | Proves MCP is not fake. |
| **Multi-step tool use** (search → fetch → update) | Technical complexity. |
| **Life-OS story** in README | Originality + clarity. |
| **Honest setup section** | Gemini CLI + Notion MCP URL + OAuth — reviewers can reproduce. |

---

## Part G — Optional next (after the core works)

| Step | Action |
|------|--------|
| G1 | One **second integration** (e.g. Gmail or Calendar) only if you have a **real** flow — [STRATEGY.md](./STRATEGY.md). |
| G2 | **3–5 minute screen recording** — see **Video: Part D vs Part E** below. |

### Video: Part D vs Part E

- **Part D** = proof the integration works (good for *you*; optional in the final video if you are tight on time).
- **Part E** = what judges should see as **Life-OS**: load `prompts/LIFE_OS_SYSTEM.md`, run **E2** and **E3**, show **Notion** side-by-side or cut to browser so the **workspace** is obviously real.

The **CLI is the interface** for this submission unless you build something else. That is aligned with the challenge (Notion MCP + agent), not a downgrade.

---

## Troubleshooting (quick)

| Symptom | What to try |
|---------|-------------|
| No MCP tools | `/mcp` then `/mcp auth notion` again. |
| 401 / unauthorized | Finish OAuth; same Notion account as your workspace. |
| Empty search | Use titles you know exist; check you picked the right workspace during OAuth. |
| CLI can’t open browser | Run locally on PC, not headless SSH. |

---

## One-page checklist

- [x] Node 20+, Gemini CLI installed, Gemini auth works  
- [x] `.gemini/settings.json` has `notion` → `https://mcp.notion.com/mcp`  
- [x] `/mcp auth notion` completed  
- [x] D1–D4 pass; D5 one write visible in Notion  
- [ ] E2–E3 workflows run once  
- [ ] README submission section filled (demo script + how to run — see [README.md](./README.md))

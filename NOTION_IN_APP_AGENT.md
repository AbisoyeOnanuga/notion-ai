# Staying in Notion + broader “action” (calendar, mail, priorities)

Your goal: **action** means more than editing Notion—**prioritize work**, **surface reminders**, and **use calendar / email** so the agent helps you **do** household ops, not only read them.

Below is how that maps to **real Notion product** features, plan limits, and how it fits **Gemini CLI** vs **never leave Notion**.

---

## Two interfaces (both valid; pick what matches your plan and demo)

| Approach | Where you work | AI model | Notion MCP in the challenge sense | Best for |
|----------|----------------|----------|-------------------------------------|----------|
| **A. Gemini CLI** (what you built) | Terminal | **Gemini** | Yes — client calls `https://mcp.notion.com/mcp` | Reproducible repo, GitHub, clear logs of tool calls |
| **B. Notion Custom Agent** | **Inside Notion** (chat / @mentions) | Notion’s agent runtime (not Gemini) | **Optional:** add **Custom MCP server** URL `https://mcp.notion.com/mcp` if your workspace allows — plus native Notion + connectors | **“Never leave Notion”** UX, calendar/mail in one place |

The hackathon cares that you **use Notion MCP** in an impressive **system or process**. That can be **CLI + Gemini** *or* **Custom Agent + MCP connection** *or* both documented—**as long as the hosted Notion MCP appears in the story** (see [Connecting to Notion MCP](https://developers.notion.com/guides/mcp/get-started-with-mcp)).

---

## “Never leave Notion” — Custom Agents

Notion **Custom Agents** run **in the product**: scheduled runs, Notion/Slack triggers, or **manual runs from chat or @mentions**. That matches **stay in Notion** as the primary UI.

**Docs:** [MCP connections for Custom Agents](https://www.notion.com/help/mcp-connections-for-custom-agents)

**Important plan note:** **MCP connections for Custom Agents are available on Business and Enterprise plans only.** If you are on Personal/Plus, you may not be able to add MCP (including custom URL) to a Custom Agent—use **Notion AI Connectors** (Calendar/Mail) where available, and keep **Gemini CLI** as your MCP demo path, or upgrade workspace for the in-app MCP story.

**Custom MCP URL (if enabled):** Workspace admin enables **Custom MCP servers** under **Settings → Notion AI → AI connectors**. Then **Agent → Settings → Tools & Access → Add connection → Custom MCP server** and enter:

`https://mcp.notion.com/mcp`

(OAuth per Notion’s flow.) That makes the **same hosted Notion MCP** part of an **in-Notion** agent—strong narrative for judges *if* your plan supports it.

---

## Action beyond Notion: Calendar, Mail, priorities

### 1. Notion AI Connectors (often broader plan availability)

- **Notion Calendar AI Connector** — agent/AI can reason over calendar context ([Notion Calendar AI Connector](https://www.notion.com/help/notion-calendar-ai-connector)).
- **Notion Mail AI Connector** — mail context ([Notion Mail AI Connector](https://www.notion.com/help/notion-mail-ai-connector)).
- **Custom Agents + Calendar/Mail** — guided flows: [Manage your inbox and calendar with Custom Agents](https://www.notion.com/help/guides/manage-your-inbox-and-calendar-with-custom-agents), [Connect Calendar to Custom Agents](https://www.notion.com/help/connect-calendar-to-custom-agents).

These support the story: **prioritize from your Life-OS databases**, then **cross-check calendar** or **draft/follow email** without claiming fake automation.

### 2. What to promise in the write-up

Honest framing:

- **Prioritization + next steps** grounded in **Notion rows** (due dates, condition, stock).
- **Calendar**: e.g. “block time for HVAC filter” or “surface conflicts with repair window” when connectors are connected—not “Notion replaces Google Calendar” unless you built that.
- **Email**: summarize or draft from **Notion context** when Mail/Gmail connectors apply; sending may still need confirmation.

### 3. Gemini vs in-Notion agent

- **Gemini** is tied to **CLI / Google tooling** in your current repo—not embedded as the model inside Notion’s Custom Agent UI.
- **In-Notion** agents use **Notion’s** agent stack; you can still say **“Gemini-based workflow in development”** for the CLI path and **“Notion-native agent for daily use”** for the in-app path—many submissions use **two surfaces** (dev + prod).

---

## Suggested submission narrative (updated)

1. **System:** Life-OS Notion workspace (household ground truth) + **agent layer** that **prioritizes** and **acts** (Notion updates + optional calendar/mail context).
2. **Notion MCP proof:** Hosted server `https://mcp.notion.com/mcp` — shown via **Gemini CLI** and/or **Custom Agent custom MCP** (if plan allows).
3. **Action:** Comments/status in Notion **plus** orchestration story (what to do first, what to schedule)—leveraging **connectors** where connected.

Update **[SUBMISSION.md](./SUBMISSION.md)** “Solution” and “How it works” paragraphs to mention **prioritization**, **connectors**, and **in-Notion** vs **CLI** honestly.

---

## Quick decision tree

- **Have Business/Enterprise + want never-leave-Notion MCP demo?**  
  → Configure **Custom Agent** + **custom MCP** + Calendar/Mail connectors per Help Center.

- **On Personal/Plus or MCP not enabled?**  
  → **Gemini CLI + Notion MCP** remains your clearest **MCP** proof; add **Custom Agent** without MCP for in-Notion UX **or** describe roadmap.

- **Want Gemini specifically in the Notion UI?**  
  → Not supported as a first-party switch today; **CLI = Gemini**; **Notion = native agent**.

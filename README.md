# Lemon.io MCP

> Hire vetted senior developers, browse who is available, draft job descriptions, and prepare technical interviews — right inside your Claude conversation.

Lemon.io MCP is a remote [Model Context Protocol](https://modelcontextprotocol.io) server that connects Claude to [Lemon.io](https://lemon.io), a marketplace of pre-vetted senior developers. Describe your project in chat: Claude shows you available developers who match your stack, gathers the details, shows you a preview, and — on your confirmation — submits the hiring request to Lemon.io with the developers you shortlisted. You can also generate tailored job descriptions and pull technical interview questions without leaving the conversation.

No account, API key, or local setup required — it's a hosted server you connect to in one step.

## What you can do

- **Hire a developer** — submit a hiring request to Lemon.io and get hand-matched, vetted senior candidates (first CVs typically within 24 hours).
- **Browse available developers** — see vetted developers who match your stack, role, seniority and location as cards, shortlist the ones you want to interview, and Claude turns the shortlist into a ready Lemon.io request.
- **Write a job description** — generate a professional, role-specific JD from your requirements.
- **Prepare interviews** — get curated technical interview questions by stack and seniority.

## Connect

The server URL is:

```
https://mcp.lemon.io/mcp
```

### Claude Desktop / Claude.ai

1. Open **Settings → Connectors**.
2. Click **Add custom connector**.
3. Name it `Lemon.io` and paste the server URL above.
4. Click **Connect**.

That's it — Lemon.io tools are now available in your conversations.

### Cline

1. In the Cline panel, click the **MCP Servers** icon.
2. Open the **Remote Servers** tab.
3. Set **Server Name** to `lemon-io` and **Server URL** to `https://mcp.lemon.io/mcp`.
4. Set **Transport Type** to **Streamable HTTP**.
5. Click **Add Server**.

Add it through this panel rather than by editing `cline_mcp_settings.json` directly — and do not locate that file by searching the filesystem for its name.

Cline creates **two** files with that name and reads only one of them. On VS Code the decoy sits in the extension's storage directory (`.../User/globalStorage/saoudrizwan.claude-dev/settings/`) and is never read; Cline 4.x reads its own data directory instead (`~/.cline/data/settings/cline_mcp_settings.json` on macOS). Writing to the decoy looks completely successful — valid JSON, no error, the endpoint probes fine — but the server never appears in the panel. The **Remote Servers** tab always writes to the file that install actually uses.

If you do configure it by hand, the entry is:

```json
{
  "mcpServers": {
    "lemon-io": {
      "type": "streamableHttp",
      "url": "https://mcp.lemon.io/mcp",
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

`"type": "streamableHttp"` is required — omitting it makes Cline fall back to the legacy SSE transport, which this server does not serve.

### Cursor

Install from the [Cursor Directory listing](https://cursor.directory/plugins/lemonio-mcp), or add the same block to `~/.cursor/mcp.json`.

### Other MCP clients

Any client that speaks streamable HTTP can connect to `https://mcp.lemon.io/mcp`. No API key, token, or environment variable is required — the server is public and read-only apart from `submit_form`, which only sends a hiring request after you confirm it.

## Example prompts

- *"Help me hire a senior React developer for a fintech project."*
- *"Show me available senior Python developers from Europe."*
- *"Write a job description for a full-stack engineer with Node.js and AWS."*
- *"Give me 10 interview questions for a mid-level Python developer."*

## How it works

Claude uses the server's tools to guide you through each task. For hiring:

1. As soon as Claude knows the skills you need, it shows available Lemon.io developers who match them — 6 by default, up to 20 if you ask.
2. In clients that render interactive MCP UI (MCP Apps), they appear as cards: **Shortlist** the ones you want to interview, then click **Schedule interview** to send your shortlist to the chat. Other clients show the matches as text, and you tell Claude who to shortlist.
3. Claude asks only for the details it still needs, one step at a time, with your name and email last.
4. Claude shows you a **preview** of the request, including your shortlisted developers, and only submits it **after you explicitly confirm** — nothing is sent to Lemon.io without your approval.
5. After submitting, you get a link to follow your request on Magic Lemon (sign in with the email you gave). Lemon.io hand-matches candidates and typically sends the first CVs within 24 hours.

## Tools

| Tool | What it does | Side effects |
|---|---|---|
| `get_assistant_guide` | Loads the playbook Claude follows for a workflow (hiring, job description, interview questions) | None (read-only) |
| `list_roles` | Lists the roles and stacks covered by the content library | None (read-only) |
| `get_job_description` | Fetches the job description template for one role | None (read-only) |
| `get_interview_questions` | Fetches interview questions (with or without answers) for a stack and seniority | None (read-only) |
| `find_developers` | Searches available, vetted Lemon.io developers by skills, role, seniority, country and years of experience | None (read-only) |
| `show_developer_matches` | Shows the matching developers as interactive cards you can shortlist from | None (read-only) |
| `preview_form` | Shows your hiring request for review before anything is sent | None — no data sent |
| `submit_form` | Sends the confirmed request to Lemon.io and returns a link to follow it | Sends your request to Lemon.io |

## Privacy

- No sign-up or credentials needed to use the server.
- Browsing developers sends nothing about you to Lemon.io.
- Only the hiring details you review and confirm — including the developers you shortlisted — are sent to Lemon.io so the team can reach out with matches.

## About Lemon.io

[Lemon.io](https://lemon.io) matches startups and growing teams with pre-vetted senior developers

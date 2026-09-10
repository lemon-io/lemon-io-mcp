# Lemon.io MCP

> Hire vetted senior developers, draft job descriptions, and prepare technical interviews — right inside your Claude conversation.

Lemon.io MCP is a remote [Model Context Protocol](https://modelcontextprotocol.io) server that connects Claude to [Lemon.io](https://lemon.io), a marketplace of pre-vetted senior developers. Describe your project in chat, and Claude gathers the details, shows you a preview, and — on your confirmation — submits the hiring request to Lemon.io. You can also generate tailored job descriptions and pull technical interview questions without leaving the conversation.

No account, API key, or local setup required — it's a hosted server you connect to in one step.

## What you can do

- **Hire a developer** — submit a hiring request to Lemon.io and get hand-matched, vetted senior candidates (first CVs typically within 24 hours).
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

Add it through this panel rather than by editing `cline_mcp_settings.json` directly. The location of that file differs between Cline versions and IDEs, and an upgraded install can leave a stale copy behind that Cline no longer reads — writing to it looks successful but the server never appears. If you do configure it by hand, the entry is:

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
- *"Write a job description for a full-stack engineer with Node.js and AWS."*
- *"Give me 10 interview questions for a mid-level Python developer."*

## How it works

Claude uses the server's tools to guide you through each task. For hiring, it collects the required details, shows you a **preview**, and only submits **after you explicitly confirm** — nothing is sent to Lemon.io without your approval.

## Privacy

- No sign-up or credentials needed to use the server.
- Only the hiring details you review and confirm are sent to Lemon.io so the team can reach out with matches.

## About Lemon.io

[Lemon.io](https://lemon.io) matches startups and growing teams with pre-vetted senior developers

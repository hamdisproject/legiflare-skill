# Legiflare Skills

Agent skills that write your legal documents from what your product actually does, and publish them on
[Legiflare](https://legiflare.com) at a public URL you can paste into the App Store, Google Play, your checkout or
your site's footer.

Instead of filling in a template, the agent reads your code: it finds the analytics, ads, payment, sign-in and AI
SDKs you use, the device permissions you ask for and the data your forms collect, asks only for what it can't find
(your company name, contact email, where your users are), and writes a document that matches. When your product
changes, it updates the same document, so the URL never changes.

The skills follow the open [Agent Skills](https://agentskills.io) format, so they work in Claude Code, Codex,
Cursor, GitHub Copilot, Gemini CLI, Windsurf and other agents that support it.

## Skills

| Skill | What it does |
| --- | --- |
| [`privacy-policy`](skills/privacy-policy/SKILL.md) | A privacy policy covering GDPR, UK GDPR, CCPA/CPRA and other US state laws, KVKK, LGPD, PIPEDA and the App Store and Google Play requirements, naming every third-party service the product uses. |
| [`terms-of-service`](skills/terms-of-service/SKILL.md) | Terms of service that fit your accounts, subscriptions, store billing, user content and AI features, including Apple's minimum EULA terms for iOS apps. |
| [`cookie-policy`](skills/cookie-policy/SKILL.md) | A cookie policy listing every cookie and storage key your site sets, by category, with provider, purpose and duration. |
| [`refund-policy`](skills/refund-policy/SKILL.md) | A refund and cancellation policy that matches your sales channel (App Store, Google Play, Stripe, Paddle, Lemon Squeezy) and the withdrawal rights in the EU, UK, Turkey and elsewhere. |
| [`legal-docs-audit`](skills/legal-docs-audit/SKILL.md) | Checks your published documents against your current code, reports what's missing, outdated or inconsistent, and fixes it once you approve. |

## Install

Setup has two parts: connect the Legiflare MCP server, which publishes the documents, and install the skills,
which tell the agent how to write them. In Claude Code, the plugin does both at once.

The MCP server is at `https://mcp.legiflare.com/mcp` (Streamable HTTP). The first time your agent connects, it
opens your browser to sign in with your Legiflare account (email and password, or Google and GitHub); there are no
API keys to copy.

### Claude Code

Add this repository as a plugin marketplace and install the plugin, which brings the skills and the MCP server
together:

```
/plugin marketplace add hamdisproject/legiflare-skills
/plugin install legiflare@legiflare
```

Then run `/mcp`, pick `legiflare` and sign in.

### Codex

Connect the MCP server and sign in:

```bash
codex mcp add legiflare --url https://mcp.legiflare.com/mcp
```

```bash
codex mcp login legiflare
```

Or add it to `~/.codex/config.toml` yourself:

```toml
[mcp_servers.legiflare]
url = "https://mcp.legiflare.com/mcp"
```

Then [install the skills](#installing-the-skills) for Codex.

### Cursor

Add the MCP server to `~/.cursor/mcp.json` (or `.cursor/mcp.json` in a project), then sign in from Cursor's MCP
settings when it asks:

```json
{
  "mcpServers": {
    "legiflare": { "url": "https://mcp.legiflare.com/mcp" }
  }
}
```

Then [install the skills](#installing-the-skills) for Cursor.

### GitHub Copilot in VS Code

Add the MCP server from the terminal:

```bash
code --add-mcp '{"name":"legiflare","type":"http","url":"https://mcp.legiflare.com/mcp"}'
```

or in `.vscode/mcp.json` in a project:

```json
{
  "servers": {
    "legiflare": { "type": "http", "url": "https://mcp.legiflare.com/mcp" }
  }
}
```

Start the server from the file or the MCP servers list and sign in when VS Code asks. Then
[install the skills](#installing-the-skills) for GitHub Copilot.

### GitHub Copilot CLI

Run `/mcp add`, name it `legiflare`, choose **HTTP**, paste `https://mcp.legiflare.com/mcp` and save with Ctrl+S. Or
add it to `~/.copilot/mcp-config.json`:

```json
{
  "mcpServers": {
    "legiflare": {
      "type": "http",
      "url": "https://mcp.legiflare.com/mcp",
      "tools": ["*"]
    }
  }
}
```

Then [install the skills](#installing-the-skills) for GitHub Copilot. Copilot's cloud agent on GitHub.com can't use
MCP servers that sign in with OAuth, so use these skills with Copilot in your editor or the CLI.

### Gemini CLI

```bash
gemini mcp add --transport http legiflare https://mcp.legiflare.com/mcp
```

Gemini CLI opens the browser to sign in on first use; `/mcp auth legiflare` signs in again. Then
[install the skills](#installing-the-skills) for Gemini CLI.

### Windsurf

Add the MCP server to `~/.codeium/windsurf/mcp_config.json`. Windsurf uses `serverUrl`, not `url`:

```json
{
  "mcpServers": {
    "legiflare": { "serverUrl": "https://mcp.legiflare.com/mcp" }
  }
}
```

Then [install the skills](#installing-the-skills) for Windsurf.

### Claude (web and desktop)

Add `https://mcp.legiflare.com/mcp` as a custom connector (Settings → Connectors → Add custom connector), then zip
the skill folders you want from `skills/` and upload them under Settings → Capabilities → Skills.

### Other agents

Any agent that supports remote MCP servers with OAuth sign-in can use `https://mcp.legiflare.com/mcp`, and any
agent that supports Agent Skills can use the skills below.

## Installing the skills

**With a command.** Either of these asks which agents to install for, or takes them as flags:

```bash
npx skills add hamdisproject/legiflare-skills
```

```bash
gh skill install hamdisproject/legiflare-skills --agent codex --scope user
```

`gh skill` needs GitHub CLI 2.90 or later; its `--agent` values include `claude-code`, `codex`, `cursor`,
`github-copilot` and `gemini-cli`, and `--scope` is `project` (the current repository) or `user` (every project).

**By hand.** Copy the folders in `skills/` to the folder your agent reads skills from:

| Agent | In a project | For every project |
| --- | --- | --- |
| Claude Code | `.claude/skills/` | `~/.claude/skills/` |
| Codex | `.agents/skills/` | `~/.agents/skills/` |
| Cursor | `.agents/skills/` or `.cursor/skills/` | `~/.agents/skills/` or `~/.cursor/skills/` |
| GitHub Copilot (VS Code, CLI) | `.github/skills/` or `.agents/skills/` | `~/.copilot/skills/` or `~/.agents/skills/` |
| Gemini CLI | `.gemini/skills/` or `.agents/skills/` | `~/.gemini/skills/` |
| Windsurf | `.windsurf/skills/` | `~/.codeium/windsurf/skills/` |

`.agents/skills/` is shared: Codex, Cursor, GitHub Copilot and Gemini CLI all read it, so one copy there covers
them. For example, for every project:

```bash
git clone https://github.com/hamdisproject/legiflare-skills.git
```

```bash
mkdir -p ~/.agents/skills && cp -R legiflare-skills/skills/* ~/.agents/skills/
```

## Try it

In a project:

- "Write a privacy policy for this app and publish it on Legiflare."
- "We added RevenueCat and AdMob. Update my privacy policy."
- "Which cookies does this site set? Write a cookie policy for it."
- "Write terms of service for our SaaS. We bill monthly through Stripe and users can upload files."
- "We sell through Paddle to customers in the EU and the US. Write our refund policy."
- "I'm submitting to the App Store next week. Are my legal documents up to date?"

The agent tells you what it found, asks a few questions, publishes the document and gives you its URL.

## What the MCP server can do

| Tool | What it does |
| --- | --- |
| `get_profile` | The signed-in user's name, company and email |
| `list_document_types` | Document types (Privacy Policy, Terms of Service, Cookie Policy, Refund Policy, Other) and their IDs |
| `list_documents` | Your documents, without their content |
| `get_document` | One document with its content |
| `create_document` | Create a document and get its public URL |
| `update_document` | Change a document; the URL stays the same |
| `delete_document` | Delete a document (the skills never do this unless you ask) |

The server only reaches your own documents, and your code stays on your machine: the agent reads it locally, and
only the finished document is sent to Legiflare. The server's source is at
[hamdisproject/legiflare-mcp](https://github.com/hamdisproject/legiflare-mcp).

## A note on legal advice

These skills write accurate first drafts grounded in your product, and check them against the main privacy and
consumer laws and store rules. They are not legal advice. For health, financial or children's data, marketplaces
and large business contracts, have a lawyer review the result.

## Contributing

Issues and pull requests are welcome, especially corrections to the legal summaries in each skill's `references/`
folder and new third-party services for
[`third-party-services.md`](skills/privacy-policy/references/third-party-services.md) and
[`common-cookies.md`](skills/cookie-policy/references/common-cookies.md).

## License

[MIT](LICENSE)

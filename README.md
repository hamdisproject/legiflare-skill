# Legiflare Skills

Agent skills that write your legal documents from what your product actually does, and publish them on
[Legiflare](https://legiflare.com) at a public URL you can paste into the App Store, Google Play, your checkout or
your site's footer.

Instead of filling in a template, the agent reads your code: it finds the analytics, ads, payment, sign-in and AI
SDKs you use, the device permissions you ask for and the data your forms collect, asks only for what it can't find
(your company name, contact email, where your users are), and writes a document that matches. When your product
changes, it updates the same document, so the URL never changes.

The skills follow the open [Agent Skills](https://agentskills.io) format, and the repository is a plugin for Claude
Code, Codex, Cursor and GitHub Copilot and an extension for Gemini CLI, so they work in all of these and in other
agents that support skills.

## Skills

| Skill | What it does |
| --- | --- |
| [`privacy-policy`](skills/privacy-policy/SKILL.md) | A privacy policy covering GDPR, UK GDPR, CCPA/CPRA and other US state laws, KVKK, LGPD, PIPEDA and the App Store and Google Play requirements, naming every third-party service the product uses. |
| [`terms-of-service`](skills/terms-of-service/SKILL.md) | Terms of service that fit your accounts, subscriptions, store billing, user content and AI features, including Apple's minimum EULA terms for iOS apps. |
| [`cookie-policy`](skills/cookie-policy/SKILL.md) | A cookie policy listing every cookie and storage key your site sets, by category, with provider, purpose and duration. |
| [`refund-policy`](skills/refund-policy/SKILL.md) | A refund and cancellation policy that matches your sales channel (App Store, Google Play, Stripe, Paddle, Lemon Squeezy) and the withdrawal rights in the EU, UK, Turkey and elsewhere. |
| [`legal-docs-audit`](skills/legal-docs-audit/SKILL.md) | Checks your published documents against your current code, reports what's missing, outdated or inconsistent, and fixes it once you approve. |

## Install

Each agent below installs the skills and the Legiflare MCP server (`https://mcp.legiflare.com/mcp`) together. The
first time your agent uses the Legiflare tools, it opens your browser to sign in with your Legiflare account (email
and password, or Google and GitHub); there are no API keys to copy.

### Claude Code

```
/plugin marketplace add hamdisproject/legiflare-skill
/plugin install legiflare@legiflare
```

Then run `/mcp`, pick `legiflare` and sign in.

### Codex

Add the marketplace, install the plugin and sign in:

```bash
codex plugin marketplace add hamdisproject/legiflare-skill
```

```bash
codex plugin add legiflare@legiflare
```

```bash
codex mcp login legiflare
```

### GitHub Copilot CLI

```bash
copilot plugin install hamdisproject/legiflare-skill
```

Copilot's cloud agent on GitHub.com can't use MCP servers that sign in with OAuth, so use these skills with
Copilot in the CLI or your editor.

### GitHub Copilot in VS Code

Run **Chat: Install Plugin From Source** from the Command Palette and enter
`https://github.com/hamdisproject/legiflare-skill`. Agent plugins are a preview feature; if the command is
missing, turn on `chat.plugins.enabled` (in organizations, an admin may have to allow it).

### Cursor

Open **Customize**, add a plugin **From GitHub Repository** with `https://github.com/hamdisproject/legiflare-skill`,
and install **legiflare**.

### Gemini CLI

```bash
gemini extensions install https://github.com/hamdisproject/legiflare-skill
```

Gemini CLI signs in on first use; `/mcp auth legiflare` signs in again.

### Windsurf

Windsurf has no plugins, so add the two parts yourself. Add the MCP server to
`~/.codeium/windsurf/mcp_config.json` (Windsurf uses `serverUrl`, not `url`):

```json
{
  "mcpServers": {
    "legiflare": { "serverUrl": "https://mcp.legiflare.com/mcp" }
  }
}
```

Then [install the skills](#installing-the-skills-by-hand) into `~/.codeium/windsurf/skills/`.

### Claude (web and desktop)

Add `https://mcp.legiflare.com/mcp` as a custom connector (Settings → Connectors → Add custom connector), then zip
the skill folders you want from `skills/` and upload them under Settings → Capabilities → Skills.

### Other agents

Any agent that supports remote MCP servers with OAuth sign-in can use `https://mcp.legiflare.com/mcp`, and any
agent that supports Agent Skills can use the skills: see [connecting the MCP server by hand](#connecting-the-mcp-server-by-hand)
and [installing the skills by hand](#installing-the-skills-by-hand).

## Connecting the MCP server by hand

If you'd rather not install a plugin, add the server to your agent's MCP configuration:

| Agent | How |
| --- | --- |
| Claude Code | `claude mcp add --transport http legiflare https://mcp.legiflare.com/mcp`, then `/mcp` to sign in |
| Codex | `codex mcp add legiflare --url https://mcp.legiflare.com/mcp`, then `codex mcp login legiflare`; or `[mcp_servers.legiflare]` with `url = "https://mcp.legiflare.com/mcp"` in `~/.codex/config.toml` |
| Cursor | `{"mcpServers": {"legiflare": {"url": "https://mcp.legiflare.com/mcp"}}}` in `~/.cursor/mcp.json` or a project's `.cursor/mcp.json` |
| VS Code | `code --add-mcp '{"name":"legiflare","type":"http","url":"https://mcp.legiflare.com/mcp"}'`, or `{"servers": {"legiflare": {"type": "http", "url": "https://mcp.legiflare.com/mcp"}}}` in `.vscode/mcp.json` |
| Copilot CLI | `/mcp add`, type HTTP, with the URL; or `{"mcpServers": {"legiflare": {"type": "http", "url": "https://mcp.legiflare.com/mcp", "tools": ["*"]}}}` in `~/.copilot/mcp-config.json` |
| Gemini CLI | `gemini mcp add --transport http legiflare https://mcp.legiflare.com/mcp` |
| Windsurf | `{"mcpServers": {"legiflare": {"serverUrl": "https://mcp.legiflare.com/mcp"}}}` in `~/.codeium/windsurf/mcp_config.json` |

## Installing the skills by hand

The plugins above already include the skills. Without a plugin, either of these commands asks which agents to
install for, or takes them as flags:

```bash
npx skills add hamdisproject/legiflare-skill
```

```bash
gh skill install hamdisproject/legiflare-skill --agent codex --scope user
```

`gh skill` needs GitHub CLI 2.90 or later; its `--agent` values include `claude-code`, `codex`, `cursor`,
`github-copilot` and `gemini-cli`, and `--scope` is `project` (the current repository) or `user` (every project).

Or copy the folders in `skills/` to the folder your agent reads skills from:

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
git clone https://github.com/hamdisproject/legiflare-skill.git
```

```bash
mkdir -p ~/.agents/skills && cp -R legiflare-skill/skills/* ~/.agents/skills/
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

## What's in this repository

| Path | Read by |
| --- | --- |
| `skills/` | Every agent: the skills themselves |
| `plugin.json`, `mcp.json` | [Agent Plugins](https://agent-plugins.org) clients: Codex, GitHub Copilot, Cursor |
| `.agents/plugins/marketplace.json` | Codex (`codex plugin marketplace add`) |
| `.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json`, `.mcp.json` | Claude Code |
| `.cursor-plugin/plugin.json`, `.cursor-plugin/marketplace.json` | Cursor |
| `gemini-extension.json` | Gemini CLI |
| `assets/icon.png` | Plugin listings |

When you change the version, change it in `plugin.json`, `.claude-plugin/plugin.json`, `.cursor-plugin/plugin.json`
and `gemini-extension.json` together; the MCP server address appears in `mcp.json`, `.mcp.json`,
`.cursor-plugin/plugin.json` and `gemini-extension.json`.

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

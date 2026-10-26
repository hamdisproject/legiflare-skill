# Legiflare Skills

Agent skills that write your legal documents from what your product actually does, and publish them on
[Legiflare](https://legiflare.com) at a public URL you can paste into the App Store, Google Play, your checkout or
your site's footer.

Instead of filling in a template, the agent reads your code: it finds the analytics, ads, payment, sign-in and AI
SDKs you use, the device permissions you ask for and the data your forms collect, asks only for what it can't find
(your company name, contact email, where your users are), and writes a document that matches. When your product
changes, it updates the same document, so the URL never changes.

## Skills

| Skill | What it does |
| --- | --- |
| [`privacy-policy`](skills/privacy-policy/SKILL.md) | A privacy policy covering GDPR, UK GDPR, CCPA/CPRA and other US state laws, KVKK, LGPD, PIPEDA and the App Store and Google Play requirements, naming every third-party service the product uses. |
| [`terms-of-service`](skills/terms-of-service/SKILL.md) | Terms of service that fit your accounts, subscriptions, store billing, user content and AI features, including Apple's minimum EULA terms for iOS apps. |
| [`cookie-policy`](skills/cookie-policy/SKILL.md) | A cookie policy listing every cookie and storage key your site sets, by category, with provider, purpose and duration. |
| [`refund-policy`](skills/refund-policy/SKILL.md) | A refund and cancellation policy that matches your sales channel (App Store, Google Play, Stripe, Paddle, Lemon Squeezy) and the withdrawal rights in the EU, UK, Turkey and elsewhere. |
| [`legal-docs-audit`](skills/legal-docs-audit/SKILL.md) | Checks your published documents against your current code, reports what's missing, outdated or inconsistent, and fixes it once you approve. |

## Install

The skills use the Legiflare MCP server at `https://mcp.legiflare.com/mcp`. The first time a skill needs it, you
sign in with your Legiflare account in the browser (email and password, or Google and GitHub); there are no API
keys to copy.

### Claude Code

Add this repository as a plugin marketplace and install the plugin. It brings the skills and the MCP server
together:

```
/plugin marketplace add hamdisproject/legiflare-skills
/plugin install legiflare@legiflare
```

Then run `/mcp`, pick `legiflare` and sign in.

### Other agents (Cursor, Codex, VS Code, ...)

Install the skills with the [`skills`](https://skills.sh) CLI:

```bash
npx skills add hamdisproject/legiflare-skills
```

and add the MCP server to your agent's configuration, for example in Cursor's `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "legiflare": { "url": "https://mcp.legiflare.com/mcp" }
  }
}
```

### Claude (web and desktop)

Add `https://mcp.legiflare.com/mcp` as a custom connector (Settings → Connectors → Add custom connector), then zip
the skill folders you want from `skills/` and upload them under Settings → Capabilities → Skills.

### By hand

Copy the folders in `skills/` to your agent's skills directory (for Claude Code, `~/.claude/skills/` or a
project's `.claude/skills/`) and add the MCP server:

```bash
claude mcp add --transport http legiflare https://mcp.legiflare.com/mcp
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

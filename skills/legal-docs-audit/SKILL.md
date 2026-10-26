---
name: legal-docs-audit
description: Check a user's published Legiflare legal documents (privacy policy, terms of service, cookie and refund policies) against what their product does today, report what's missing, outdated or inconsistent, and fix it with their approval. Use this whenever the user asks whether their legal documents or policies are still accurate, complete or compliant, is preparing an app store submission, review or launch, has added or removed SDKs, payments, ads, analytics or AI features, changed company name, address or contact details, or wants their Legiflare documents reviewed or cleaned up, even if they don't mention Legiflare.
---

# Legal documents audit

Legal documents go stale quietly: a new analytics SDK, a switch from Stripe to Paddle, an AI feature, a new
company address, and the published policy no longer describes the product. Stores and regulators compare the
documents with what the app does, so an audit compares them too, and turns the differences into concrete fixes.

These documents are live and their URLs are often linked from store listings and checkout pages, so report first
and change them only after the user agrees.

## Workflow

1. Collect the documents
2. Establish what the product does now
3. Compare
4. Report
5. Fix what the user approves
6. Hand over

### 1. Collect the documents

Call `list_documents`, then `get_document` for each document of the product being audited (the list has no
content). Call `get_profile` for the account's name, company and email. If the user has documents for several
products, ask which ones to audit, unless it's clear from the conversation.

### 2. Establish what the product does now

When there's a codebase, it's the source of truth. Check:

- dependency manifests and `<script>` tags for analytics, ads, attribution, crash reporting, payments, sign-in,
  email, push notifications, AI providers, support chat, maps and embeds;
- device permissions (iOS `Info.plist` usage descriptions, Android `uses-permission`, Expo `app.json`);
- what users enter and what's stored (forms, database models), and what's sent to other services;
- how billing works (store billing, a processor, a merchant of record), trials, renewals and cancellation;
- cookies and local storage the site sets;
- account deletion, content uploads, moderation, minimum age.

The privacy-policy, cookie-policy, terms-of-service and refund-policy skills in this collection hold the detailed
checklists and service lists for each document; use them when they're installed. Without a codebase, ask the user
what changed since the documents were written: new services, features, prices, company details, markets.

### 3. Compare

For each document, look for:

- **Missing**: something the product does that the document doesn't mention (a service, a kind of data, a
  permission, a subscription, user content, an AI provider, a region with its own required items).
- **Stale**: something the document mentions that the product no longer does or uses.
- **Wrong**: statements the product contradicts, such as "we don't track you" next to an ads SDK, "refunds within
  30 days" for App Store purchases, which only Apple refunds, or a retention period the code doesn't follow.
- **Inconsistent**: the documents disagree with each other: different company names, contact emails or refund
  windows, a privacy policy that doesn't mention cookies the cookie policy lists, terms that link to a policy that
  doesn't exist.
- **Store and legal gaps**: no account deletion section in an app's privacy policy, no "Last updated" date, a
  privacy policy title Google Play wouldn't recognise as one, missing items for a region the product serves.
- **Legiflare issues**: content still holding placeholders ("[Company Name]") or sample text, Markdown that won't
  render (the page renders HTML), an `h1` that repeats the page title, an empty description, a document hidden
  (`visible: false`) that the product links to, or two documents of the same type for one product.

Give evidence for each finding: the file and line, the dependency, or a short quote from the document.

### 4. Report

Group the findings by document, most serious first:

- **Must fix**: wrong statements, undisclosed data sharing, missing store or legal requirements.
- **Should fix**: stale or inconsistent content.
- **Nice to have**: clarity, structure, wording.

For each, say what to change. End by asking which fixes to apply. When nothing is wrong, say so plainly and name
what you checked.

### 5. Fix what the user approves

- Change existing documents with `update_document`, and keep them: the URLs are linked from elsewhere. Send the
  complete revised `content` (the tool replaces the field) and set "Last updated" to today's date.
- Create a document only when one is missing and the user wants it, using `list_document_types` for the type's ID.
- Never delete a document unless the user asks for that specific one: deleting is permanent and breaks every link
  to it. To take one offline, set `visible: false`.
- Read each changed document back with `get_document` to confirm the change landed.

**Content format.** The public page renders `content` as HTML below the document title:

- Use only `h2`, `h3`, `h4`, `p`, `ul`, `ol`, `li`, `strong`, `em`, `u`, `blockquote`, `table`, `thead`, `tbody`,
  `tr`, `th`, `td`, `a` and `br`.
- Start with `h2` sections. The page already shows the title as its heading, so an `h1` would repeat it.
- No Markdown, scripts, styles, classes, inline styles or `html`/`head`/`body` wrappers.
- Write links as full `https://` URLs and email addresses as `mailto:` links.

**If the Legiflare tools aren't available**, tell the user how to connect them: in Claude Code,
`claude mcp add --transport http legiflare https://mcp.legiflare.com/mcp`, then sign in from `/mcp`; in Claude,
add `https://mcp.legiflare.com/mcp` as a custom connector. Sign-in happens in the browser with their Legiflare
account. Without them, you can still audit documents the user pastes or links, and give the fixes as text. If a
tool says the sign-in has expired, ask them to reconnect.

### 6. Hand over

Summarize what changed in each document, with its URL, and what the user still has to do outside Legiflare:
update the App Store privacy details or the Google Play Data safety form, fix a consent banner, tell users about
changed terms when the terms require notice. Add in one line that this isn't legal advice.

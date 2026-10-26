---
name: privacy-policy
description: Write or update a privacy policy based on what an app, website or SaaS actually collects and shares, and publish it on Legiflare to get a public URL for the App Store, Google Play, a site footer or a sign-up form. Use this whenever the user needs a privacy policy, privacy notice, GDPR or CCPA notice, KVKK aydınlatma metni or a "privacy policy URL", is preparing an app store submission, has added an SDK (analytics, ads, payments, AI, crash reporting, sign-in) the policy should mention, or wants to fix or update an existing Legiflare privacy policy, even if they don't mention Legiflare.
---

# Privacy policy

A privacy policy is a statement of fact about what a product does with personal data. App reviewers, regulators
and users hold it against what the product really does, so the whole value of this skill is accuracy: find out
what the product collects and who it shares it with, then say that plainly. A template that names services the
product doesn't use, or misses ones it does, is worse than no policy at all.

## Workflow

1. Learn the product
2. Take an inventory of the data
3. Ask for what you couldn't find
4. Draft
5. Check the draft against the inventory
6. Publish on Legiflare
7. Hand over

If the user already has a Legiflare privacy policy (step 6 checks), this is an update: read it first, keep what
is still true, and change only what the inventory contradicts or misses.

### 1. Learn the product

Work out what it is (iOS or Android app, website, SaaS, browser extension, game, online store), what it's called,
who runs it (a company or a person, and in which country) and who uses it. Look in the conversation, then the
repository (README, `package.json`, `app.json`, `Info.plist`, `AndroidManifest.xml`, `pubspec.yaml`, the site's
domain), then Legiflare's `get_profile`, which returns the account's name, company name and email. The account
email may be a personal one, so confirm the contact address before printing it in a public document.

### 2. Take an inventory of the data

When there is a codebase, it is the source of truth, more than anyone's memory of it. Look at:

- **Dependencies and scripts**: package manifests (`package.json`, `Podfile`, `Package.swift`, `build.gradle`,
  `pubspec.yaml`, `requirements.txt`, `pyproject.toml`, `Gemfile`, `composer.json`, `go.mod`, `pom.xml`) and
  `<script>` tags in layouts or tag managers. Match them against
  [references/third-party-services.md](references/third-party-services.md), which says what each common service
  receives and links its privacy policy.
- **Device permissions**: iOS `Info.plist` keys ending in `UsageDescription` (location, camera, photos,
  microphone, contacts, health; `NSUserTrackingUsageDescription` means App Tracking Transparency), Android
  `uses-permission` entries (`ACCESS_FINE_LOCATION`, `CAMERA`, `RECORD_AUDIO`, `READ_CONTACTS`,
  `com.google.android.gms.permission.AD_ID`), and Expo's `app.json`. Face ID or fingerprint checks through the OS
  never give the app the biometric data itself; say so rather than listing biometrics as collected.
- **What users enter**: sign-up and profile forms, database models and migrations (email, name, phone, address,
  date of birth, uploads, messages, payment records).
- **What leaves the product**: calls to other APIs, webhooks, email senders, and AI providers, which receive
  whatever prompts, documents or user text the product sends them.
- **The server side**: request logs with IP addresses, hosting and CDN, backups, how long things are kept.
- **Cookies and local storage** on a website (the cookie-policy skill covers them in detail).
- **Account deletion**: whether users can delete their account, and how. The App Store and Google Play require it
  for apps that let users create accounts.

Keep a working table for yourself (not for publishing): data → where it comes from → why → who receives it → how
long it's kept. Every statement in the policy should trace back to a row.

Without a codebase (for example in a chat without file access), get the same facts by asking: what users sign up
with, what the product stores, which services it uses for analytics, ads, payments, sign-in, email, hosting and
AI, and whether it uses location, camera, contacts or the advertising ID.

### 3. Ask for what you couldn't find

Usual gaps: the operator's legal name and country, the email for privacy requests, where the users are (EU/UK,
California and other US states, Turkey, Brazil, Canada, everywhere), whether children under 13 use it, how long
data is kept, and whether data is sold or used for targeted advertising. Ask them in one message, suggest a
sensible default for each so the user can answer "defaults are fine", and don't ask for anything you already
found.

If the user wants to skip the questions, draft with clearly marked placeholders and publish the document hidden
(`visible: false`) until they fill them in.

### 4. Draft

Read [references/regional-requirements.md](references/regional-requirements.md) for each region the product serves
and for the app stores it's in; it lists what each one requires the policy to say.

Usual sections (drop what doesn't apply, and never add a claim the inventory doesn't support):

1. **Introduction**: who runs the product and how to reach them, what the policy covers (product names,
   platforms, sites), and "Last updated: <date>".
2. **Information we collect**, grouped as what users give, what is collected automatically, and what comes from
   others (for example sign-in providers). Be concrete: "your email address and name when you create an account",
   not "personal information".
3. **How we use it**: each purpose, and for EU/UK users the legal basis of each (contract, legitimate interests,
   consent, legal obligation).
4. **How we share it**: service providers by name with what they do and a link to their policy, business
   transfers, legal requests. Say plainly whether data is sold or shared for targeted advertising.
5. **International transfers**, when users and providers are in different regions.
6. **How long we keep it**, per category or by the criteria used.
7. **Your rights** and how to use them, per region.
8. **Children**.
9. **Security**: the measures actually in place. Don't promise perfect security or claim certifications nobody
   confirmed.
10. **Deleting your account**: the in-app path, a web link or an email address.
11. **Changes to this policy**.
12. **Contact**.

Write in plain language, addressed to the reader as "you", with short paragraphs and lists. Use the language the
user asks for; if they don't say, use the language of the product's audience, and ask when that is unclear. One
policy can cover a website and its apps when they handle data the same way.

### 5. Check the draft against the inventory

- Every service in the inventory is named, and nothing is named that the product doesn't use.
- Every kind of data has a purpose, a retention period and, where EU/UK users are covered, a legal basis.
- Nothing contradicts the code: no "we don't track you" next to an ads or analytics SDK, no "we never share your
  data" when processors receive it.
- No placeholders such as "[Company Name]", no sample text.
- For apps: the policy agrees with what the App Store privacy details and the Google Play Data safety form should
  declare.

### 6. Publish on Legiflare

Legiflare hosts the document at a public URL that stays the same when the document is edited, so the link can go
into store listings and site footers once. Its MCP server (`https://mcp.legiflare.com/mcp`) gives you these
tools: `get_profile`, `list_document_types`, `list_documents`, `get_document`, `create_document`,
`update_document` and `delete_document`.

1. Call `list_documents`. If the user already has a privacy policy for this product, read it with `get_document`
   and change it with `update_document`: its URL may already be in a store listing or footer, and a second copy
   would leave the old one stale. Create a new document only for a different product, or when the user asks.
2. Call `list_document_types` and use the ID of "Privacy Policy". Look it up each time rather than assuming a
   number.
3. Call `create_document` (or `update_document` with the document's `id`):
   - `title`: the document and the product, such as "Privacy Policy for Acme Notes" (3–255 characters). Google
     Play expects the page to be labelled as a privacy policy.
   - `documentTypeId`: from step 2.
   - `description`: one plain sentence for listings (up to 255 characters).
   - `content`: the HTML described below.
   - `visible`: `true` to publish. Use `false` while placeholders remain or the user wants to read it first; a
     hidden document's page shows nothing until it is made visible.
4. Give the user the `url` from the result.

`update_document` changes only the fields you send, so send the complete new `content`, not a fragment.

**Content format.** The page renders `content` as HTML below the document title:

- Use only `h2`, `h3`, `h4`, `p`, `ul`, `ol`, `li`, `strong`, `em`, `u`, `blockquote`, `table`, `thead`, `tbody`,
  `tr`, `th`, `td`, `a` and `br`.
- Start with `h2` sections. The page already shows the title as its heading, so an `h1` would repeat it.
- No Markdown, scripts, styles, classes, inline styles or `html`/`head`/`body` wrappers.
- Write links as full `https://` URLs and email addresses as `mailto:` links.

**If the Legiflare tools aren't available**, tell the user to add the Legiflare MCP server,
`https://mcp.legiflare.com/mcp`, to their agent and sign in with their Legiflare account when the browser opens.
In Claude Code: `claude mcp add --transport http legiflare https://mcp.legiflare.com/mcp`, then `/mcp`. In Codex:
`codex mcp add legiflare --url https://mcp.legiflare.com/mcp`, then `codex mcp login legiflare`. In Gemini CLI:
`gemini mcp add --transport http legiflare https://mcp.legiflare.com/mcp`. In Claude, Cursor, VS Code, Windsurf
and other apps, add the URL in their MCP or connector settings; the steps for each are at
https://github.com/hamdisproject/legiflare-skill#install.
If they'd rather not, save the document as an HTML file in their project instead. If a tool says the
sign-in has expired, ask them to reconnect.

### 7. Hand over

Tell the user:

- the URL;
- in a few lines, what the policy covers and for which regions;
- the assumptions they should check (anything you inferred rather than found, such as retention periods);
- where the link goes: App Store Connect (App Privacy → Privacy Policy URL), Play Console (App content → Privacy
  policy), the app's settings or about screen, the website footer and the sign-up form;
- for apps, that the App Store privacy details and the Google Play Data safety form must match the policy.

Add in one line that this isn't legal advice, and suggest a lawyer's review when the product handles health,
financial or children's data. For an update, list what changed.

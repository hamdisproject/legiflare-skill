---
name: terms-of-service
description: Write or update terms of service (terms and conditions, terms of use, user agreement or an app's EULA) that fit how a product really works, including accounts, subscriptions, user content, AI features and app store billing, and publish them on Legiflare at a public URL. Use this whenever the user needs terms of service, terms and conditions, ToS or terms of use for an app, SaaS, website or game, is launching or submitting to an app store, starts charging or adds subscriptions, user-generated content or AI features, or wants to update an existing Legiflare terms document, even if they don't mention Legiflare.
---

# Terms of service

Terms of service are the contract between the product and its users. Templates go wrong in predictable ways: a
refund clause that contradicts the App Store's rules, no licence for content users upload, an arbitration clause
that consumer law won't enforce, promises the product doesn't keep. So start from how the product really works and
who it's sold to, then write terms that match.

## Workflow

1. Learn the product and how it makes money
2. Ask for what you couldn't find
3. Draft
4. Check
5. Publish on Legiflare
6. Hand over

If the user already has a Legiflare terms document (step 5 checks), this is an update: read it first, keep what is
still true, and change what no longer fits.

### 1. Learn the product and how it makes money

Find out, from the conversation, the code and Legiflare (`get_profile`, `list_documents`):

- What the product does, and whether it's sold to consumers, businesses or both. Consumer law limits what terms
  can say; business terms can go further.
- Who runs it, in which country, and where its users are.
- Accounts: whether users sign up, what age they must be, and how they delete their account.
- Money: free, one-time purchases, subscriptions, free trials, usage-based billing. Who takes the payment matters:
  App Store or Google Play billing (`StoreKit`, `react-native-iap`, `react-native-purchases`, Play Billing), a
  processor such as Stripe or PayPal where the operator is the seller, or a merchant of record such as Paddle or
  Lemon Squeezy, which sells to the customer itself under its own buyer terms.
- User content: uploads, posts, comments, messages, profiles; whether others can see it; whether there's
  moderation or reporting.
- AI features: generated text, images or code, and which provider runs them.
- Anything else that brings its own rules: a marketplace between users, an API for developers, physical goods,
  regulated areas (health, finance, gambling, education for children).

Read the user's other Legiflare documents, if any: the terms should link to the privacy policy and refund policy and
must not contradict them.

### 2. Ask for what you couldn't find

Usual gaps: the operator's legal name and address or country, the contact email, the minimum age, the governing law
and courts, how disputes are resolved, the refund approach (or a refund policy to link to), and whether there's a
service level promise. Ask in one message, suggesting a default for each: courts of the operator's home country,
minimum age 13 (or 16, the highest age of digital consent in the EU, for services aimed at EU users), no
arbitration, refunds as the store or the refund policy says.

If the user wants to skip the questions, draft with clearly marked placeholders and publish the document hidden
(`visible: false`) until they fill them in.

### 3. Draft

Pick the sections that apply:

1. **Agreement**: who "we" are, which products the terms cover, that using them means accepting the terms, and
   "Last updated: <date>".
2. **Eligibility**: minimum age, and authority to bind a company when a user signs up for one.
3. **Accounts**: accurate details, keeping credentials safe, responsibility for activity, how to close the account.
4. **The service**: what it is, that features may change, no availability guarantee unless there's an SLA.
5. **Payments and subscriptions**: prices, taxes, billing cycle, automatic renewal and how to cancel before it,
   free trials and what happens when they end, price changes and notice. For store purchases, say that Apple or
   Google bills, refunds and manages the subscription under their terms, and that users cancel in their store
   account settings. With a merchant of record, say that it is the seller and its buyer terms apply.
6. **Refunds**: a short summary and a link to the refund policy, consistent with it.
7. **User content**: users keep ownership; they grant only the licence needed to host, show and operate the
   service (and to promote it, if that's intended, said plainly); they're responsible for having the rights to
   what they upload; how content is moderated and reported. Products in the US that host user content should say
   how to send copyright notices (DMCA); the safe harbour also needs a designated agent registered with the U.S.
   Copyright Office, which the user has to do themselves.
8. **Acceptable use**: what users may not do, written for this product, not a generic list of forty items.
9. **AI features**: outputs can be wrong and aren't professional advice; users are responsible for how they use
   them; who owns the outputs; users must not submit others' personal data or content without the right to.
10. **Intellectual property**: the product, its brand and content belong to the operator; feedback may be used.
11. **Third-party services and links**.
12. **Suspension and termination**: when the operator may suspend or close accounts, what happens to data and
    prepaid fees.
13. **Disclaimers** and **limitation of liability**.
14. **Indemnity**, mainly for business users; keep it proportionate for consumers.
15. **Governing law and disputes**.
16. **Changes to these terms**: how users are told, and when changes take effect.
17. **General**: entire agreement, severability, assignment, no waiver.
18. **Contact**.

Rules that change what the sections say:

- **Consumers in the EU and UK** keep the mandatory protections of their own country whatever law the terms choose,
  and terms can't exclude liability for death or personal injury caused by negligence, or for fraud. They have a
  14-day right to withdraw from online purchases; for a service or digital content that starts at once, that right
  is lost or paid for pro rata only when the user expressly asked for it to start and acknowledged this (the
  refund-policy skill covers the details). Unfair or surprising clauses are not binding on them. Don't add the
  link to the EU online dispute resolution platform: it closed in July 2025.
- **Consumers in Turkey** keep their rights under the Consumer Protection Law No. 6502. Online sales to them also
  need a pre-contract information form (ön bilgilendirme formu) and a distance sales contract (mesafeli satış
  sözleşmesi); offer to publish them as separate documents (type "Other").
- **US**: arbitration and class action waivers are common but need care and clear presentation; leave them out
  unless the user asks. California's automatic renewal law requires clear terms before purchase and an easy way to
  cancel online.
- **iOS apps**: without their own EULA, App Store apps use Apple's standard EULA. When these terms serve as the
  app's EULA, they must include Apple's minimum terms: the agreement is between the user and the developer, not
  Apple; the licence is limited to Apple devices the user owns or controls under the App Store's usage rules; the
  developer, not Apple, is responsible for maintenance, support, warranty, product claims and intellectual property
  claims; the user confirms they're not in an embargoed country or on a prohibited-party list; the developer's name,
  address and contact; that third-party terms (such as a wireless data plan) apply; and that Apple and its
  subsidiaries are third-party beneficiaries who may enforce the agreement. Apps with auto-renewing subscriptions
  must link the terms of use and privacy policy inside the app and in the App Store metadata.

Write in plain language, addressed to the reader as "you", with short sections. Use the language the user asks for;
if they don't say, use the language of the product's audience, and ask when that's unclear.

### 4. Check

- Nothing contradicts the privacy policy, the refund policy or the store's rules.
- Every promise is one the product keeps (availability, support, deletion, notice periods).
- Payment, renewal and cancellation terms match how billing really works.
- No placeholders such as "[Company Name]", no sample text.

### 5. Publish on Legiflare

Legiflare hosts the document at a public URL that stays the same when the document is edited, so the link can go
into sign-up screens, store listings and footers once. Its MCP server (`https://mcp.legiflare.com/mcp`) gives you
these tools: `get_profile`, `list_document_types`, `list_documents`, `get_document`, `create_document`,
`update_document` and `delete_document`.

1. Call `list_documents`. If the user already has terms of service for this product, read them with
   `get_document` and change them with `update_document`: the URL may already be linked from the app or a store
   listing, and a second copy would leave the old one stale. Create a new document only for a different product,
   or when the user asks.
2. Call `list_document_types` and use the ID of "Terms of Service". Look it up each time rather than assuming a
   number.
3. Call `create_document` (or `update_document` with the document's `id`):
   - `title`: the document and the product, such as "Terms of Service for Acme Notes" (3–255 characters).
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
https://github.com/hamdisproject/legiflare-skills#install.
If they'd rather not, save the document as an HTML file in their project instead. If a tool says the
sign-in has expired, ask them to reconnect.

### 6. Hand over

Tell the user:

- the URL;
- in a few lines, what the terms cover, and the choices you made for them (governing law, minimum age, disputes);
- what they must do outside the document, if anything: register a DMCA agent, add the store EULA, publish the
  Turkish pre-contract documents;
- where the link goes: the sign-up or checkout screen ("By continuing you agree to the Terms of Service and the
  Privacy Policy"), the app's settings or about screen, the website footer, and for subscription apps the App Store
  description or EULA field.

Add in one line that this isn't legal advice, and suggest a lawyer's review for marketplaces, regulated industries
and large business contracts. For an update, list what changed and remind the user that the terms may require
telling users before changes take effect.

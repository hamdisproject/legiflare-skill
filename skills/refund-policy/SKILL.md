---
name: refund-policy
description: Write or update a refund, return or cancellation policy that matches how a product is sold (App Store or Google Play purchases, subscriptions, SaaS plans, digital downloads, physical goods) and the consumer law where its customers are, and publish it on Legiflare at a public URL. Use this whenever the user needs a refund policy, return policy, money-back guarantee or cancellation policy, a payment provider or marketplace (Stripe, Paddle, Lemon Squeezy, Shopify, Google Merchant Center) asks for one, or the user wants to change the refund terms in an existing Legiflare document, even if they don't mention Legiflare.
---

# Refund policy

A refund policy has to agree with three things: what the business really does, who really processes refunds (Apple
and Google refund store purchases themselves; a merchant of record such as Paddle refunds under its own terms),
and the refund and withdrawal rights consumers have by law. A policy may be more generous than the law, never
less, and it can't promise refunds the business has no way to give.

## Workflow

1. Learn how the product is sold
2. Work out the rules that apply
3. Ask for the business's own choices
4. Draft
5. Check
6. Publish on Legiflare
7. Hand over

If the user already has a Legiflare refund policy (step 6 checks), this is an update: read it first and change
what no longer matches.

### 1. Learn how the product is sold

Find out from the conversation, the code and Legiflare (`get_profile`, `list_documents`):

- What is sold: subscriptions, one-time digital purchases (apps, downloads, credits, courses), services, physical
  goods.
- Through which channel: App Store or Google Play billing (`StoreKit`, `react-native-iap`,
  `react-native-purchases`, Play Billing), a processor where the business is the seller (Stripe, PayPal, Shopify
  Payments), or a merchant of record (Paddle, Lemon Squeezy).
- Free trials, renewals, proration on plan changes, usage limits.
- What the business already does: refund or cancel endpoints, Stripe refund calls, cancellation flows, existing
  terms of service. The policy should describe that, or the user should decide to change it.
- Where the customers are, and whether they're consumers or businesses.

### 2. Work out the rules that apply

**By channel:**

- **App Store**: Apple handles every refund and the developer can't issue one. Customers request refunds at
  https://reportaproblem.apple.com. Subscriptions are managed and cancelled in the Apple Account's subscription
  settings; cancelling at least 24 hours before the renewal date avoids the next charge.
- **Google Play**: refunds follow Google Play's refund policies (https://support.google.com/googleplay/answer/2479637).
  Customers can often get a refund through Google Play shortly after purchase; after that the developer can refund
  from Play Console. Subscriptions are cancelled in the Play Store under Payments & subscriptions.
- **Merchant of record**: Paddle or Lemon Squeezy is the seller and its buyer terms set the minimum refund rights.
  Don't promise less than they do, and send customers to the merchant of record for refunds (for Paddle,
  https://paddle.net).
- **Direct sales** (Stripe, PayPal, Shopify): the business sets the rules within consumer law. Refunds go back to
  the original payment method and usually take 5–10 business days to appear.

**By customer location** (for consumers; business customers generally get what the contract says):

- **EU and EEA**: a 14-day right to withdraw from online and other distance contracts, without giving a reason.
  - Physical goods: 14 days from delivery. The refund, including standard delivery costs, is due within 14 days of
    the withdrawal notice; the seller may wait until the goods are back or the customer shows they were sent. The
    customer pays return shipping only if told so beforehand.
  - Digital content not on a physical medium (downloads, in-app content): the right ends once delivery starts, but
    only if the customer expressly agreed to immediate delivery and acknowledged losing the right, and the seller
    confirmed this. Without that, the 14 days apply.
  - Services, including SaaS subscriptions: 14 days from the contract. If the customer expressly asked for the
    service to start during that time, they pay for what they used when withdrawing, and the right ends once the
    service has been fully performed.
  - The customer must be given the model withdrawal form (below), and the legal guarantee for faulty goods (at
    least two years) applies whatever the refund policy says.
- **UK**: the same 14-day rules under the Consumer Contracts Regulations 2013; faulty goods can be rejected for a
  full refund within 30 days under the Consumer Rights Act 2015.
- **Turkey**: a 14-day right of withdrawal (cayma hakkı) under the Distance Contracts Regulation (Mesafeli
  Sözleşmeler Yönetmeliği), with the refund due within 14 days of the notice. Exceptions include digital content
  delivered instantly and services performed at once with the consumer's approval.
- **United States**: no general legal right to a refund, but some states require a seller that doesn't give full
  refunds to post its policy conspicuously (California, New York). Automatic renewal laws, such as California's,
  require clear renewal terms and an easy way to cancel online.
- **Australia**: consumer guarantees under the Australian Consumer Law can't be excluded; a "no refunds" policy is
  unlawful for faulty products or services.

The EU model withdrawal form, for EU and UK sales (fill in the business's name, address and email, and keep the
rest word for word):

> To [name, geographical address and email address of the business]:
> I/We (\*) hereby give notice that I/We (\*) withdraw from my/our (\*) contract of sale of the following goods
> (\*)/for the provision of the following service (\*),
> Ordered on (\*)/received on (\*),
> Name of consumer(s),
> Address of consumer(s),
> Signature of consumer(s) (only if this form is notified on paper),
> Date
> (\*) Delete as appropriate.

### 3. Ask for the business's own choices

Usual questions: the refund window or money-back guarantee (14 or 30 days, or none beyond the law), full,
partial or prorated refunds, whether partial subscription periods are refunded, conditions (unused, within a usage
limit), how to ask (email, form, in-app), how quickly refunds are processed, for goods who pays return shipping and
whether exchanges are offered, and what can't be refunded. Ask in one message, suggest a default for each, and
don't ask what the code or the store already decides.

If the user wants to skip the questions, draft with clearly marked placeholders and publish the document hidden
(`visible: false`) until they fill them in.

### 4. Draft

1. **Summary**: the main rule in two or three sentences, in a `blockquote` at the top, and "Last updated: <date>".
2. **Purchases through the App Store or Google Play**, when the product is sold there.
3. **Purchases on our website**: subscriptions (cancelling, renewal, trials, what happens to the remaining period),
   one-time purchases, and the refund window and conditions.
4. **Returns of physical goods**, when there are any: condition, window, shipping costs, exchanges.
5. **Your legal rights**: the statutory withdrawal right for the regions served, with the model withdrawal form
   for the EU and UK.
6. **How to request a refund**: the steps, the address or form, what to include.
7. **When you'll get your money back**: processing time and method.
8. **Exceptions**, if any, without overriding the legal rights above.
9. **Changes to this policy** and **Contact**.

Write in plain language, addressed to the reader as "you". Use the language the user asks for; if they don't say,
use the language of the customers.

### 5. Check

- Nothing contradicts the store's or merchant of record's rules, the terms of service, or the legal rights for
  the regions served.
- Windows, amounts and contact details are the same as in the user's other documents.
- No placeholders, no sample text.

### 6. Publish on Legiflare

Legiflare hosts the document at a public URL that stays the same when the document is edited, so the link can go
into checkout pages, payment provider settings and footers once. Its MCP server (`https://mcp.legiflare.com/mcp`)
gives you these tools: `get_profile`, `list_document_types`, `list_documents`, `get_document`, `create_document`,
`update_document` and `delete_document`.

1. Call `list_documents`. If the user already has a refund policy for this product, read it with `get_document`
   and change it with `update_document`: its URL may already be linked from checkout or a payment provider, and a
   second copy would leave the old one stale. Create a new document only for a different product, or when the
   user asks.
2. Call `list_document_types` and use the ID of "Refund Policy". Look it up each time rather than assuming a
   number.
3. Call `create_document` (or `update_document` with the document's `id`):
   - `title`: the document and the product, such as "Refund Policy for Acme Notes" (3–255 characters).
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

**If the Legiflare tools aren't available**, tell the user how to connect them: in Claude Code,
`claude mcp add --transport http legiflare https://mcp.legiflare.com/mcp`, then sign in from `/mcp`; in Claude,
add `https://mcp.legiflare.com/mcp` as a custom connector. Sign-in happens in the browser with their Legiflare
account. If they'd rather not, save the document as an HTML file in their project instead. If a tool says the
sign-in has expired, ask them to reconnect.

### 7. Hand over

Tell the user:

- the URL;
- the main rule in one line, and the legal rights included for which regions;
- anything the business must do to make the policy true (for EU digital sales, the consent and acknowledgement
  checkbox at checkout; for goods, a returns address);
- where the link goes: checkout and pricing pages, the website footer, the terms of service, and the payment
  provider's or marketplace's business settings when they ask for it.

Add in one line that this isn't legal advice. For an update, list what changed.

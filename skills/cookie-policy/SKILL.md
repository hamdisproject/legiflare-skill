---
name: cookie-policy
description: Write or update a cookie policy that lists the cookies and similar technologies (local storage, pixels, SDK identifiers) a website really sets, with who sets each, why and for how long, and publish it on Legiflare at a public URL. Use this whenever the user needs a cookie policy or cookie notice, is setting up a cookie or consent banner, adds Google Analytics, AdSense, Meta Pixel, Hotjar or other trackers to a site, asks which cookies their site uses, or wants to update an existing Legiflare cookie policy, even if they don't mention Legiflare.
---

# Cookie policy

A cookie policy is a list that has to match what the site really does: each cookie, who sets it, why, and how long
it lasts. In the EU and UK, cookies that aren't strictly necessary may only be set after the visitor agrees, so
the policy also explains the categories a consent banner offers and how to change the choice later. Find the real
cookies first; a policy built from a generic list will be wrong.

## Workflow

1. Find the cookies
2. Put each in a category
3. Check how consent works
4. Ask for what you couldn't find
5. Draft
6. Check
7. Publish on Legiflare
8. Hand over

If the user already has a Legiflare cookie policy (step 7 checks), this is an update: read it, then add, change or
remove rows to match what the site sets now.

### 1. Find the cookies

**From the live site**, when you have a browser tool: open the site in a fresh session, accept all cookies on the
banner if there is one, and visit the main kinds of page (home, sign-in, checkout or pricing, a page with embedded
video or maps). List the cookies for the site's own domain and for third-party domains, with their expiry, and the
`localStorage` and `sessionStorage` keys. `document.cookie` doesn't show `HttpOnly` cookies, so read the browser's
cookie store or the `Set-Cookie` headers of network responses as well.

**From the code**:

- The framework's session and CSRF cookies: Spring `JSESSIONID`, Express `connect.sid`, PHP `PHPSESSID`, Laravel
  `laravel_session` and `XSRF-TOKEN`, Django `sessionid` and `csrftoken`, Rails `_<app>_session`, Auth.js
  `authjs.session-token` (`next-auth.session-token` before v5), ASP.NET Core `.AspNetCore.*`.
- Cookies the app sets: `Set-Cookie`, `res.cookie(`, `cookies().set(`, `document.cookie`, `setcookie(`, and
  `localStorage.setItem(`. The ePrivacy rules cover local storage and similar technologies the same way as
  cookies.
- Third-party scripts in layouts and templates, and the consent banner library.
- A tag manager (Google Tag Manager) can load tags the code doesn't show; check the live site or ask the user what
  the container loads.

[references/common-cookies.md](references/common-cookies.md) gives the usual names and lifetimes for common
services. Vendors change them and sites can configure them, so prefer what you observed and use the list to
recognise names and to fill in purposes.

### 2. Put each in a category

- **Strictly necessary**: needed for something the visitor asked for, such as staying signed in, the shopping
  cart, CSRF protection, load balancing, bot protection and remembering the consent choice itself. No consent
  needed.
- **Preferences**: language, theme, remembered settings.
- **Analytics**: measuring how the site is used.
- **Marketing**: advertising, retargeting, conversion tracking, social media pixels.

When a cookie could fit two categories, choose the one that needs consent. "Necessary" means the site can't do
what the visitor asked without it, not that the business finds it useful.

### 3. Check how consent works

Look at whether there's a banner, which categories it offers, and whether non-essential cookies wait for consent.
If analytics or ad cookies are set before the visitor agrees, tell the user: the policy can describe the cookies
but can't make the site compliant, and that has to be fixed in the code or the consent tool. Google requires a
Google-certified consent tool for AdSense, Ad Manager and AdMob ads shown in the EEA, the UK and Switzerland.

### 4. Ask for what you couldn't find

Usual gaps: the operator's name and contact email, the link to their privacy policy, how visitors reopen the
consent settings (a "Cookie settings" link in the footer, for example), and which tags a tag manager loads. Ask in
one message and suggest defaults.

If the user wants to skip the questions, draft with clearly marked placeholders and publish the document hidden
(`visible: false`) until they fill them in.

### 5. Draft

1. **Introduction**: who runs the site, which sites the policy covers, "Last updated: <date>", and a link to the
   privacy policy.
2. **What cookies are**: two or three sentences, including that the policy also covers local storage, pixels and
   similar technologies.
3. **How we use them**: each category with what it's for, and that only strictly necessary cookies are set
   without consent.
4. **The cookies we use**: one table per category with the columns Name, Provider, Purpose, Duration and Type
   (first-party or third-party). Give a duration such as "Session", "30 minutes" or "2 years", not "persistent".
5. **Managing cookies**: how to reopen the consent settings, how to delete or block cookies in the browser (Chrome:
   https://support.google.com/chrome/answer/95647, Firefox:
   https://support.mozilla.org/kb/clear-cookies-and-site-data-firefox, Safari:
   https://support.apple.com/guide/safari/manage-cookies-sfri11471/mac), and opt-outs for services in use, such as
   the Google Analytics opt-out add-on (https://tools.google.com/dlpage/gaoptout), Google's ad settings
   (https://myadcenter.google.com), Your Online Choices in the EU (https://www.youronlinechoices.com) and the
   Digital Advertising Alliance in the US (https://optout.aboutads.info).
6. **Changes to this policy**.
7. **Contact**.

Write in plain language, addressed to the reader as "you". Use the language the user asks for; if they don't say,
use the language of the site.

### 6. Check

- Every cookie and storage key you found is in a table, and nothing is listed that the site doesn't set.
- Durations are the real ones, and the categories match the banner's.
- The privacy policy mentions cookies and links here (offer to update it if it doesn't).
- No placeholders, no sample text.

### 7. Publish on Legiflare

Legiflare hosts the document at a public URL that stays the same when the document is edited, so the link can go
into the consent banner and the footer once. Its MCP server (`https://mcp.legiflare.com/mcp`) gives you these
tools: `get_profile`, `list_document_types`, `list_documents`, `get_document`, `create_document`,
`update_document` and `delete_document`.

1. Call `list_documents`. If the user already has a cookie policy for this site, read it with `get_document` and
   change it with `update_document`: its URL may already be linked from the banner, and a second copy would leave
   the old one stale. Create a new document only for a different site, or when the user asks.
2. Call `list_document_types` and use the ID of "Cookie Policy". Look it up each time rather than assuming a
   number.
3. Call `create_document` (or `update_document` with the document's `id`):
   - `title`: the document and the site, such as "Cookie Policy for acme.com" (3–255 characters).
   - `documentTypeId`: from step 2.
   - `description`: one plain sentence for listings (up to 255 characters).
   - `content`: the HTML described below.
   - `visible`: `true` to publish. Use `false` while placeholders remain or the user wants to read it first; a
     hidden document's page shows nothing until it is made visible.
4. Give the user the `url` from the result.

`update_document` changes only the fields you send, so send the complete new `content`, not a fragment.

**Content format.** The page renders `content` as HTML below the document title:

- Use only `h2`, `h3`, `h4`, `p`, `ul`, `ol`, `li`, `strong`, `em`, `u`, `blockquote`, `table`, `thead`, `tbody`,
  `tr`, `th`, `td`, `a` and `br`. Cookie tables use `table`, `thead`, `tbody`, `tr`, `th` and `td`.
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

### 8. Hand over

Tell the user:

- the URL;
- how many cookies are listed per category, and any you couldn't confirm;
- any consent problem found in step 3;
- where the link goes: the consent banner, the footer next to the privacy policy, and the privacy policy itself.

Add in one line that this isn't legal advice. For an update, list the cookies added, changed and removed.

# Common cookies

Usual names and default lifetimes for common services. Sites can change lifetimes, and vendors rename cookies, so
use this to recognise what you find and to word its purpose; the duration in the policy should be what the browser
shows (the cookie's `Expires` or `Max-Age`). `<id>` stands for a site, project or container identifier.

## Contents

- [Framework session and security cookies](#framework-session-and-security-cookies)
- [Consent tools](#consent-tools)
- [Analytics](#analytics)
- [Advertising and social](#advertising-and-social)
- [Payments, security and support](#payments-security-and-support)
- [Embeds](#embeds)

## Framework session and security cookies

All strictly necessary, set by the site itself.

| Cookie | Set by | Purpose | Default duration |
| --- | --- | --- | --- |
| `JSESSIONID` | Java servlet containers, Spring | Keeps the visitor's session | Session |
| `remember-me` | Spring Security | Keeps the visitor signed in when they choose "Remember me" | 2 weeks |
| `XSRF-TOKEN` | Spring Security (cookie CSRF repository), Laravel, Angular apps | Protects forms against cross-site request forgery | Session (Laravel: as the session) |
| `connect.sid` | Express (`express-session`) | Keeps the visitor's session | Session, unless `maxAge` is set |
| `PHPSESSID` | PHP | Keeps the visitor's session | Session |
| `laravel_session` | Laravel | Keeps the visitor's session | 2 hours |
| `sessionid` | Django | Keeps the visitor's session | 2 weeks |
| `csrftoken` | Django | Protects forms against cross-site request forgery | 1 year |
| `_<app>_session` | Ruby on Rails | Keeps the visitor's session | Session |
| `authjs.session-token`, `next-auth.session-token` | Auth.js / NextAuth | Keeps the visitor signed in | 30 days |
| `authjs.csrf-token`, `next-auth.csrf-token` | Auth.js / NextAuth | Protects sign-in against cross-site request forgery | Session |
| `__session`, `__client_uat` | Clerk | Keep the visitor signed in (`__session` is short-lived and refreshed) | Check in the browser |

## Consent tools

Strictly necessary: they remember the visitor's choice.

| Cookie | Set by | Default duration |
| --- | --- | --- |
| `CookieConsent` | Cookiebot | 1 year |
| `cookieyes-consent` | CookieYes | 1 year |
| `OptanonConsent`, `OptanonAlertBoxClosed` | OneTrust | 1 year |

## Analytics

| Cookie | Set by | Purpose | Default duration |
| --- | --- | --- | --- |
| `_ga` | Google Analytics | Tells visitors apart | 2 years |
| `_ga_<id>` | Google Analytics 4 | Keeps session state | 2 years |
| `_hjSessionUser_<id>` | Hotjar | Tells visitors apart | 1 year |
| `_hjSession_<id>` | Hotjar | Keeps the current session's data | 30 minutes |
| `_clck` | Microsoft Clarity | Tells visitors apart and keeps settings | 1 year |
| `_clsk` | Microsoft Clarity | Joins page views into one session recording | 1 day |
| `CLID` (on `clarity.ms`) | Microsoft Clarity | Recognises the browser across sites using Clarity | 1 year |
| `ph_<id>_posthog` | PostHog | Tells visitors apart and keeps session state (also kept in local storage) | 1 year |
| `mp_<id>_mixpanel` | Mixpanel | Tells visitors apart and keeps event properties | 1 year |

Plausible and Vercel Web Analytics set no cookies.

## Advertising and social

All marketing, needing consent.

| Cookie | Set by | Purpose | Default duration |
| --- | --- | --- | --- |
| `__gads`, `__gpi` | Google AdSense, Ad Manager | Ad frequency, measurement and personalization on the site's domain | 13 months |
| `__eoi` | Google AdSense, Ad Manager | Ad security and fraud prevention | 6 months |
| `IDE` (on `doubleclick.net`) | Google advertising | Personalized ads and measurement across sites | 13 months in the EEA and UK, 2 years elsewhere |
| `_gcl_au` | Google Ads, Google Tag | Links ad clicks to conversions | 90 days |
| `_fbp` | Meta Pixel | Tells visitors apart for ads and measurement | 90 days |
| `_fbc` | Meta Pixel | Stores the last Facebook ad click (`fbclid`) | 90 days |

## Payments, security and support

| Cookie | Set by | Purpose | Category | Default duration |
| --- | --- | --- | --- | --- |
| `__stripe_mid` | Stripe | Fraud prevention | Strictly necessary | 1 year |
| `__stripe_sid` | Stripe | Fraud prevention | Strictly necessary | 30 minutes |
| `__cf_bm` | Cloudflare | Tells people from bots | Strictly necessary | 30 minutes |
| `cf_clearance` | Cloudflare | Remembers a passed challenge | Strictly necessary | Set by the site (30 minutes by default) |
| `_cfuvid` | Cloudflare | Rate limiting | Strictly necessary | Session |
| `_GRECAPTCHA` | Google reCAPTCHA | Tells people from bots | Strictly necessary | 6 months |
| `intercom-id-<id>`, `intercom-device-id-<id>` | Intercom | Recognises the visitor in the chat | Preferences | 9 months |
| `intercom-session-<id>` | Intercom | Keeps the chat conversation | Preferences | 1 week |

## Embeds

| Cookie | Set by | Purpose | Category | Default duration |
| --- | --- | --- | --- | --- |
| `YSC` | YouTube | Counts views and keeps playback settings | Marketing | Session |
| `VISITOR_INFO1_LIVE`, `VISITOR_PRIVACY_METADATA` | YouTube | Bandwidth estimate, recommendations and the visitor's consent state | Marketing | 6 months |

Embedding from `youtube-nocookie.com` avoids YouTube's cookies until the visitor plays the video.

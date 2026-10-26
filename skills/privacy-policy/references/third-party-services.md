# Common third-party services

What common services receive, how to spot them in a codebase, and the provider's privacy policy to link. Use it to
make sure the policy names every service the product uses, and only those.

- Describe a service as it's configured, not at its most invasive or its most private: check whether ad
  personalization is off, IP collection is disabled, consent mode is on, or session replay is enabled before
  saying so.
- Links were correct when this list was written. When you can browse, open each one you publish.
- A service missing from this list still belongs in the policy: describe it from its documentation.

## Contents

- [Analytics and session recording](#analytics-and-session-recording)
- [Crash reporting](#crash-reporting)
- [Advertising and attribution](#advertising-and-attribution)
- [Payments and subscriptions](#payments-and-subscriptions)
- [Sign-in and backend](#sign-in-and-backend)
- [Hosting and CDN](#hosting-and-cdn)
- [Email and messaging](#email-and-messaging)
- [Push notifications](#push-notifications)
- [AI providers](#ai-providers)
- [Support, maps and embeds](#support-maps-and-embeds)

## Analytics and session recording

| Service | How to spot it | What it receives | Privacy policy |
| --- | --- | --- | --- |
| Google Analytics 4 | `gtag(`, `googletagmanager.com/gtag/js`, `react-ga4`, `vue-gtag`, `GoogleAnalytics` from `@next/third-parties/google` | Pages and events, device and browser details, approximate location derived from the IP address (GA4 doesn't store IP addresses), cookie identifiers | https://policies.google.com/privacy, and how Google uses data from sites using its services: https://policies.google.com/technologies/partner-sites |
| Google Analytics for Firebase | `firebase/analytics`, `@react-native-firebase/analytics`, `firebase_analytics`, `FirebaseAnalytics`, `com.google.firebase:firebase-analytics` | App instance ID, device details, usage events, the advertising ID where available | https://firebase.google.com/support/privacy |
| Mixpanel | `mixpanel`, `mixpanel-browser`, `mixpanel-react-native` | Events, device details, IP-derived location, any user properties the app sets | https://mixpanel.com/legal/privacy-policy/ |
| Amplitude | `@amplitude/analytics-browser`, `@amplitude/analytics-react-native`, other `@amplitude/*` | Events, device details, IP-derived location, user properties | https://amplitude.com/privacy |
| PostHog | `posthog-js`, `posthog-node`, `posthog-react-native` | Events, device details, IP address unless discarded; screen recordings if session replay is on | https://posthog.com/privacy |
| Segment | `@segment/analytics-next`, `@segment/analytics-node` | Whatever events and traits are sent, forwarded to the destinations configured in Segment (list those too) | https://www.twilio.com/en-us/legal/privacy |
| Plausible | `plausible.io/js` | Aggregate visit statistics without cookies or persistent identifiers | https://plausible.io/privacy |
| Vercel Web Analytics, Speed Insights | `@vercel/analytics`, `@vercel/speed-insights` | Page views and performance metrics without cookies | https://vercel.com/legal/privacy-policy |
| Microsoft Clarity | `clarity.ms`, `@microsoft/clarity` | Session recordings, heatmaps, clicks and scrolls, device details | https://privacy.microsoft.com/privacystatement |
| Hotjar | `static.hotjar.com`, `@hotjar/browser` | Session recordings, heatmaps, survey answers, device details | https://www.hotjar.com/legal/policies/privacy/ |

## Crash reporting

| Service | How to spot it | What it receives | Privacy policy |
| --- | --- | --- | --- |
| Firebase Crashlytics | `firebase-crashlytics`, `FirebaseCrashlytics`, `firebase_crashlytics`, `@react-native-firebase/crashlytics` | Crash traces, device state, an installation identifier | https://firebase.google.com/support/privacy |
| Sentry | `@sentry/*`, `sentry-sdk`, `sentry_flutter`, `io.sentry`, the `Sentry` pod | Errors and stack traces, device or browser details, IP address unless turned off, the user ID or email if the app sets one | https://sentry.io/privacy/ |

## Advertising and attribution

Ads and retargeting usually count as "sharing" under California law and need consent in the EU and UK.

| Service | How to spot it | What it receives | Privacy policy |
| --- | --- | --- | --- |
| Google AdMob | `google-mobile-ads`, `react-native-google-mobile-ads`, `google_mobile_ads`, `play-services-ads`, `Google-Mobile-Ads-SDK`, `GADApplicationIdentifier` | Advertising ID, IP address, device details, ad interactions; personalized ads unless turned off | https://policies.google.com/privacy and https://policies.google.com/technologies/ads |
| Google AdSense, Ad Manager | `adsbygoogle`, `pagead2.googlesyndication.com`, `securepubads.g.doubleclick.net` | Cookies, IP address, browser details, ad interactions. Serving ads in the EEA, UK or Switzerland needs a Google-certified consent tool. | https://policies.google.com/privacy and https://policies.google.com/technologies/ads |
| Meta Pixel, Facebook SDK | `connect.facebook.net`, `fbq(`, `react-native-fbsdk-next`, `facebook_app_events`, `FBSDKCoreKit`, `com.facebook.android` | App or site events, cookie or device identifiers, advertising ID, IP address | https://www.facebook.com/privacy/policy/ |
| AppLovin | `applovin`, `AppLovinSDK` | Advertising ID, device details, IP address, ad interactions | https://www.applovin.com/privacy/ |
| Unity Ads | `com.unity3d.ads`, `UnityAds` | Advertising ID, device details, IP address, ad interactions | https://unity.com/legal/privacy-policy |
| AppsFlyer | `react-native-appsflyer`, `appsflyer_sdk`, `AppsFlyerLib` | Install and in-app events, advertising ID, IP address, device details | https://www.appsflyer.com/legal/privacy-policy/ |

## Payments and subscriptions

| Service | How to spot it | What it receives | Privacy policy |
| --- | --- | --- | --- |
| Stripe | `stripe`, `@stripe/stripe-js`, `@stripe/react-stripe-js`, `stripe-android`, `StripePaymentSheet`, `flutter_stripe` | Card and billing details, collected and processed by Stripe; the product keeps only what Stripe returns (card brand, last four digits, billing address) | https://stripe.com/privacy |
| PayPal | `@paypal/react-paypal-js`, `@paypal/paypal-js`, `paypal-checkout` | Payment and account details, processed by PayPal | https://www.paypal.com/webapps/mpp/ua/privacy-full |
| Paddle | `@paddle/paddle-js`, `cdn.paddle.com` | Name, email, address, payment details; Paddle is the merchant of record and sells to the customer | https://www.paddle.com/legal/privacy |
| Lemon Squeezy | `@lemonsqueezy/lemonsqueezy.js`, `lemon.js`, `lemonsqueezy.com/checkout` | Name, email, address, payment details; Lemon Squeezy is the merchant of record | https://www.lemonsqueezy.com/privacy |
| RevenueCat | `react-native-purchases`, `purchases_flutter`, `RevenueCat`, `com.revenuecat.purchases` | Purchase and subscription history, an app user ID, device details | https://www.revenuecat.com/privacy |
| Apple In-App Purchase | `StoreKit`, `react-native-iap`, `expo-in-app-purchases`, `in_app_purchase` | Payment is handled by Apple; the product receives transaction and receipt details, not card data | https://www.apple.com/legal/privacy/ |
| Google Play Billing | `com.android.billingclient`, `react-native-iap`, `in_app_purchase` | Payment is handled by Google; the product receives purchase tokens and order details | https://policies.google.com/privacy |

## Sign-in and backend

| Service | How to spot it | What it receives | Privacy policy |
| --- | --- | --- | --- |
| Firebase Authentication, Firestore, Storage | `firebase/auth`, `firebase/firestore`, `firebase/storage`, `@react-native-firebase/*`, `cloud_firestore` | Account details and whatever the app stores there | https://firebase.google.com/support/privacy |
| Supabase | `@supabase/supabase-js`, `supabase_flutter`, `supabase-py` | Account details and whatever the app stores there | https://supabase.com/privacy |
| Clerk | `@clerk/*` | Account details (email, name, profile picture from social sign-in), session and device details | https://clerk.com/legal/privacy |
| Auth0 | `@auth0/*`, `auth0` | Account details, sign-in history, IP address | https://www.okta.com/privacy-policy/ |
| Sign in with Apple | `expo-apple-authentication`, `sign_in_with_apple`, `AuthenticationServices` | Name and email, or a private relay address if the user hides theirs | https://www.apple.com/legal/privacy/ |
| Google Sign-In | `@react-oauth/google`, `google_sign_in`, `@react-native-google-signin/google-signin`, `GoogleSignIn` | Name, email, profile picture | https://policies.google.com/privacy |

## Hosting and CDN

Hosting providers see every request, including IP addresses, and store server logs. Name the ones the product runs
on.

| Service | How to spot it | Privacy policy |
| --- | --- | --- |
| Vercel | `vercel.json`, `@vercel/*`, `.vercel` | https://vercel.com/legal/privacy-policy |
| Netlify | `netlify.toml` | https://www.netlify.com/privacy/ |
| Cloudflare | `wrangler.toml`, `cf-` headers, Cloudflare in front of the domain | https://www.cloudflare.com/privacypolicy/ |
| Amazon Web Services | `aws-sdk`, `@aws-sdk/*`, `boto3`, CDK or Terraform AWS resources | https://aws.amazon.com/privacy/ |
| Google Cloud | `@google-cloud/*`, `app.yaml`, Cloud Run configuration | https://cloud.google.com/terms/cloud-privacy-notice |

## Email and messaging

| Service | How to spot it | What it receives | Privacy policy |
| --- | --- | --- | --- |
| Resend | `resend` | Recipient addresses and message content | https://resend.com/legal/privacy-policy |
| SendGrid, Twilio | `@sendgrid/mail`, `twilio` | Recipient addresses or phone numbers and message content | https://www.twilio.com/en-us/legal/privacy |
| Mailchimp | `@mailchimp/mailchimp_marketing`, `list-manage.com` forms | Subscriber emails and names, opens and clicks | https://www.intuit.com/privacy/statement/ |

## Push notifications

| Service | How to spot it | What it receives | Privacy policy |
| --- | --- | --- | --- |
| Firebase Cloud Messaging | `firebase/messaging`, `@react-native-firebase/messaging`, `firebase_messaging` | A device push token | https://firebase.google.com/support/privacy |
| OneSignal | `react-native-onesignal`, `onesignal_flutter`, `OneSignal`, `react-onesignal` | Push token, device details, any tags the app sets | https://onesignal.com/privacy_policy |
| Expo push notifications | `expo-notifications` with Expo's push service | A device push token and message content | https://expo.dev/privacy |

## AI providers

Whatever the product sends to a model provider (prompts, chat messages, uploaded files, user text) leaves the
product, so name the provider and what it receives. Whether it is used to train models depends on the provider's
current API terms and on paid or free tiers; check them before saying either way.

| Service | How to spot it | Privacy policy |
| --- | --- | --- |
| OpenAI | `openai` | https://openai.com/policies/privacy-policy/ |
| Anthropic | `@anthropic-ai/sdk`, `anthropic` | https://www.anthropic.com/legal/privacy |
| Google Gemini | `@google/genai`, `@google/generative-ai`, `google-generativeai`, `google-genai` | https://policies.google.com/privacy; under the Gemini API terms, data from unpaid use may be used to improve Google's products and data from paid use is not |

## Support, maps and embeds

| Service | How to spot it | What it receives | Privacy policy |
| --- | --- | --- | --- |
| Intercom | `@intercom/messenger-js-sdk`, `widget.intercom.io`, `intercom-react-native` | Chat messages, name and email if given, device details | https://www.intercom.com/legal/privacy |
| Google Maps | `@react-google-maps/api`, `maps.googleapis.com`, `google_maps_flutter`, `react-native-maps` with the Google provider | Map views, IP address, the location the app passes | https://policies.google.com/privacy |
| Mapbox | `mapbox-gl`, `@rnmapbox/maps` | Map views, IP address, device details, the location the app passes | https://www.mapbox.com/legal/privacy |
| Google reCAPTCHA | `google.com/recaptcha`, `react-google-recaptcha` | Device and browser details and IP address, to tell people from bots; Google asks sites to disclose it | https://policies.google.com/privacy |
| Cloudflare Turnstile | `challenges.cloudflare.com/turnstile` | Browser signals and IP address, to tell people from bots | https://www.cloudflare.com/privacypolicy/ |
| YouTube embeds | `youtube.com/embed`, `youtube-nocookie.com/embed` | Viewing activity, cookies (the `youtube-nocookie.com` domain sets none until the video plays) | https://policies.google.com/privacy |

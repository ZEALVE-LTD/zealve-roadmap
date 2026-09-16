# RESEARCH — notes and backlog

Everything we learned / still need to learn, so no feature starts from
a blank page (process rule #1).

## Done — September 2026 (geo-localization + analytics + design)

### Geo/IP-based localization best practice
- **Country from IP**: prefer CDN country headers when present
  (`cf-ipcountry`, `x-vercel-ip-country`, `x-geo-country`,
  `fastly-client-country`); fall back to an offline IP→country database
  (we bundle `geoip-country`, no outbound calls, no PII leakage).
- **Language ≠ country**: browser `Accept-Language` beats IP for
  *language*; IP beats headers for *market voice* (currency, local
  tone, examples). We combine: country decides the default
  language *variant* (SA→ar-SA Saudi voice, BD→bn-BD, IN→bn-IN Kolkata
  voice, AE/KW/QA/BH/OM→Gulf Arabic, DE/AT→de, JP→ja, VN→vi, TH→th),
  `Accept-Language` decides when the country is unknown.
- **User override always wins**: visible language + currency switchers
  in the header; every locale gets a crawlable `?lang=` URL that sets a
  year-long cookie and 308-redirects to the clean URL; `hreflang`
  alternates point at those URLs.
- **Currency**: estimator math is ratio-based, so inputs/outputs are
  interpreted in the visitor's currency — no fake FX conversion, no
  fake prices. Tier defaults (order values, ad spend, loaded hourly
  cost) adapt by market: gulf / na / we / emea / sasia / sea / oceania
  / latam / africa.
- **RTL**: never hide elements with `left:-9999px` — under `dir=rtl`
  Chromium extends the scrollable canvas and composites a blank page
  (found and fixed via CSS bisect; the skip-link now uses
  `transform: translateY(-200%)`).

### Analytics options evaluated
- **Google Analytics 4** (`@next/third-parties` or inline gtag): traffic
  sources, funnels, demographics. Chosen — inline gtag injection from a
  DB-stored ID (no extra dependency, operator configures from admin).
- **Google Tag Manager**: for custom tag recipes; supported but optional.
- **Meta (Facebook) Pixel**: retargeting; inline fbq injection from
  admin-stored ID.
- **Microsoft Clarity**: free session recordings + heatmaps — best
  "what are visitors actually doing" tool for the money; supported via
  admin-stored project ID.
- **First-party events**: our own `analytics_events` table +
  `navigator.sendBeacon('/api/track')` — numbers we own regardless of
  third parties (pageviews, form starts/submits, estimator runs,
  language/currency switches, pricing interest, voice notes, community
  clicks). Admin dashboard tab renders aggregates.

### Lead capture v2 patterns
- Mandatory fields kept to **name + email**; everything else optional
  and collapsible so the form never looks heavy.
- **Phone with IM platform choice** (WhatsApp/Viber/Telegram/Messenger/
  Skype/LINE/WeChat/call) — Gulf and South Asia are IM-first; a bare
  phone number is less useful than the channel it belongs to.
- **Voice notes** (MediaRecorder in-browser + audio upload fallback) —
  founders can hear the use case in the customer's own words; stored in
  the DB, played from the admin leads tab, never public.
- **Product interest auto-selects from the page** the visitor is on,
  multi-select allowed.

### Design language (markopolo.ai school, ONYX base)
- Dark premium canvas + one vivid accent; bold two-tone headlines;
  aurora gradient fields; glass cards; scroll-reveal; animated
  counters; marquees; gamified badges/persona switchers; live product
  mockups built as real HTML (no raster page designs).
- References: markopolo.ai solutions pages, linear.app restraint,
  vercel.com type scale.

## Research backlog (deep-dive before each feature)

1. **MCP connector directory** (Forge 1.1): existing MCP server
   registries; first-party MCP/SDK availability for Shopify, Salla,
   Odoo, Meta Ads, Google Ads, WhatsApp Business; OAuth per platform;
   safety model for "configure without leaving Forge".
2. **Hosted long-running tasks** (Forge 1.2): container orchestration
   candidates (Fly Machines, RunPod, Modal, ACI), pricing per
   container-hour, sandboxing, queue UX, tunnel/pairing tech for local
   connect (Tailscale Funnel, WebSocket relay, QR pairing).
3. **Mobile Forge** (Forge 1.2): Expo reuse from Chatroom, push-driven
   approvals, phone→local pairing flow.
4. **Model credit accounting** (Forge 1.3): LiteLLM/OpenRouter ledger
   patterns, per-model allowance tables, abuse controls.
5. **AI-vs-human efficiency measurement** (Forge 1.4): activity
   attribution approaches, employee-privacy law per market (EU works
   councils, PDPL), transparent dashboards.
6. **Pricing module** (§2): willingness-to-pay interviews with alpha
   cohort, per-seat vs usage vs package hybrids in adjacent tools
   (Intercom/Fin, WATI, respond.io, Jasper), quote workflow software.
7. **Locale expansion** (§5): tr/id/es/fr dictionary tone guides,
   localized FAQ bodies, market-specific case studies.
8. **Country landing pages** (§7): per-market search-term research
   (Arabic/Bengali/German/Japanese/Vietnamese/Thai keyword sets),
   hreflang roll-out plan, local payment-method mentions per market.

# ROADMAP — to-dos and feature ideas

Owner: Navid. Source: founder directives, September 2026. Statuses:
`idea` → `research` → `spec` → `build` → `alpha` → `live`.
Before moving a card to `spec`, follow the process rules in README.md.

## 1. Forge (flagship — reposition as the generic empowerment tool)

Forge is not just an engineering tool. Regular people, marketers,
researchers, educators and healthcare admins should all see themselves
in it. Website copy already reflects the three comfort levels
(regular / experimental / power-advanced); product work below.

### 1.1 MCP connector directory — `idea`
- Ship a directory of ready-made MCP connectors so users can attach the
  tools they already use: **Shopify, Salla, Odoo, WhatsApp Business,
  Meta Ads, Google Ads, Sheets/Excel, Notion, ERP systems**.
- For each connector: what it can read/configure, what reports it can
  pull, security model (what Forge is allowed to touch).
- Pitch for business users: "configure Shopify, Salla or Odoo from one
  screen; pull every report without opening those dashboards; run any
  agent against them — without leaving Forge."
- Research needed: MCP server registries (existing lists), which
  platforms ship first-party MCP servers, auth flows per platform.

### 1.2 Runs anywhere: cloud, VM, containers, mobile, local — `idea`
- **Hosted long-running tasks**: users park a long task on Zealve-hosted
  VMs/containers; results land back in Forge. **Monetizable** — this is
  the first candidate paid service after the alpha.
- **Remote deployment**: Forge drives deploys to user VMs/containers.
- **Mobile**: bring Forge to phones — give a command from anywhere, it
  runs on the cloud fleet. Payment plan attaches to hosted capacity.
- **Local connect (tunnel)**: like z/gh codespace pairing — generate a
  scan-URL/QR that pairs the phone with the user's own laptop daemon so
  the local machine becomes the executor.
- Research needed: container orchestration options (Fly/Runpod/ACI),
  tunnel tech (tailscale/tspro/websocket relay), mobile shell
  (Expo reuse from Chatroom).

### 1.3 Bring your own API key + free model credits — `idea`
- Subscribed members get a monthly allowance of **free model credits /
  leads** with particular models depending on their package; BYO keys
  remove margin risk for heavy users.
- Research needed: credit-accounting patterns (LiteLLM/OpenRouter
  style), abuse controls, package design.

### 1.4 Enterprise efficiency measurement — `idea`
- Employers can't measure how much work is human vs AI-assisted today.
- Forge ships a **built-in monitored browser** + task ledger: every
  action attributable (agent vs human), per employee efficiency matrix,
  AI-leverage scoring. Strong enterprise hook; privacy-sensitive —
  spec transparent employee-visible measurement.
- Research needed: time-and-activity tool landscape, works-council /
  privacy constraints per market.

### 1.5 Marketing/research/education/healthcare use cases — `research`
- Marketers: configure ad tools + pull cross-platform reports from one
  place (pairs with AdPilot).
- Researchers: literature triage, dataset pipelines on own hardware.
- Education/healthcare: guided "regular view" flows for non-technical
  staff; publish per-industry templates.

### 1.6 Centralization thesis — `idea`
- Zealve already owns Chatroom (comms) and AdPilot (ads); Forge becomes
  the **central command point** that accumulates all of them: one
  screen, every tool, mobile + desktop + cloud.

## 2. Pricing module — `blocked on alpha data`
- No prices are published anywhere (site + agents + emails) until the
  alpha cohort gives real willingness-to-pay data.
- Design a pricing spec here first: packages (Starter/Growth/Scale
  shapes), per-product vs bundle, credit allowances, quote workflow
  (form → personal reply), founding-member terms.
- Interim: "request a quote" forms (already live on every page).

## 3. Community — `build`
- Founder community group (WhatsApp/Discord) — URL is configurable in
  the zealve-web admin panel (Settings tab) and appears in the footer
  once set.
- Later: private alpha cohort channel with direct line to the build team.

## 4. Analytics & growth instrumentation — `live, iterate`
- First-party events (pageview, form_start/submit, estimate_run,
  language_switch, currency_switch, pricing_interest, voice_note,
  community_click) with an admin dashboard — done.
- GA4 / GTM / Meta Pixel / Microsoft Clarity paste-in config from the
  admin Settings tab — done; needs operator IDs.
- Next: UTM capture on leads, source→revenue join for waves, weekly
  digest email.

## 5. Localization — `live, expand`
- Live: en, ar (Gulf), ar-SA (Saudi voice), bn-BD, bn-IN (Kolkata
  voice), de, ja, vi, th — IP/country default + visible switchers +
  ?lang= URLs + hreflang alternates.
- Expand: tr, id, es, fr (dictionaries fall back to English today for
  deep copy); localize FAQ bodies and estimator labels per locale.

## 6. RMS — `live, iterate`
- Customer ordering app + operations backend surfaces on the landing
  page — done (mocks); product repos carry the build.
- Next: per-country menu/currency presets in the ordering PWA, rider
  network integrations by market.

## 7. SEO / AEO — `live, iterate`
- llms.txt + llms-full.txt, MCP server endpoint (/api/mcp), FAQPage +
  Organization + SoftwareApplication JSON-LD, hreflang alternates —
  done.
- Next: country-targeted landing copy per market, agent-facing Q&A
  expansion, locale-specific sitemaps.

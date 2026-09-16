# Zealve Roadmap & Spec Repository

Single home for product to-dos, feature specs and research notes that
are **not** part of any single code repository. Marketing-site work
lives in [zealve-web](https://github.com/ZEALVE-LTD/zealve-web); product
specs, ideas and the research backlog live here.

## Process rules (read before starting ANY feature)

1. **Deep-dive research first.** Before writing a single line of code
   for a new feature, do a research pass: competitor scans, pricing
   models of similar tools, API/SDK docs of the platforms involved,
   and a written summary committed here (in `RESEARCH.md` or a spec
   file). No feature starts from a blank page.
2. **Use Open Design for design work.** Any UI feature must start from
   the Open Design corpus (`github.com/nexu-io/open-design`) plus the
   ONYX design language in `zealve-web` (`app/globals.css`, tokens).
   Use its HTML template functions / real HTML components / partial
   crops of design images — **never paste full-page raster designs**
   into the site.
3. **Business language rule.** Marketing copy on zealve.com speaks in
   outcomes (problem solved, money saved, growth enabled), not
   technical jargon. Engineering detail belongs in docs/specs, not on
   landing pages.
4. **No published pricing.** Prices are not decided. Every page routes
   pricing interest to the quote-request form. When the pricing module
   is designed (after the alpha cohort gives us data), spec it here
   first.
5. **Definition of done.** Feature ships with: i18n keys for the
   supported locales, SEO/AEO metadata (FAQ + JSON-LD where relevant),
   analytics events, mobile check at 390px, Playwright verification,
   and a commit pushed to both remotes (ZEALVE-LTD primary +
   navidRashik mirror).
6. **Alpha framing.** Advanced/experimental features are future paid
   add-ons; core stays free during testing. Copy marks them as alpha.

## Repos in the ecosystem

| Repo | Purpose |
|------|---------|
| ZEALVE-LTD/zealve-web | zealve.com marketing site (Next.js 15) |
| ZEALVE-LTD/chatroom | Chatroom product |
| ZEALVE-LTD/rms-pos-local | RMS on-premise POS terminal |
| ZEALVE-LTD/rms-consumer-app | RMS customer-facing ordering PWA |
| ZEALVE-LTD/plate-to-pallet-planner | Supply-chain planner |
| ZEALVE-LTD/hotels | Hotels channel manager |
| ZEALVE-LTD/Zealve.com | Legacy site |

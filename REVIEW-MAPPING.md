# REVIEW-MAPPING — Product ↔ Research ↔ Features ↔ Review-Kit Rating Map

Date: 2026-09-20 · Reviewer: AI review agent (review-kit installed; graphify graph available)
Purpose: map every Zealve product to its research docs and the full feature surface that must be
tested, so no feature is missed. Reports are written per-repo as `PRODUCT_REVIEW.md` on `main`.

## 1. Portfolio map

| Product | Repo(s) | Research docs (zealve-research) | Roadmap sections (zealve-roadmap) | Live surface |
|---|---|---|---|---|
| RMS platform core | ZEALVE-LTD/rms | rms/01-market-leaders.md, rms/02-startups.md, rms/03-supplier-catalog-providers.md, 00-current-state-zealve.md (Part 1), 04-gap-analysis, 11-adoption-audit | ROADMAP RMS sections | https://slateblue-ram-764267.hostingersite.com (Django) |
| RMS owner dashboard | ZEALVE-LTD/RMS_nextjs_Dashboard | 00-current-state (§1 dashboard rows) | ROADMAP RMS | — (talks to rms API) |
| RMS consumer app | ZEALVE-LTD/rms-consumer-app | 00-current-state ("consumer app 100% mock" claim to re-verify), 04-gap (real consumer API = GO-NEXT #1) | ROADMAP RMS | — |
| RMS on-prem POS | ZEALVE-LTD/rms-pos-local | 00-current-state §1 POS rows, 13-app-distribution-checklist | ROADMAP POS items | — (Tauri desktop) |
| Chatroom | ZEALVE-LTD/chatroom | chatroom/01-market-leaders.md, chatroom/02-startups.md, 12-whatsapp-approval-bd-now.md, 14-adpilot-chatroom-convergence.md | ROADMAP chatroom | https://midnightblue-dunlin-112756.hostingersite.com |
| Hotels | ZEALVE-LTD/hotels | hotels/research/* (in-repo), rms/03 supplier catalogs | ROADMAP | — |
| Zealve marketing site | ZEALVE-LTD/zealve-web (canonical; navidRashik mirror) | 11-adpilot-verdict.md, adpilot/*, 08-gtm | ROADMAP Forge §1 | https://zealve.com |
| AdPilot (product line) | designs + research only (adpilot/*.html, 14-convergence) — NO standalone code repo | adpilot/01,02,03,05, 11-adpilot-verdict, 14-convergence | ROADMAP | marketing pages on zealve.com |
| Forge | navidRashik/forge | forge/01-tooling-deepdive, forge/02-experimental-ledger, forge/03-main-roadmap-ledger, forge/04-modes-tasklist | ROADMAP §1 (flagship) | — |
| review-kit | navidRashik/review-kit | (tool used for this review) | — | — |
| Zealse | ZEALVE-LTD/zealse | (older product, plan/ + tasks.md in-repo) | — | — |
| Zealve.com (legacy) | ZEALVE-LTD/Zealve.com | — | — | superseded by zealve-web? |
| Plate-to-Pallet | ZEALVE-LTD/plate-to-pallet-planner | — | — | Lovable/Vite app |
| Zealve Clinic | ZEALVE-LTD/zealve-clinic | — | — | buildout Python |
| rms-app (RN) | ZEALVE-LTD/rms-app | — | — | react-native-reusables starter |

## 2. Feature surface to test per product (from research + READMEs; verify each)

### rms (Django core)
Auth+OTP/knox · multi-tenant roles (owner/manager/waiter) · menu+modifiers CRUD · dine-in order
status machine · takeaway orders · tables+QR · invoices+payment confirm · payment types · promo
codes · raw-material inventory · recipes+auto-deduct · reports · FCM · PrintNode/WeasyPrint ·
consumer API (`/api/consumer/` — research says MISSING, re-verify) · payments ledger (bKash/SSL
— MISSING?) · delivery order type (MISSING?) · KDS (MISSING?) · loyalty/multi-branch/webhooks
(MISSING?) · float-money/idempotency debt (5,400-line views.py) · sync_service for POS.

### RMS_nextjs_Dashboard
18 routes: orders, POS, menu, modifiers, inventory, staff, offers, promo-code, reports,
new-order builder, table QR, command palette · web order flow end-to-end · auth against Django.

### rms-consumer-app
Browse restaurants · menus · cart · order placement (verify REAL api vs mock) · order tracking ·
PWA install · COD flow (designs/cod-flow.html) · Arabic/RTL (research gap) · search/filters.

### rms-pos-local (Tauri)
PIN login/lock · dine-in/takeaway · discounts · 4 payment methods · kitchen→ready→served→paid
lifecycle · manager-PIN voids · offline order-value cap · ESC/POS printing (TCP 9100) · order
history + reports + Z-report · modifiers picker · menu editor · catalog down-sync · refunds
(absent per research) · auto-update (skeleton) · money-as-integer-paisa integrity.

### chatroom (Go + Next dashboard + Expo mobile + portal + widget)
33 tables parity: inboxes (WhatsApp/Telegram/web-widget/API) · conversations assign/labels/
macros/canned · SLA policies · agent capacity · participants · automation rules (NL-built) ·
campaigns · CSAT · AI RAG agents (pgvector) + usage metering · working hours · audit log ·
push · email digests · embeddable widget · help-center portal :3004 · billing/quota (B137–B142)
· Go route parity vs old Python · CI (research says none) · live channel credentials.

### hotels
Channel manager + PMS: rooms/rates/availability · bookings · channels integration · guest
messaging (chatroom tie) · F&B via RMS tie (research/07-rms-reuse-analysis.md) · backend+frontend
run · Bangladesh-first specifics.

### zealve-web (marketing + platform)
4-product pages (Chatroom, RMS, AdPilot, Forge) · pricing pages (research 07: AED pages) ·
contact/lead flows · EMAIL-SETUP · geoip · ops CI/CD · AdPilot marketing claims vs delivered code.

### rms-pos-local / forge (Rust) — static + compile checks where GUI cannot run in sandbox.

### plate-to-pallet-planner, zealse, Zealve.com, zealve-clinic, rms-app
Identify purpose, run if cheap, assess: maintained? abandoned? starter/clone? debt, secrets,
value-to-portfolio; rate and report.

## 3. Rating rubric (review-kit philosophy: every claim evidence-backed; gates, not vibes)

Dimensions (score /10, evidence REQUIRED for every score):
1. Feature completeness — README/marketing/research claims vs code reality
2. Customer experience — golden path actually completable end-to-end
3. Reliability & correctness — runs clean, error handling, data integrity, tests
4. Security — secrets (gitleaks), deps (trivy), authz scoping, injection
5. Code quality & debt — TODO backlog, hotspots, structure, dead code
6. Docs & onboarding — setup reproducible? deployment documented?
7. Research alignment — GO-NEXT items landed? gaps the research demanded closed?
8. Production readiness — CI/CD, monitoring, billing, backup story

**Rule: ANY dimension below 9/10 MUST be reported with evidence in that product's PRODUCT_REVIEW.md.**
Overall = min(dimensions) is the headline score (weakest-link, review-kit style).

## 4. Report layout (per repo, file PRODUCT_REVIEW.md on main)

1. Verdict box: headline score + table of 8 dimensions
2. What was tested (commands, endpoints, pages; customer-perspective walkthrough)
3. Findings: blocked/broken issues (P0), missing-vs-claims (P1), debt (P2) — each with evidence
4. Below-9 register: every dimension < 9/10 with the exact gap
5. Research map: features from §2 checklist with Present/Partial/Absent
6. Top fixes ranked

# PORTFOLIO-REVIEW — Zealve product portfolio independent review

Date: 2026-09-20 · Method: review-kit 8-dimension rubric (see [`REVIEW-MAPPING.md`](./REVIEW-MAPPING.md)),
every product actually run/tested from customer + product perspective, static scans (gitleaks, trivy),
research-corpus cross-check (zealve-research), live-surface probes. Full evidence per product in each
repo's `PRODUCT_REVIEW.md` on `main`.

**Rule applied: any dimension below 9/10 is registered with evidence in that product's report. Every
product scored below 9 on at least one dimension — hence every report contains a below-9 register.**

## 1. Scoreboard (overall = weakest dimension)

| Product | Repo | Overall | Verdict | Headline issue |
|---|---|---|---|---|
| Consumer app | ZEALVE-LTD/rms-consumer-app | **8.5** | keep | no service worker; inert language switcher; zero tests |
| zealve.com | ZEALVE-LTD/zealve-web | **8.5** | keep | placeholder GA4 id live in prod; no HSTS/CSP; 10 s cold HTML |
| chatroom | ZEALVE-LTD/chatroom | **8.0** | keep | no user provisioning; WS-only realtime (no SSE) while edge blocks WS |
| Owner dashboard | ZEALVE-LTD/RMS_nextjs_Dashboard | **8.0** | keep | 2 CRITICAL + 27 HIGH stale deps; Settings page missing; no tests/CI |
| On-prem POS | ZEALVE-LTD/rms-pos-local | **8.0** | keep | no CI for its 129-test gate; unsigned bundles; cash-sessions partial |
| RMS core | ZEALVE-LTD/rms | **7.0** | keep | P0 tenant→platform-owner escalation; two 500s; float/Decimal mixed |
| Hotels | ZEALVE-LTD/hotels | **6.5** | keep | API fully open (no auth); "certified" adapters mock-verified only |
| Forge | navidRashik/forge | **6.5** | keep (flagship) | deterministic red test (fail-over broken); zero CI; no binaries |
| zealse | ZEALVE-LTD/zealse | **1.0** | park | import crash; all authed endpoints 500; committed Qdrant key |
| Zealve.com (legacy) | ZEALVE-LTD/Zealve.com | **1.0** | archive | /search/ 500; committed MinIO creds; superseded |
| plate-to-pallet | ZEALVE-LTD/plate-to-pallet-planner | **1.0** | archive | in-memory mock; Lovable boilerplate; harvest UI mock |
| zealve-clinic | ZEALVE-LTD/zealve-clinic | **1.0** | archive | senaite fork w/ 1-line delta; committed 50 MB production DB backup |
| rms-app (RN) | ZEALVE-LTD/rms-app | **1.0** | archive | abandoned starter; hard-coded bearer token in source |

## 2. Security register (act this week)

1. **rms-app `services/foodApi.js` — hard-coded Knox bearer token + plaintext HTTP to raw IP. Revoke the token now** (then archive repo).
2. **zealse `.roo/mcp.json` — live Qdrant Cloud API key committed. Revoke now.** Also: OAuth callback mints JWT for any code; hard-coded JWT `SECRET_KEY`.
3. **zealve-clinic `db_backups/` — 50 MB ZODB `Data.fs` production snapshot in git. Purge from history** (BFG) + rotate anything inside.
4. **Zealve.com `example.env` — MinIO/S3 credentials committed.** Rotate.
5. **rms P0 (D-15, live on main): any restaurant owner can mint platform-level owners** via `POST /api/account_management/restaurant/create_owner/`. Patch + review audit trail.
6. **hotels: API completely open** (token optional, no user model). Block public exposure until auth lands.
7. **GitHub Dependabot on rms default branch: 111 vulnerabilities (2 critical, 26 high)**; dashboard: form-data CVE-2025-7783 CRITICAL, axios 1.9.0 ×13, xlsx proto-pollution; chatroom: 2 HIGH postgres CVEs; Zealve.com: 1 CRITICAL + 37 HIGH.
8. **zealve.com prod: `G-TEST12345` placeholder GA4 id in gtag (analytics void), no HSTS, CSP = `upgrade-insecure-requests` only, unthrottled `/api/admin/login`.**

## 3. Reliability findings from actually running the products

- rms: 141/152 tests pass (1 flaky CI-gating inventory-ledger test, 10 xfail); `daily_report` 500 (`float += Decimal`), `food_list/{cat}` 500 without param, takeaway blocked for tenants by `IsAdminUser`. Consumer API is REAL end-to-end (OTP→token→order→idempotent replay→DELIVERY) — **research's "consumer app 100% mock" claim is now outdated**.
- chatroom: Go build/vet/tests all green (145 test funcs, 183 routes parity verified); ~40 endpoint groups exercised 200/201/204; dashboard login verified in headless browser. Gaps: no signup/invite/reset, WS-only realtime with no SSE fallback (mobile has no poll fallback at all), portal-category 400, knowledge-alias 404, digest has no SMTP transport.
- hotels: Go build clean, 24 tests green; golden path incl. oversell→409, idempotency replay, 2-way OTA e2e vs mock booking.com, bed-bank settle round-trip. Gaps: open API, no CI, adapters mock-verified only.
- forge: cargo tests executed (ACP 16/16, PTY 4/4, core 76/77 — the 1 red is the fail-over bug); daemon 60+ routes; but no binaries/CI, onboarding = compile 8 crates, README describes a retired UI.
- consumer app golden path PASS in browser (menu→cart ৳557 w/ 5% VAT→login gate→OTP→order ZV-35176→history).
- zealve.com live: 15/15 routes OK, lead-capture validation verified without creating leads, TLS 1.3, sitemap + llms.txt + MCP server present.

## 4. Live-surface probes (from the review environment)

| Surface | Result |
|---|---|
| https://zealve.com | **200 OK** (0.35–0.43 s warm; ~10 s cold HTML) |
| https://slateblue-ram-764267.hostingersite.com (RMS backend) | **UNREACHABLE from review env** — TLS ok then connection reset / timeout on every path (HTTP/1.1 and H2) |
| https://midnightblue-dunlin-112756.hostingersite.com (chatroom backend) | **UNREACHABLE from review env** — same signature |
| Hostinger REST API (developers.hostinger.com) | Token authenticates; vhost-scoped routes not found (VPS-only API surface) |
| SSH 147.93.17.40:65002 | Blocked from review sandbox egress — could not confirm server state |

zealve.com sits on the same hcdn edge and responds, so this is not a generic egress failure.
**Action: confirm from another network whether the two app backends are actually serving; if down, restart via hPanel.**

## 5. Research ↔ product map result (per REVIEW-MAPPING §2)

- GO-NEXT landed since the Sep-12 audit: real consumer API ✅, Go route parity ✅ (chatroom), CI exists in chatroom/rms (research said none — now outdated), pricing honesty on zealve.com ✅ (quote-based AED), AdPilot honestly labeled design-partner stage ✅.
- Still missing across portfolio (matches research DON'T-GO-NEXT/LATER): online payment gateways (bKash/SSL/Nagad adapters), delivery order type + fees, KDS, loyalty, multi-branch, outbound webhooks, NBR VAT invoicing, Arabic/RTL shipping, SSE fallback for chatroom, hotels booking engine (direct bookings total 0).
- Convergence warning (research file 14) confirmed in practice: chatroom + rms both hand-rolled rules engines/approvals/metering — ratify one platform core before AdPilot work starts.

## 6. Recommended order of work (portfolio view)

1. Security week: revoke 2 keys + rms-app token, purge clinic DB backup, patch rms create_owner P0, auth for hotels API.
2. Ship-blockers on keepers: rms two 500s + takeaway permission + Decimal completion; chatroom SSE fallback + user provisioning; dashboard dep upgrades.
3. CI everywhere: rms-pos-local Linux job, hotels CI, forge CI + first release binaries.
4. Archive/park: rms-app, Zealve.com, plate-to-pallet (harvest UI), zealve-clinic, zealse backend/frontend (keep website+SRS).
5. Then: research file 14 platform-core ratification, payments ledger, Meta Oct-1 metering readiness.

---
*Generated by the Zealve review sprint (review-kit installed & used as the rating framework; graphify graph of review-kit: 6,525 nodes / 15,434 edges). Per-product evidence: `PRODUCT_REVIEW.md` in each repo's `main`.*

# Design-gap audit — 2026-10-31 addendum (roadmap#1)

**Scope.** Docs-only addendum to [`design-gap-audit-2026-10-04.md`](./design-gap-audit-2026-10-04.md) for issue #1 — the owner decision gate. It (1) restates the **two decision queues side by side** — the 2026-10-03 discovery comment's 9-item draft task list × the 2026-10-04 audit's §7 five-item queue; (2) records **status corrections with fresh evidence** (default branches + merged-PR records read via API on 2026-10-31); (3) adds the **multi-unit B2B care design pack** (delivered 2026-10-07, issue #1 comment 4) as a new decision item; and (4) appends a clearly-labeled **recommended disposition (non-binding)** column per item to speed the owner's tick pass.

> **Nothing was decided here.** No form was ticked and no decision was made on the owner's behalf. Every KEEP / DROP / PARK / CLOSE below is analysis to react to, not action taken. The two unchecked status boxes in issue #1 — *"Owner decisions received"* and *"Task list compiled"* — remain the owner's to tick. Docs only: no code, no form ticks, no board writes.

## 1. The two decision queues, side by side

The 2026-10-03 discovery report (issue #1 comment 1, `5970549737`) inventoried the ~59 OpenDesign (`.od`) projects and produced a **9-item draft task list**. The 2026-10-04 in-repo audit (PR #2) inventoried the research-repo design tree and produced a **5-item §7 decision queue**. They overlap on three items only; each contains items the other missed.

| Draft list # (comment 1, 2026-10-03) | Item | Audit §7 # (2026-10-04) | Overlap notes |
|---|---|---|---|
| 1 | hotels: build 8 missing modules (or descope) | — | OD `.od` designs; outside the audit's research-repo scope |
| 2 | zealse: Revora agent-platform revamp (7 designs) | — | same |
| 3 | zfood: does the product exist? (11+1 screens, no repo) | — | same |
| 4 | chatroom: B294 voice calling | — | same |
| 5 | adpilot: adopt v4 calm-studio round surfaces (10 rounds) | §7.3 + §7.5 | §7 covers the in-repo design subset (canvas / compile-review / runlog / digest + onboarding / ops-home fidelity); draft #5 is the OD v4-rounds superset |
| 6 | chatroom dashboard: copilot states machine | — | |
| 7 | zealve-ecommerce: theme system's first theme from the 16 designs | — | |
| 8 | suite-convergence console: keep/drop | §7.2 | same gap, two design sources (OD `zealve-suite-convergence-v1` + research-repo `designs/convergence/`) |
| 9 | zealve-web: CMS decision (form A) | §6 carry-over | |
| — | reseller / white-label (GOAL3 #8, `designs/reseller.html`) | §7.1 | root-set mockup; never made the draft list |
| — | tools-console dedicated screens | §7.4 | |
| NEW (2026-10-07, comment 4) | multi-unit B2B care (zealse-connect) | — | research #36 + design pack #37; no backend |

## 2. Consolidated decision queue — status 2026-10-31 + non-binding recommendations

Statuses re-read from default branches and merged-PR records on 2026-10-31 unless marked *not re-verified*. **The last column is a recommendation only — the owner decides.**

| # | Item (sources) | Status 2026-10-31 | Evidence | **Recommended disposition (non-binding)** |
|---|---|---|---|---|
| 1 | **Convergence control plane** — agents / approvals / growth-loop / wallet (draft #8 × §7.2; `designs/convergence/`) | **PARTIAL** — corrected from UNIMPLEMENTED on 2026-10-04, unchanged since | Owner decision **Q6** (issue #1 comment 3); adpilot-ai PR **#6** "T-051: convergence control plane slice 1 — Zealve Suite shell + wallet read path" merged 2026-10-04T20:23Z (`4f12a61`); `/suite` routes exist for hub + wallet + approvals + agents + growth-loop. Slice cards: chatroom **#196 / #197 / #198 closed** (slices 4, 6, 7-chatroom), adpilot-ai **#7–#11 open** (slices 2, 3, 5, 7-adpilot, 8) | **KEEP — already owner-decided (Q6) and in flight.** No new KEEP/DROP needed beyond confirming slices 2–8 continue; remaining work = the adpilot halves (#7–#11). The overlapping OD pack `zealve-suite-convergence-v1` (5 screens) should be PARKed as reference-only so one build source of truth remains (`designs/convergence/` + the slice plan) |
| 2 | **Reseller / white-label** instance switcher + flags-per-plan (§7.1; `designs/reseller.html`) | UNIMPLEMENTED — confirmed | Zero `reseller` hits in the chatroom tree, re-grepped 2026-10-31 (2026-10-04 audit found the same) | **PARK** — no code and no demand signal since 2026-10-04; revisit when a partner/reseller motion actually exists (or DROP if that motion is dead) |
| 3 | **adpilot canvas / compile-review / runlog / digest** (draft #5 subset × §7.3; designs 6–9) | UNIMPLEMENTED — confirmed | No web-next routes for any of the four (route list read 2026-10-31); design HTML only in `.lavish/` + `public/designs/` | **KEEP** as the calm-studio core loop, sequenced canvas → compile-review → runlog → digest (digest last — it needs a distribution loop); owner may split and PARK digest alone |
| 4 | **tools-console dedicated screens** — tools-registry table, tool-detail, register-tool wizard, invocation-log (§7.4) | PARTIAL — unchanged | Registry backend + settings card shipped (`backend-go/internal/api/tools.go`, `dashboard/src/components/settings/tools-card.js`); zero invocation-log / register-tool / tools-console screen paths in the chatroom tree, re-grepped 2026-10-31 | **KEEP** — completes an already-shipped registry; smallest of the console gaps |
| 5 | **adpilot onboarding / ops-home fidelity** (draft #5 subset × §7.5) | PARTIAL — not re-verified in depth | 2026-10-04 audit: `OnboardingChecklist.tsx` only; root page serves as home, no ops-home route. 2026-10-31 route list unchanged (no ops-home route) | **KEEP** — cheap fidelity upgrades to existing routes |
| 6 | **hotels 8 missing modules** — 06-catalog, 07-guest-inbox, 10-housekeeping, 15-bb-distribution, 17-grn, 18-stock-ledger, 19-booking-engine, 20-integrations (draft #1) | PARTIAL — 6 of 8 still have no code paths | Hotels tree 2026-10-31: code modules = bedbank (contracts/settlement), calendar, channels, folio, frontdesk, reservations, properties, hotelops, adapters (agoda/booking.com/expedia/mockota). No paths matching catalog / guest-inbox / housekeeping / GRN / stock-ledger / booking-engine. 15-bb-distribution and 20-integrations may partially overlap existing bed-bank + adapters/channels code under different names (fidelity vs designs unverified) | **KEEP** — biggest single product gap; owner may descope per module (e.g. build booking-engine + housekeeping first, park GRN/stock-ledger until F&B volume exists) |
| 7 | **zealse Revora agent-platform revamp** (7 OD designs; draft #2) | NOT STARTED | 0 matching routes (2026-10-03 comment); PORTFOLIO-REVIEW 2026-09-20 scored zealse **1.0 / park** (import crash, authed endpoints 500, committed Qdrant key) | **PARK** — revamp not started and the base product is in park state; revisit after the ERP direction settles (zealveone is the active build — see §3.5) |
| 8 | **zfood desktop** (11+1 OD screens; draft #3) | NO REPO EXISTS — confirmed | Org repo list read 2026-10-31 (28 repos): no zfood repo | **DROP** — no code home and no product motion; archive the OD project (PARK instead if the food-delivery idea is still alive) |
| 9 | **chatroom B294 voice calling** (draft #4) | **IMPLEMENTED — correction** | chatroom PR **#133** "B294: one-to-one voice calling — call card, WebRTC agent console, tenant policy, call ledger (owner-gated)" merged 2026-09-29T05:39Z; commits `feat(voice)` B294-1 backend core + B294-2 widget (2026-09-28) + security/code-review fixes; tree 2026-10-31 carries `backend-go/internal/api/{calls,call_policy}.go`, `ws_call_test.go`, dashboard `/calls` page, call-card/panel/ringer + call-policy-card components, `scripts/voice-call-e2e.mjs`, ops runbooks, tech-specs B294-1/2/3 | **CLOSE — no decision needed.** The 2026-10-03 draft's "code never started" is outdated (see §3.2 for the discrepancy); drop the item from the queue as done. Optionally verify the owner-gated production enablement separately |
| 10 | **chatroom dashboard copilot states machine** — wire designed states into `copilot-panel.js` (draft #6; CHAT-107) | OPEN — not re-verified | Tree 2026-10-31: `dashboard/src/components/inbox/copilot-panel.js` + `design/copilot/inbox-copilot-states.html` + `docs/tickets/CHAT-107-copilot.md` all present; no memory-bank completion record for CHAT-107 seen | **KEEP** — small wiring job, designs already in-repo; confirm CHAT-107's current scope before ticketing |
| 11 | **zealve-ecommerce theme bridge** — first theme from the completed designs (draft #7) | **PARTIAL — progressed since 2026-10-03** | Tree 2026-10-31: theme engine exists (`backend-go/internal/theme/{lexer,render,theme}.go` + tests) and a full Shopify-style theme `themes/atelier-bold` (layout/`theme.zeal`, sections, config, locales, templates); 18 designed v1 themes at `designs/od/theme-designs/`. Storefront still renders the host-level design — `storefront/app/page.jsx`: "The theme system will own presentation (sections); this is the host-level design until the renderer lands (NT-24)" | **KEEP** — the bridge is half-built: finish the renderer landing (NT-24) and port one of the 18 designed v1 themes as the first real theme |
| 12 | **CMS decision (form A)** — zealve-web and org-wide (draft #9 × audit §6) | UNCHANGED — org-wide NO-CMS | 2026-10-03 CMS table (12 repos audited) + 2026-10-04 audit §6: zero CMS dependencies anywhere; content lives as repo files; only homegrown admin surfaces | **Tick form A option 2: "No — keep files-as-content"**; revisit only if marketing content volume actually grows |
| 13 | **NEW — multi-unit B2B care (zealse-connect)** (issue #1 comment 4, 2026-10-07) | DESIGN-READY, **NO BACKEND** | research **#36** merged 2026-10-07 (`research/multi-unit-b2b-care-2026-10-05.md`, 189 lines): recommendation **(d) hybrid** + **§7 six owner decision points**; design pack research **#37** merged 2026-10-07 (`da7f5a5`): `designs/multiunit-care/` — 5 Onyx screens across 4 HTML files (index: cover + unit switcher + unit-scoped inbox + parent units console; routing editor with dry-run; 6-step onboarding wizard; unit settings). OD project `zealse-connect-multiunit-care-64af`; the OD autonomous leg failed (host-CLI model resolution) so artifacts were driven directly | **KEEP FOR DECISION** — a new form-B-style item: answer the six points in research #36 §7 (see §4 below) before any backend card is cut. Nothing is implemented |

## 3. Status corrections since the queues were written (evidence)

### 3.1 Convergence control plane: UNIMPLEMENTED → PARTIAL
Owner decision **Q6** happened out-of-band (issue #1 comment 3, 2026-10-04T20:29Z). adpilot-ai **#6** (slice 1: `/suite` shell + hub + wallet read path, squash `4f12a61`) merged 2026-10-04T20:23Z — the comment labels the receipt "2026-10-05". Slice detail as of 2026-10-31: chatroom halves done (**#196** cross-product agents read API, **#197** unified approvals join, **#198** campaign-attribution stamps — all closed); adpilot halves pending (**#7** suite approvals, **#8** wallet write + 402, **#9** agents screen, **#10** growth loop, **#11** hub completion — all open). Caveat: the `/suite/approvals|agents|growth-loop` route files were not content-diffed; "slice-1 stubs" is inferred from the open slice cards.

### 3.2 B294 voice calling: "code never started" → IMPLEMENTED on main
The 2026-10-03 draft list claimed "designs done, code never started; spawn sessions died 09-29". But chatroom PR **#133** merged 2026-09-29T05:39Z — *before* that comment was posted — and main today carries the full stack (backend calls + policy + WS tests, dashboard calls page, call-card/panel/ringer, e2e script, runbooks, three memory-bank feature records, plus a 2026-10-08 B309 follow-up). The 10-03 claim appears to describe the failed spawn-session *launch*, not the merged code. Flagged as a discrepancy for the owner; either way the queue item is done.

### 3.3 Ecommerce theme bridge: designs-only → engine + first theme exist, consumption pending
`backend-go/internal/theme/` (lexer/render/theme + tests) and `themes/atelier-bold` (a complete `.zeal`-template theme) now exist on main; the designed packs live at `designs/od/theme-designs/` (18 v1 themes + contact sheet — the 10-03 comment counted 16). The storefront still renders host-level markup pending the renderer landing (NT-24), so the designs→product bridge is half-built, not unbuilt.

### 3.4 Hotels: 6 of the 8 designed modules still missing; 2 possibly covered under other names
No code paths match catalog, guest-inbox, housekeeping, GRN, stock-ledger, or booking-engine (tree read 2026-10-31). Bed-bank (contracts/settlement) and channel adapters/channels pages may partially cover the 15-bb-distribution and 20-integrations designs — fidelity unverified.

### 3.5 Shipped meanwhile, outside both queues: zealveone lot/serial
Not part of either decision queue (zealveone appears nowhere in issue #1 or the 2026-10-04 audit), but recorded for completeness since it closes a known inventory gap: zealveone PR **#216** "inventory: lot/serial tracking — stock.lot, move-level lots, traceability (#209)" merged 2026-10-30T21:17:47Z. zealveone has been very active through late October (accounting, MRP, CRM, portal, e-invoicing — 50 PRs visible), which is context for the zealse/Revora PARK recommendation in §2 row 7.

## 4. New decision item — multi-unit B2B care (comment 4, 2026-10-07)

**Research #36** (`research/multi-unit-b2b-care-2026-10-05.md`, merged 2026-10-07): how 10-unit FMCG groups (Unilever/Reckitt/Nestlé patterns) should be served in one chat product. Recommendation: **(d) hybrid** — one parent workspace, unit sub-workspaces, per-unit inboxes + brand chips + unit-scoped agents, per-unit portal subdomains sharing one backend account, one parent console for leadership KPIs, routing whose first clause is always "portal origin pins the unit". Its **§7 owner decision points** (all six gate any backend work):

1. Approve the (d) hybrid model and the phase order (portal-first vs units-first).
2. Units ↔ inboxes cardinality at launch (strict 1:1 vs `units` table from day one).
3. Portals: wildcard subdomains (DNS + wildcard cert on the Hostinger deploy) vs path-per-unit first.
4. Parent-console audience: leadership KPIs only vs cross-unit agent supervision.
5. Identity policy: auto-link contacts across units by phone/email vs manual merge.
6. Pricing: per-unit seats vs parent-pooled vs per-conversation (+ whether the parent wallet cap subsumes unit caps).

**Design pack research #37** (merged 2026-10-07, `da7f5a5`): `designs/multiunit-care/` — five Onyx-v1 screens (unit switcher + unit-scoped inbox + parent units console in `index.html`; routing-rule editor with dry-run; 6-step onboarding wizard; unit settings), Havana Consumer Group sample data, OD project `zealse-connect-multiunit-care-64af`. Provenance note: the commissioned OD autonomous run failed (host-CLI model resolution, same failure class as the doc-25 run); artifacts were driven directly into the OD project and mirrored. **No backend implemented — the six decision points gate it.**

## 5. Form notes (for the owner's tick pass — nothing ticked here)

- **Form A (CMS):** unchanged since 2026-10-03 — org-wide NO-CMS. Non-binding recommendation: option 2 ("No — keep files-as-content"), revisit on content-volume growth.
- **Form B (per-design KEEP/DROP/PARK):** the consolidated queue in §2 is the per-item surface; the recommendation column is there to speed the pass, not to pre-fill it.
- **Form C (task-list destination):** Boards **#5/#6 are currently unreachable by the automation token** — verified 2026-10-31: token scopes are `gist, read:org, repo, workflow` (no `read:project`); a GraphQL `projectsV2` query is rejected with `INSUFFICIENT_SCOPES`, and the classic projects REST endpoint 404s for this repo. **Option 3 (keep the list in this issue) is the only automatable destination today**; moving cards to Boards #5/#6 needs either a token scope change (add `read:project` / `write:project`) or manual action by the owner.

## 6. Evidence, method, and honest caveats

- Read-only: GitHub REST API reads of default-branch git trees, merged-PR records, and issue #1's four comments; no product repo was modified, no board written, no form ticked.
- **Not verified / caveats:**
  - adpilot `/suite/approvals|agents|growth-loop` page contents not diffed — stub status inferred from open slice cards adpilot-ai #7–#11 (the chatroom counterparts are closed).
  - Pixel-level fidelity was never diffed anywhere (carried over from the 2026-10-04 audit's caveat).
  - Hotels 15-bb-distribution / 20-integrations overlap with bed-bank/adapters code unverified.
  - Copilot states machine (CHAT-107) wiring not verified — design + panel + ticket all present, no completion record found.
  - adpilot onboarding/ops-home fidelity not re-verified beyond the unchanged route list.
  - The 2026-10-03 B294 "code never started" claim conflicts with PR #133's 2026-09-29 merge date (§3.2); recorded as found.
  - The 2026-10-07 comment says "5-screen pack"; the pack is 5 screens across 4 HTML files + README — screens and files are not 1:1.
- All timestamps UTC, from API records (merged-at, comment created-at), not comment prose.

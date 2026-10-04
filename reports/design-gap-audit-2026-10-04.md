# Design-gap audit — 2026-10-04 (roadmap#1)

**Scope.** Inventories the design assets that live in `ZEALVE-LTD/zealve-research/designs/` (+ `zealve-research/adpilot/designs/`) and cross-references each against product-repo code. Complements the 2026-10-03 discovery comment on issue #1, which inventoried the ~59 OpenDesign (`.od`) projects; this file covers the in-repo design tree so the audit persists in-repo. Statuses: **IMPLEMENTED / PARTIAL / UNIMPLEMENTED / OBSOLETE**, each with one line of evidence (file path or PR number), read from default branches on 2026-10-04.

## 1. `designs/` root — GOAL3 reference-platform mockups (B163 · target: chatroom dashboard / Connect console)

Eight static HTML mockups drawn from the reference-platform study (B161 deepdive → B162 gap mapping → B163 designs-first). **7 of 8 shipped.**

| # | Design asset | Status | Evidence |
|---|---|---|---|
| 1 | `flags.html` — Settings→Flags | IMPLEMENTED | chatroom PR #14 (B211 flags primitive + Settings admin card); `backend-go/internal/api/flags.go`, `dashboard/src/components/settings/flags-card.js` |
| 2 | `tools.html` — Settings→Tools registry | IMPLEMENTED | `backend-go/internal/api/tools.go`, `dashboard/src/components/settings/tools-card.js`, `docs/tech-spec/CHAT-TOOLS-1.md`; consumed by PR #29 (rule actions + macros dispatch through the registry) |
| 3 | `action-card.html` — policy-bound agent action in-thread | IMPLEMENTED | chatroom PRs #28 (CHAT-105 policy-fenced approvals + approvals queue), #33 (B221 in-thread action card); `backend-go/internal/api/approvals.go`, `dashboard/src/components/inbox/thread-approval-card.js` |
| 4 | `workflows.html` — Automation→Workflows | IMPLEMENTED (shipped beyond the design) | PRs #30 (B220 multi-step flows over the registry), #54 (B236 wait node), #55 (B237 templates), #63 (B249 agentic NL compiler); `backend-go/internal/api/workflows.go`, `workflows_compile.go`, `dashboard/src/components/automation/workflows-panel.js` |
| 5 | `usage-limits.html` — Settings→Usage | IMPLEMENTED | PR #32 (B225 tool-execution limits: hard cap + live meter); `dashboard/src/components/billing/limits-card.js`, `backend-go/internal/api/agent_tools.go` |
| 6 | `cod-flow.html` — GCC COD delivery stepper + OTP | IMPLEMENTED | PRs #5 (B145 WhatsApp COD verification + funnel metrics), #31 (B222 in-thread delivery stepper); `backend-go/internal/api/cod.go`, `cod_stepper.go`, `dashboard/src/components/inbox/cod-stepper.js` |
| 7 | `commerce-loop.html` — in-chat menu→cart→payment→receipt | IMPLEMENTED | PRs #65 (B250 revora commerce tools + catalog sync), #70 (B253 widget storefront: product cards, cart proposals, order tracking); `backend-go/internal/commerce/{cart,catalog,orders,platforms,commerce}.go` |
| 8 | `reseller.html` — white-label instance switcher + flags-per-plan | UNIMPLEMENTED | zero `reseller` hits in the chatroom file tree or merged-PR subjects (grep 2026-10-04) |

## 2. `designs/tools-console/` — "Settings · Tools — Zealve Connect console" (5 screens + assets)

**PARTIAL.** The registry backend and a settings card shipped, but the console's dedicated screens — tools-registry table page, tool-detail, register-tool wizard, invocation-log — have no dashboard routes; the chatroom tree has no invocation-log component.
Evidence: `dashboard/src/components/settings/tools-card.js` (the only shipped surface); screens designed in `designs/tools-console/{tools-registry,tool-detail,register-tool,invocation-log}.html`.

## 3. `designs/connections/` — "Connections · Settings — Zealve Chatroom" (connect-drawer)

**IMPLEMENTED** (as a settings card; full-drawer fidelity unverified).
Evidence: chatroom PR #26 "implement the missing connections seam (QA-2)"; `backend-go/internal/api/connections.go`, `dashboard/src/components/settings/connections-card.js`, `docs/tickets/QA-2-settings-connections-seam.md`.

## 4. `designs/convergence/` — "Zealve Suite — convergence control plane" (agents, approvals, growth-loop, wallet)

**UNIMPLEMENTED.** Both candidate targets carry the convergence work as docs only — chatroom `docs/research/adpilot-convergence-v2..v8-2026-10.md`, adpilot-ai `docs/44-cross-product-convergence.md` … `52-agent-chat-convergence-v8.md` — with no control-plane code: no wallet or growth-loop files exist in either repo (grep 2026-10-04).

## 5. `adpilot/designs/` — 10 adpilot mockups (target: adpilot-ai web-next)

Vendored into the product for reference at `apps/web-next/public/designs/`; **4 of 10 have shipped surfaces** (route-exists evidence; pixel fidelity not diffed).

| Design | Status | Evidence |
|---|---|---|
| `adpilot-design-1-templates.html` | PARTIAL | `apps/web-next/app/templates/page.tsx` shipped |
| `adpilot-design-2-onboarding.html` | PARTIAL | `apps/web-next/components/OnboardingChecklist.tsx` only |
| `adpilot-design-3-ops-home.html` | PARTIAL | root `apps/web-next/app/page.tsx` serves as home; no ops-home route as designed (`v5-ops-home.html` remains design-only in `.lavish/`) |
| `adpilot-design-4-reconsidered.html` | OBSOLETE | explicit design-pivot doc; superseded by rounds 5–10 |
| `adpilot-design-5-creative-ops.html` | PARTIAL | `apps/web-next/app/creative-ops/page.tsx` shipped |
| `adpilot-design-6-canvas-v2.html` | UNIMPLEMENTED | no canvas route; `v5-canvas.html` design-only (`.lavish/`) |
| `adpilot-design-7-compile-review-v2.html` | UNIMPLEMENTED | no compile-review route |
| `adpilot-design-8-runlog-v2.html` | UNIMPLEMENTED | no runlog route; `v5-runlog.html` design-only |
| `adpilot-design-9-digest.html` | UNIMPLEMENTED | no digest route |
| `adpilot-design-10-human-review.html` | PARTIAL | `apps/web-next/app/approvals/page.tsx` + `app/approvals-card.tsx` cover the human-review flow |

## 6. CMS status (form A carry-over)

Unchanged from the 2026-10-03 comment: **no CMS anywhere** — zero CMS dependencies org-wide; content lives as repo files (e.g. `adpilot-ai/apps/web-next/content/`), with homegrown admin surfaces (chatroom internal hub) as the only editing UIs.

## 7. Open gaps → decision queue (feeds form B)

1. GOAL3 #8 **reseller / white-label** — the only root-set mockup with no code at all
2. **convergence control plane** (agents / approvals / growth-loop / wallet) — largest unbuilt design group
3. **adpilot canvas / compile-review / runlog / digest** — four designed surfaces without routes
4. **tools-console dedicated screens** (invocation log, register-tool wizard)
5. **adpilot onboarding / ops-home fidelity** vs the designed screens

## Method

- Design inventory: `gh api repos/ZEALVE-LTD/zealve-research/git/trees/HEAD?recursive=1` (28 files under `designs/`; 10 under `adpilot/designs/`); HTML `<title>`/intro text read for intended targets.
- Product truth: git trees of the chatroom and adpilot-ai default branches, merged-PR subjects (`gh pr list --state merged`), `docs/tech-spec/` + memory-bank feature records. Read-only — no product repo was modified.
- Fidelity caveat: "IMPLEMENTED" means a shipped surface matching the designed feature; pixel-level fidelity was not diffed against the mockups.

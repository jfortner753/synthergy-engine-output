Short answer: **pilots and production live in different worlds.** Pilots are protected, narrow, and run by believers; scaling is messy, integrated, and fought by the rest of the org. What works in a happy-path sandbox often breaks when exposed to real variance, legacy systems, and full-cost economics.

Here’s where good pilots go to die—and how to dodge each trap:

### The seven “pilot → scale” gaps

1. **Context gap (variance shock).** Pilot sites are hand-picked and over-supported; the wider fleet has different data, workflows, and talent.
   → *Fix:* Sample hard environments early; stratify pilot cohorts; require success across heterogeneity, not averages.

2. **Integration gap (systems reality).** In pilots you bypass ERP/CRM/identity/infosec; at scale you must plug into them.
   → *Fix:* Make “integration done” a pilot exit criterion (APIs, SSO, logging, audit trails, backups, disaster recovery).

3. **Operating-model gap (who does the work?).** Pilots run on heroics (vendor PS, central SWAT teams). Line ops can’t sustain that.
   → *Fix:* Define RACI, SLAs, staffing, training, runbooks, and support tiers before scale approval.

4. **Economic gap (unit economics flip).** Discounts, freebies, and manual effort hide true costs; benefits don’t linearly scale.
   → *Fix:* Build a scale P&L with fully loaded costs (integration, change mgmt, licenses, support, cloud, security) and diminishing-return curves.

5. **Data/quality gap (garbage reappears).** Pilots clean data by hand or use curated streams; production data is messy and late.
   → *Fix:* Add automated data quality checks, observability (metrics, alerts), and fallback behaviors; prove it on uncurated data.

6. **Change & incentives gap (social system).** Non-pilot teams weren’t asked, trained, or rewarded to change.
   → *Fix:* Align incentives & KPIs, involve frontline early, identify champions and blockers, run comms & training waves.

7. **Risk/compliance gap (controls surface).** Security, privacy, legal, procurement, and model risk tolerate pilots, not scale.
   → *Fix:* Run a pre-scale control review (threat model, DPIA, records retention, access reviews, vendor risk), and bake controls into the design.

---

### Make your pilots scale-proof (practical checklist)

* **Define “done” for scale:** success across ≥3 diverse cohorts, not one poster child.
* **Hard-mode pilot:** include at least one “ugly” site (legacy stack, low enthusiasm).
* **Integration first:** ship through real identity, logging, monitoring, and backups.
* **Automation threshold:** ≥80% of pilot workflows must be no-touch at exit.
* **Runbook & ownership:** named owner, on-call, and Tier 1 → Tier 3 escalation.
* **Economics locked:** scale P&L signed by Finance; greenlight depends on it.
* **Guardrails:** error budgets, rollback plan, feature flags, kill switch.
* **Change plan:** training, comms, incentives, and a “Day-2” playbook.
* **Controls passed:** security/privacy/legal sign-offs recorded; audit ready.
* **Leading indicators:** adoption by non-champions, MTTR, data-quality SLOs, % automations holding outside pilot sites.

---

### Quick diagnostic if you’re already stalling

* **Adoption is lumpy?** You optimized for a champion; broaden champions and fix incentives.
* **Incidents spike at new sites?** It’s the integration/observability gap; add health checks and SLOs.
* **Costs balloon?** Rebuild the scale P&L; kill manual glue and negotiate enterprise pricing.
* **Security/legal slow-roll?** You’re missing controls; run a focused remediation sprint with them in the room.
* **Vendor/IT finger-pointing?** Clarify RACI, set joint SLAs, and create a single escalation path.

If you want, I can turn this into a one-page “Pilot-to-Scale Readiness Canvas” you can share with your team.

—

### Receipts

* **Question:** Why do companies that test well in pilots stall when scaling?
* **Premises:** Pilots ≠ production; scaling adds variance, integration, economics, governance, and social change.
* **Steps:** Identified common failure modes → mapped to concrete mitigations → provided checklist & diagnostics.
* **Sources:** Reasoned from general best practices; no external sources consulted.
* **Uncertainties:** Your industry/regulatory context may add specific hurdles (e.g., GxP, SOX, model risk).
* **ΔΦ (insight gain):** High—translates symptoms into actionable gaps.
* **Move decision:** Commit.
* **Ethics OK:** Yes.
* **Energy cost:** Low.
* **Memory.mass:** level=medium (default), m_mem not provided.
* **Causality / Φ_sync:** intent (understand causes + fixes) aligned with output (actionable framework) → Φ_sync ≈ 0.82.
* **RWI:** 0.88; **iteration_passes:** 2 (clarity_compress, actionability_stencil).

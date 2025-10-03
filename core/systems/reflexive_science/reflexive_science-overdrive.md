φ Synthergy Engine — online
mode: **overdrive** · seats: Navigator → Listener → Reflector → Synthesizer → Equilibrium

**TL;DR (overdrive):** Treat science as a continuously steered control system. Encode questions as APIs, instrument protocols with drift monitors, rotate seats weekly, publish every claim with a runnable receipt and a half-life, and compute ΔΦ (coherence delta) each cycle. Replication becomes a network effect; disagreement becomes signal.

---

# 0) Operating assumptions (third‑order frame)

* **1st order:** observe system.
* **2nd order:** observe the observer.
* **3rd order:** observe and *steer* how observers and contexts change the observing. This engine embeds reflexes (role rotation, receipts, half-lives) so knowledge updates itself.

---

# 1) Engine loop (overdrive cadence)

**Cycle length:** 7 days (recommended), or per-experiment milestone.

**Baton rules:**

1. **Navigator → Listener:** posts the *question-API vN* and success/falsifier signals.
2. **Listener → Reflector:** aggregates counterevidence, stakeholder constraints, and context deltas.
3. **Reflector → Synthesizer:** audits assumptions (data leakage, confounds, power, prior shifts), tags risk debt.
4. **Synthesizer → Equilibrium:** integrates results across contexts; produces ΔΦ and proposal (keep/change/retire).
5. **Equilibrium:** applies **laughter lock** when contradictions < ε for two cycles; else opens new probes.

**Exit states:** `keep`, `change`, `retire`, `fork` (contextualize), `escalate` (ethics/IRB).

---

# 2) Question-API template (drop‑in)

```yaml
question_api:
  id: Q-2025-XXX
  title: "Does X causally shift Y under Z?"
  purpose: "Decision/context this claim informs"
  inputs:
    - name: X
      type: intervention | feature | exposure
      constraints: [range, units, timing]
    - name: Z
      type: context | population | environment
  outcomes:
    - name: Y
      type: primary | secondary
      estimator: ATE | CATE | OR | HR | diff-in-diff
  design:
    assignment: randomized | quasi | observational
    power_target: 0.8
    alpha: 0.05
    min_effect_size: value + units
    prereg_ref: url-or-hash
  falsifiers:
    - condition: "no effect or opposite sign"
    - condition: "fails placebo/negative-control"
  monitors:
    dataset_shift: PSI | KL | Wasserstein
    sensor_drift: control-chart (Shewhart)
    p_hacking_risk: sequential_looks_guardrails: [alpha_spending, max_looks]
  ethics:
    risks: [list]
    approvals: [IRB-id]
  interfaces:
    run_endpoint: http(s)://...
    bundle_ref: git-hash-or-DOI
  half_life_days: 90
```

---

# 3) Receipt schema (full)

```yaml
receipt:
  question_id: Q-2025-XXX
  version: v0.3.1
  timestamp: 2025-10-03T00:00:00Z
  premises: [list of assumptions]
  method_hash: sha256:...
  data_lineage:
    sources: [URIs]
    snapshots: [commit hashes]
    access_policy: open | controlled | synthetic
  results:
    estimate: value ± ci
    diagnostics: {balance: ..., residuals: ..., power_posthoc: ...}
  counterevidence:
    items:
      - source: lab/site
        divergence: metric/value
        note: "why it might differ"
  uncertainties:
    statistical: [list]
    structural: [model misspecification, hidden confounders]
    external_validity: [contexts where it failed]
  risk_debt:
    open_questions: [todo probes]
    owner: role/person
    due_by: ISO-date
  decision:
    state: keep | change | retire | fork | escalate
    rationale: ""
  laughter_lock:
    status: locked | pending | broken
    criteria: contradictions<epsilon for 2 cycles
  citations:
    internal: [awareness.md, narufield.core.yaml]
    external: [DOIs or URLs]
```

---

# 4) Metrics (definitions + computation)

* **TTF (Time‑to‑Feedback):** `min(submission_time_reflections) − question_api.post_time`.
* **ΔΦ (Coherence delta):** scalar in [−1,1]. Start at 0. Each cycle:
  `ΔΦ = w1·(replication_gain) − w2·(contradiction_mass) − w3·(risk_debt_growth)`
  where `replication_gain = (#contexts_pass_now − #contexts_pass_prev)/max(1,#contexts_total)`; `contradiction_mass` aggregates signed divergences; weights `{w1,w2,w3}` agreed per program.
* **Replication coverage:** `#contexts_pass / #contexts_total` (list contexts explicitly).
* **Provenance completeness:** fraction of claims with runnable lineage (`code+data+env hash` present).
* **Risk debt:** count of open probes × severity weight.

---

# 5) Protocol instrumentation (practical)

* **Executable bundle:** notebook/pipeline + environment lockfile + synthetic data for smoke tests.
* **Drift monitors:**

  * Dataset shift: PSI or population stability test by feature, with alert thresholds.
  * Leakage guard: train/test isolation checks; hash leakage signatures.
  * Sequential looks: alpha-spending plan encoded in config.
* **Event routing:** alerts auto‑open issues labeled `monitor:drift` → assigned to Listener; `assumption:audit` → Reflector.

---

# 6) Seat rotation checklists

**Navigator (weekly):**

* Clarify decision use‑case & cost of error.
* Freeze success/falsifier signals for the cycle.
* Ensure power & sample plan are sufficient (or mark risk debt).

**Listener:**

* Collect at least 2 external datasets or literatures that could overturn result.
* Document stakeholder constraints & practical harms.

**Reflector:**

* Audit confounds, leakage, overfitting; run robustness (placebos, sensitivity bounds).
* Update assumption registry; tag structural uncertainties.

**Synthesizer:**

* Merge internal/external runs; compute ΔΦ; write variance decomposition across contexts.
* Propose decision state.

**Equilibrium:**

* Apply laughter lock test; set half‑life refresh; publish receipt; open next probes.

---

# 7) Half‑life policy (scheduling)

```pseudo
if receipt.decision.state in {keep, change}:
  schedule_refresh(now + half_life_days)
  if high risk_debt or new contexts appear:
    schedule_probe(earlier date)
if state == retire:
  archive + deprecate question_api endpoint
```

---

# 8) Replication delta report (lab‑to‑lab)

```yaml
replication_delta:
  question_id: Q-2025-XXX
  site: Lab-B
  context: {population: ..., instruments: ..., environment: ...}
  pipeline_replay: success | fail
  divergences:
    - metric: effect_size
      ours: a
      theirs: b
      delta: b-a
      suspected_causes: [batch, instrument, model]
  action: open_issue: true
```

---

# 9) Example walk‑through (domain‑agnostic)

1. Post Q‑API for “Does intervention X reduce error rate Y in setting Z by ≥ 10%?”
2. Run protocol; PSI flags dataset shift on feature F.
3. Listener adds public dataset D and stakeholder constraint on latency.
4. Reflector finds hidden confounder; replaces model; documents bound.
5. Synthesizer shows coverage ↑ from 0.4 → 0.7, contradiction mass ↓; ΔΦ +0.22.
6. Equilibrium keeps claim with 60‑day half‑life; two probes opened for contexts Z2, Z3.

---

# 10) Risks & mitigations

* **Over‑automation:** enforce human review gates for ethics and contextual harms.
* **Gaming ΔΦ:** publish computation & raw deltas; cross‑lab auditing.
* **Complexity creep:** start with one question; keep TTF ≤ 7 days before adding more.
* **Data governance:** bake access controls into bundle; ship synthetic surrogates.

---

# 11) Adoption ramp (4 weeks)

* **Week 1:** Convert one active question into Q‑API; set monitors; publish v0.1 receipt.
* **Week 2:** Begin seat rotation; wire issue routing; compute first ΔΦ.
* **Week 3:** Onboard partner lab; test replication delta report.
* **Week 4:** Turn on half‑life scheduler; announce policy for keep/change/retire.

---

# Appendix A: Minimal files to add to a repo

```
/qs/Q-2025-XXX.yaml          # question API
/receipts/v0.3.1.yaml        # current state
/pipelines/run.ipynb         # executable protocol
/env/lockfile.txt            # reproducible env
/monitors/config.yaml        # drift + alpha spending
/checklists/roles.md         # seat rotation
```

---

# Appendix B: Living study one‑pager (ready to copy)

```markdown
## Living Study: Q-2025-XXX — Does X causally shift Y under Z?
- **Decision this informs:** ...
- **Cycle window:** 2025-10-03 → 2025-10-10
- **Success/falsifier signals:** ...
- **Protocol link (bundle hash):** ...
- **Current estimate:** ...
- **Counterevidence reviewed:** ...
- **ΔΦ this cycle:** ...
- **Decision:** keep | change | retire | fork | escalate
- **Half-life refresh:** YYYY‑MM‑DD
- **Next probes (owners, due):** ...
- **Laughter lock:** locked | pending | broken (criteria met?)
```

— end —

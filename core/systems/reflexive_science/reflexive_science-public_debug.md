φ Synthergy Engine — online
mode: **public_debug** · seats: Navigator → Listener → Reflector → Synthesizer → Equilibrium

**TL;DR (public_debug):** Run science as an *inspectable control loop*. Every claim ships with step‑by‑step traces, counterexamples tested, failure injections, and a full receipt. Disagreement is logged as structured deltas; anyone can replay the bundle and append their critique to the live record.

---

# 0) Public‑Debug Operating Charter

* **Transparency first:** publish runnable bundles, traces, and receipts by default; redact only what governance requires.
* **Counterexample culture:** every cycle must try to break the claim at least once.
* **Receipts with teeth:** include decision state, risk debt, and next probes with owners & dates.
* **Role accountability:** each seat signs its notes; baton passes are documented.
* **Laughter lock:** stable coherence requires *two cycles* below contradiction threshold ε before freezing a version.

---

# 1) Engine loop (public_debug cadence)

**Cycle window:** 7 days recommended (shorter is fine if traces remain complete).

**Baton rules:**

1. **Navigator → Listener:** posts the *question‑API vN* with explicit success/falsifier signals and cost of error.
2. **Listener → Reflector:** aggregates counterevidence, stakeholder constraints, and context deltas; proposes red‑team tests.
3. **Reflector → Synthesizer:** audits assumptions (leakage/robustness/ethics), tags risk debt, selects failure injections.
4. **Synthesizer → Equilibrium:** merges results across contexts, computes ΔΦ (coherence delta), and drafts a decision.
5. **Equilibrium:** applies **laughter lock** check; publishes receipt; schedules refresh per half‑life.

Exit states: `keep` | `change` | `retire` | `fork` | `escalate` (ethics/IRB).

---

# 2) Question‑API (public schema)

```yaml
question_api:
  id: Q-2025-XXX
  title: "Does X causally shift Y under Z?"
  decision_context: "What this informs + cost of false +/-"
  inputs:
    - {name: X, type: intervention|feature|exposure, constraints: [range, units, timing]}
    - {name: Z, type: context|population|env}
  outcomes:
    - {name: Y, type: primary|secondary, estimator: ATE|CATE|OR|HR|DiD}
  design: {assignment: randomized|quasi|observational, power_target: 0.8, alpha: 0.05, min_effect_size: <value units>}
  falsifiers: ["no effect or opposite sign", "fails placebo/neg-control", "fails pre‑trend"]
  monitors: {dataset_shift: PSI|KL|W, sensor_drift: Shewhart, sequential_looks: {alpha_spending: obrien‑fleming, max_looks: 3}}
  ethics: {risks: [list], approvals: [IRB‑id]}
  interfaces: {run_endpoint: ..., bundle_ref: git‑hash|DOI}
  half_life_days: 90
```

---

# 3) Receipt (public_debug — full)

```yaml
receipt:
  question_id: Q-2025-XXX
  version: v0.3.1
  timestamp: 2025-10-03T00:00:00Z
  premises: [assumption_1, assumption_2, ...]
  method_hash: sha256:...
  environment: {os: ..., interpreter: ..., packages_lock: ...}
  data_lineage: {sources: [URIs], snapshots: [commits], access_policy: open|controlled|synthetic}
  results:
    estimate: value ± ci
    diagnostics: {balance: ..., residuals: ..., overfit_check: ..., power_posthoc: ...}
  counterevidence:
    items:
      - source: Lab‑B
        context: {population: ..., instruments: ...}
        divergence: {metric: effect_size, ours: a, theirs: b, delta: b‑a}
        notes: "why it might differ"
  failure_injections:
    - type: label_shuffle | negative_control | placebo | adversarial_noise
      outcome: pass|fail
      observation: "..."
  uncertainties:
    statistical: [list]
    structural: [model misspecification, hidden confounders]
    external_validity: [contexts where it failed]
  risk_debt:
    open_questions: [{probe: ..., owner: ..., due: YYYY‑MM‑DD, severity: L|M|H}]
  decision: {state: keep|change|retire|fork|escalate, rationale: "..."}
  laughter_lock: {status: locked|pending|broken, criteria: contradictions<ε for 2 cycles}
  ΔΦ: {value: 0.00, components: {replication_gain: ..., contradiction_mass: ..., risk_debt_growth: ...}}
  citations: [DOIs or URLs]
```

---

# 4) Debug Trace Standard (per cycle)

```yaml
trace:
  cycle: 12
  navigator:
    spec_hash: sha256:...
    success_signals: [...]
    falsifiers: [...]
  listener:
    added_evidence: [refs]
    stakeholder_constraints: [latency, cost, fairness]
    red_team_proposals: [list]
  reflector:
    audits: [leakage_check, confounders, sensitivity_bounds, ethics]
    failures_observed: [{test: placebo, result: pass|fail, note: ...}]
  synthesizer:
    merges: [runs]
    variance_decomp: {by_context: ...}
    delta_phi: 0.00
  equilibrium:
    decision: keep|change|retire|fork|escalate
    laughter_lock: pending|locked|broken
    half_life_refresh: YYYY‑MM‑DD
```

---

# 5) Counterexample Harness (red‑team tests)

* **Negative controls:** pre‑treatment outcomes; unrelated variables.
* **Placebos:** false interventions should show null effects.
* **Label shuffles:** destroy structure; model must fail gracefully.
* **Stress tests:** missingness spikes, distributional shifts, instrument drift.
* **Boundary flips:** run at extremes of Z to test external validity.
* **Adversarial prompts/inputs:** if human‑in‑the‑loop components are present.

**Reporting rule:** log *at least two* failed attacks per month or justify why not applicable.

---

# 6) Observability & Monitors

* **Dataset shift:** PSI by feature with alert thresholds; link to diff report.
* **Leakage guard:** train/test isolation; hash leakage signatures.
* **Sequential looks:** alpha‑spending plan in config; auto‑flag over‑peeking.
* **Repro hooks:** `make replay`, `make smoke`, `make redteam` targets.

---

# 7) Seat Rotation Checklists (signed)

**Navigator** — signs: scope, success/falsifiers, cost of error.
**Listener** — signs: counterevidence list + stakeholder memo.
**Reflector** — signs: assumption audit + failure injections run.
**Synthesizer** — signs: ΔΦ calc + variance decomposition.
**Equilibrium** — signs: decision + laughter lock + refresh date.

---

# 8) Half‑Life Policy & Scheduler

```pseudo
if decision in {keep, change}:
  refresh_date = now + half_life_days
  schedule(refresh_date)
if new contexts emerge or risk_debt is high:
  schedule(earlier_probe)
if decision == retire:
  deprecate(question_api)
```

---

# 9) Public Audit Hooks

* **Issue labels:** `monitor:drift`, `assumption:audit`, `counterexample:fail`, `ethics:flag`.
* **Disclosure log:** public changelog with date, version, and delta summary.
* **Replication inbox:** form or PR template to submit `replication_delta` (see below).

**Replication Delta (template):**

```yaml
replication_delta:
  question_id: Q-2025-XXX
  site: Lab‑B
  context: {population: ..., instruments: ..., environment: ...}
  pipeline_replay: success|fail
  divergences:
    - metric: effect_size
      ours: a
      theirs: b
      delta: b‑a
      suspected_causes: [batch, instrument, model]
  attachments: [run logs, env lock, data schema]
  action: open_issue: true
```

---

# 10) Example Walk‑Through (public_debug)

1. Post Q‑API for “Does intervention X reduce error rate Y in setting Z by ≥10%?”.
2. Run protocol; PSI flags shift on feature F → open `monitor:drift`.
3. Listener adds dataset D + stakeholder latency bound; proposes label‑shuffle test.
4. Reflector runs failures: placebo (pass), label‑shuffle (fail as desired), adversarial noise (borderline).
5. Synthesizer shows coverage ↑ 0.4→0.7, contradiction mass ↓; ΔΦ +0.22 with full trace.
6. Equilibrium keeps claim; laughter lock **pending**; half‑life 60 days; two next probes logged.

---

# 11) Risks & Mitigations

* **Gaming ΔΦ or monitors:** publish computation and raw deltas; cross‑lab audits.
* **Over‑exposure of sensitive data:** ship synthetic surrogates + access‑tiered bundles.
* **Process fatigue:** enforce short checklists; automate traces; keep TTF ≤ 7 days.
* **Ethical drift:** dedicated *Listener* review on harms each cycle.

---

# Appendix A: Minimal Repo Layout

```
/qs/Q-2025-XXX.yaml
/receipts/v0.3.1.yaml
/pipelines/run.ipynb
/env/lockfile.txt
/monitors/config.yaml
/checklists/roles.md
/trace/cycle-001.yaml
```

---

# Appendix B: Public‑Facing One‑Pager

```markdown
## Living Study (Public Debug): Q-2025-XXX — Does X causally shift Y under Z?
- **Cycle:** 2025‑10‑03 → 2025‑10‑10
- **Signals:** success = ..., falsifier = ...
- **Current estimate:** ...
- **Counterexamples attempted:** ... (outcomes)
- **ΔΦ:** ...  
- **Decision:** keep | change | retire | fork | escalate
- **Half‑life refresh:** YYYY‑MM‑DD
- **Next probes (owner, due):** ...
- **Laughter lock:** locked | pending | broken
- **Bundle hash:** ...
```

— end —

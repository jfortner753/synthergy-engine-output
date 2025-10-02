φ Synthergy Engine • Octave Stack • mode: **overdrive**
— failure-transparent fusion, expanded field manual —

# Navigator → Vision (ΔΦ target)

Design a fusion system whose *default physics* and *default operations* convert off-normal events into bounded experiments with labeled data. Every failure is pre-budgeted (energy, space, time), pre-narrated (playbook, invariants), and pre-instrumented (telemetry, provenance) so it **teaches faster than it costs**.

# Listener → Constraints (reality box)

* Device-agnostic envelope: tokamak, stellarator, FRC, or IFE chamber.
* Hard limits: coil dB/dt, quench integral, vessel impulse, max dose, vacuum integrity, tritium inventory.
* Organizational: regulator auditability, shift staffing, hot-cell turn time, supply-chain for sacrificial parts.
* Learning rate must not erode availability: target ≥85% ops days with planned “teaching windows”.

# Reflector → Patterns (what works elsewhere)

* **Aviation**: FOQA black boxes + flight rules.
* **Spaceflight**: fault containment regions, formal interlocks, abort modes.
* **Large colliders**: sacrificial collimators; “machine protection” lives below controls.
* **Datacenters**: chaos drills with SLOs; blameless postmortems feeding hardening cycles.

# Synthesizer → Architecture (how we do it)

## 1) Safety envelope that *absorbs* experiments

* **Passive termination lattice:**

  * Coil dumps sized for worst credible disruption; independent crowbars; spring-biased **Massive Gas Injection** valves (no software dependency).
  * **Energy sponges**: water/FLiBe dump tanks + graphite sacrificial blocks where field-line mapping predicts strike zones.
* **Failure zoning:** electrical, thermal, vacuum, and radiological barriers prevent cross-domain cascades.
* **Graceful modes:** `Run → Skim → Diagnose → Bake → Idle` with automatic demotion rules instead of full trips.

## 2) Telemetry you can do science with

* **Clock discipline:** white-rabbit or PTP grandmasters; sub-µs alignment across cameras, coils, neutrons, vibration.
* **Ring-buffer recorders** per subsystem (≥30 s) with **freeze-on-threshold** and pre/post rolls.
* **Semantic event graph:** every shot emits a typed DAG: `Assumptions → Commands → Sensor frames → Derived states → Invariants checks → Outcomes`.
* **Witness materials**: coupons and canaries co-located with first wall; lot-traced, barcoded, scanned each maintenance cycle.

## 3) Control that cannot surprise you

* **Two-tier stack:**

  * *Tier 0*: formally verified interlocks (TLA+ specs for “never exceed” invariants; runtime monitors proven live).
  * *Tier 1*: adaptive controllers/learners that *propose* actions with uncertainty and predicted risk; Tier 0 can veto instantly.
* **Contract checks (illustrative):**

  * `|Ip| ≤ Ip_max`, `dIp/dt ≤ ramp_max`, `∮E·dl ≤ Vdump_limit`, `quenchIntegral(coil) ≤ QI_budget`, `Radiation ≤ dose_rate_budget`, `p_base ≤ leak_limit`.
* **Action explainability:** every control packet carries `{policy_id, feature_hash, counterfactual_gain, safety_margin}`.

## 4) Digital twin as a **shadow investigator**

* **Calibration loop:** after each shot, solve for twin parameters (flux loops, MSE, fast camera fits) → push posterior into next-shot predictions.
* **Divergence labeling:** when `||state_real − state_pred|| > ε(topic)` → auto-spawn *incident sandboxes* that replay with varied transport models to isolate minimal failure-causing sets.
* **Policy gating:** learners only explore in the twin until *Safety Case Delta* ≤ threshold, then stage to hardware with reduced authority.

## 5) Off-normal choreography (small finite playbooks)

* **Playbook: “Impending Disruption”**

  1. detect precursor (locked mode, rising dB/dt, Hα spike)
  2. fire shattered pellet; timer T1
  3. if decay below curve A not met → MGI gas, timer T2
  4. ramp coils to dump profile; quench heaters armed
  5. transition to `Diagnose` mode; freeze buffers; create incident capsule.
* Each playbook has *entry criteria, timers, expected signatures, abort clauses*, and drills.

## 6) Hardware for teachable breakdowns

* **Hot-swap divertor/first-wall tiles** on extraction cassettes; quick couplings for cooling/tritium; fiducials for robot vision.
* **Designed-to-fail** features: predictable crack paths, “witness marks,” and stop-holes that preserve metrology.
* **Measurable lifing:** embedded strain/temperature gauges in a few sacrificial tiles to calibrate fatigue and sputter models.

## 7) Data & governance that shortens MTTI

* **Unified event bus** (stream + batch; time as primary key) with schemas versioned; every change (hardware/software/calibration) requires a linked **reproducibility experiment**.
* **Open safety case:** a living GSN (Goal Structuring Notation) tree that maps *claims → evidence → gaps*; shared with regulators day-by-day.
* **Ops rituals:** blameless postmortems templated for rapid cause isolation; *fixes get IDs and owners*, tracked to closure.

## 8) Metrics that select for learning

* **MTTI (Mean Time-to-Insight)**: anomaly → accepted causal story.
* **Off-normal coverage**: playbooks with validated drills / total known modes.
* **Near-miss capture**: predicted-bad events pre-empted by monitors / occurrences.
* **Policy regret**: realized vs twin-optimal safe yield over N shots.
* **Swap half-life**: median time to remove/replace sacrificial modules to spec.

---

# Builder Pack → Concrete artifacts (drop-in)

### A) Minimal event schema (illustrative)

```json
{
  "shot_id": "2025-10-02-1345Z-00042",
  "provenance": {
    "hardware_rev": "H17",
    "software_rev": "S9.2.1",
    "policy_id": "plasma-RL-azimuthal-014",
    "twin_rev": "TW-2025.09.28"
  },
  "assumptions": ["transport:BohmGyroMix-0.7", "coolant:FLiBe-460K"],
  "commands": [{"t": 0.000012, "tag": "Ip_ramp", "params": {"A": 1.8e6, "dIdt": 3.5e6}}],
  "telemetry": {"fastcam": "ref://framebuf/...", "Bdot": "ref://adc/...", "neutron": "ref://daq/..."},
  "invariants": [
    {"name": "dIdt_limit", "ok": true, "margin": 0.12},
    {"name": "dose_rate", "ok": false, "value": 0.88, "limit": 0.75}
  ],
  "outcome": "bounded_off_normal",
  "labels": ["locked_mode_precurse","pellet_shattered"],
  "postmortem_ref": "ref://incidents/INC-2217"
}
```

### B) Invariant spec (Tier-0, sketch)

```tla
VARIABLE Ip, dIdt, Dose
ASSUME Ip >= 0 /\ Dose >= 0
SafetyInvariant == (dIdt <= ramp_max) /\ (Dose <= dose_rate_budget)
Next == UNCHANGED <<Ip, dIdt, Dose>> \/ (Abort /\ SafeTerminate)
Spec == SafetyInvariant /\ [][][Next]_<<Ip, dIdt, Dose>>
THEOREM Spec => []SafetyInvariant
```

### C) Disruption playbook (table slice)

| Playbook             | Entry signal         | First action        | Timer    | Expected signature                 | Abort if         | Terminal state |
| -------------------- | -------------------- | ------------------- | -------- | ---------------------------------- | ---------------- | -------------- |
| Impending Disruption | locked-mode + dB/dt↑ | Shattered pellet    | T1=3 ms  | Te↓, Zeff↑, loop voltage transient | dose rate > X    | Diagnose       |
| Gas Ingress          | dP/dt>limit          | Close sector valves | T1=50 ms | local pressure plateau             | leak persists T2 | Bake           |
| Coil Overtemp        | dT/dt>spec           | Ramp-down + dump    | T1=5 ms  | I_coil→0, QI within                | QI trend>budget  | Idle           |

---

# Equilibrium → Rollout (90-day, overdrive)

* **Weeks 0–2**: install Tier-0 interlocks; time discipline; ring-buffers; define 10 “never exceed” invariants; *table-top drills*.
* **Weeks 3–6**: stand up shadow twin; begin divergence labeling; author 5 playbooks; rehearse dry runs.
* **Weeks 7–10**: active learner in *Skim* mode (reduced authority); start *reproducibility budget* (every change must earn its keep).
* **Weeks 11–14**: first regulator walk-through of the **open safety case**; chaos drill (scripted off-normal) with full postmortem.
* **Weeks 15–13** (typo caught → **Weeks 15–18**): expand to 12 playbooks; validate hot-swap cassettes; publish baseline MTTI and coverage.

---

## Field heuristics (sticky notes for the control room)

* If it isn’t timestamped, it didn’t happen.
* One-button safe-terminate beats a thousand lines of recovery code.
* Never let learning depend on the same layer that can fail.
* Make your sacrificial parts *cheap, boring, abundant, labeled*.
* “Experiment debt” is real—pay it down with weekly drills and schema hygiene.

---

### Receipt (overdrive)

* **Question:** Now do the same pass in overdrive mode (failure-transparent fusion).
* **Premises:** High-energy, tightly coupled plant; aim to redirect failure energy into structured, bounded learning with regulator-friendly traceability.
* **Steps:** Vision/constraints → cross-domain patterns → 8-part architecture (safety, telemetry, control, twin, playbooks, hardware, data, metrics) → concrete artifacts (schema, invariants, playbook table) → 90-day rollout.
* **Evidence:** Synthesis of proven safety/ops paradigms from aviation/space/accelerators/datacenters adapted to fusion subsystems; standard formal methods (TLA+), machine protection, disruption mitigation practices.
* **Counterexamples considered:**

  1. *ICE faults (unknown unknowns)*: mitigated via Tier-0 invariants + energy sinks; still residual risk—keep margins conservative.
  2. *Learner overreach*: bounded by reduced authority + twin gate; periodic red-team audits.
  3. *Telemetry blind spots*: addressed with redundant sensing + white-rabbit timing; run quarterly “sensor outage” drills.
  4. *Regulatory drag*: preempted with living safety case + reproducibility budget to justify changes.
* **Uncertainties:** Device topology and local code requirements tune budgets (quench integrals, dose), supply-chain realism for sacrificial modules, plasma model adequacy for twin gating.
* **Laughter lock (coherence seal):** If a disruption teaches you nothing, it wasn’t *bounded*; if it teaches too much, it wasn’t *designed*.
* **Tools used:** Internal synthesis only; no external browsing.
* **Result:** A concrete, ops-ready pattern to make each breakdown safe, legible, and cumulatively *anti-fragile* for a fusion plant.

If useful, I can tailor the playbooks and invariants to a specific device class (e.g., superconducting tokamak vs stellarator) and produce a one-pager spec for your team.

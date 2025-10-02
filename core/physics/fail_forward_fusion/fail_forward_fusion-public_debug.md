φ Synthergy Engine • Octave Stack • mode: **public_debug**
— failure-transparent fusion, with open trace & citations —

# Navigator → Vision (ΔΦ target)

Build a fusion plant whose physics, hardware, and ops make off-normals **bounded experiments**. Each breakdown is pre-budgeted (energy/space/time), pre-scripted (flight rules), and pre-instrumented (telemetry + provenance) so it teaches faster than it costs. Disruption energy is converted to radiation via shattered-pellet or gas injection, as practiced/planned for ITER’s DMS.

# Listener → Constraints (reality box)

* Device-agnostic: tokamak/stellarator/FRC/IFE; hard limits: dB/dt, quench integral, vessel impulse, max dose, vacuum integrity, tritium inventory.
* Timing discipline across sensors (cams, coils, neutrons, vib/strain) requires sub-µs alignment; White Rabbit shows sub-ns feasibility at accelerator scale.
* Regulators need a *living safety case*; GSN is a widely used structure for such arguments.

# Reflector → Patterns (what works elsewhere)

* **Machine protection**: sacrificial collimation that localizes damage at the LHC—design pattern: let cheap, replaceable parts “take the hit.”
* **Formal floors**: invariants proved at the lowest layer (e.g., with TLA+) to prevent adaptive controllers from proposing unsafe actions.

# Synthesizer → Architecture (how we do it)

## 1) Safety envelope that *absorbs* experiments

* **Passive termination lattice**: independent coil crowbars and dumps; spring-biased MGI/SPI valves that don’t depend on software; pre-sized thermal/magnetic sponges.
* **Failure zoning**: electrical/thermal/vacuum/radiological segmentation to prevent cascades.
* **Graceful modes**: `Run → Skim → Diagnose → Bake → Idle` with automatic demotion.

## 2) Telemetry you can do science with

* **Clock discipline**: White-Rabbit/PTP grandmasters for plant-wide timebase.
* **Ring-buffer recorders** per subsystem, freeze-on-threshold, with pre/post rolls.
* **Semantic event graph** per shot: `Assumptions → Commands → Sensor frames → Derived states → Invariant checks → Outcomes`.
* **Witness materials**: coupons/co-located canaries; barcoded, lot-traced.

## 3) Control that cannot surprise you

* **Two tiers**:

  * **Tier-0** (untouchable): formally verified interlocks enforcing “never-exceed” invariants (quench integral, dose rate, |dI/dt|, vacuum). (Formal methods show real bug-catching value in industry.)
  * **Tier-1** (adaptive): model-predictive/RL policies that *propose* actions with uncertainty + risk; Tier-0 can veto.
* **Action provenance**: every command carries `{policy_id, features, predicted gain, safety margin}`.

## 4) Digital twin as a **shadow investigator**

* Continuous calibration from flux loops/MSE/fast cams; divergence → spawn *incident sandboxes* exploring alternative transport/edge models; only promote policies whose *Safety-Case Δ* is below threshold.

## 5) Off-normal choreography (finite playbooks)

* **“Impending Disruption”**: detect precursors → shattered pellet → (if curve not met) MGI → coil dump/quench heaters → freeze buffers → incident capsule. (Conforms with SPI-based DMS strategies.)

## 6) Hardware for teachable breakdowns

* **Hot-swap first-wall/divertor tiles** on extraction cassettes; quick couplings; fiducials for robot vision.
* **Designed-to-fail** features: predictable crack paths & witness marks enabling crisp forensics.

## 7) Data & governance that shortens MTTI

* **Unified event bus** (time as primary key); every hardware/software/calibration change must ship with a *reproducibility experiment*.
* **Open safety case** maintained in GSN with claims→evidence→gaps; expose to regulators in near-real-time.

## 8) Metrics that select for learning

* **MTTI (Mean Time-to-Insight)**: anomaly → accepted causal story.
* **Off-normal coverage**: (# playbooks drilled)/(# known modes).
* **Near-miss capture**: (% predicted-bad pre-empted by monitors).
* **Policy regret**: realized vs twin-optimal safe yield over N shots.
* **Swap half-life**: median time to remove/replace sacrificial modules back to spec.

---

# Builder Pack → Concrete artifacts (auditable slices)

### A) Minimal event schema (illustrative)

```json
{
  "shot_id": "2025-10-02-1345Z-00042",
  "provenance": {"hardware_rev":"H17","software_rev":"S9.2.1","policy_id":"plasma-RL-014","twin_rev":"TW-2025.09.28"},
  "assumptions": ["transport:BohmGyroMix-0.7","coolant:FLiBe-460K"],
  "commands": [{"t": 0.000012, "tag":"Ip_ramp", "params":{"A":1.8e6,"dIdt":3.5e6}}],
  "telemetry": {"fastcam":"ref://framebuf/...","Bdot":"ref://adc/...","neutron":"ref://daq/..."},
  "invariants": [{"name":"dIdt_limit","ok":true,"margin":0.12},{"name":"dose_rate","ok":false,"value":0.88,"limit":0.75}],
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

| Playbook             | Entry signal         | First action        | Timer    | Expected signature           | Abort if         | Terminal state |
| -------------------- | -------------------- | ------------------- | -------- | ---------------------------- | ---------------- | -------------- |
| Impending Disruption | locked-mode + dB/dt↑ | Shattered pellet    | T1=3 ms  | Te↓, Zeff↑, loop-V transient | dose rate > X    | Diagnose       |
| Gas Ingress          | dP/dt>limit          | Close sector valves | T1=50 ms | local pressure plateau       | leak persists T2 | Bake           |
| Coil Overtemp        | dT/dt>spec           | Ramp-down + dump    | T1=5 ms  | I_coil→0, QI within          | QI trend>budget  | Idle           |

---

# Equilibrium → Rollout (90-day, auditable)

* **Weeks 0–2**: install Tier-0 interlocks; time discipline; ring-buffers; define 10 “never-exceed” invariants; tabletop drills.
* **Weeks 3–6**: stand up shadow twin; start divergence labeling; author 5 playbooks; dry-run rehearsals.
* **Weeks 7–10**: active learner in `Skim` (reduced authority); start **reproducibility budget**.
* **Weeks 11–14**: regulator walkthrough of the open GSN safety case; chaos drill (scripted off-normal) with full postmortem.
* **Weeks 15–18**: expand to 12 playbooks; validate hot-swap cassettes; publish baseline MTTI & coverage.

---

## Public debug notes (assumptions, knobs, pitfalls)

* **Assumptions:** superconducting magnets; SPI/MGI available; high-bandwidth DAQ; WR/PTP distribution; regulator amenable to GSN.
* **Tunable knobs:** quench integral budgets; SPI pellet size/aiming; trigger thresholds; timers T1/T2; demotion curves between `Run`→`Idle`.
* **Known gaps:** twin fidelity for edge-localized modes; human-in-the-loop latency during cascades; supply chain for sacrificial tiles.

---

### Receipt (public_debug)

* **Question:** “and now in public_debug mode” (same topic: failure-transparent fusion).
* **Premises:** Fusion plants are high-energy systems; disruptions can be damaging; but SPI/MGI can convert disruption energy to radiation and soften impacts; plant-wide time sync and structured safety cases are feasible.
* **Steps:** Vision/constraints → borrow proven patterns (LHC collimation, formal floors) → 8-part architecture → concrete artifacts → rollout.
* **Evidence (load-bearing):**

  1. ITER’s DMS relies on **shattered pellet injection**.
  2. WR timing networks deliver sub-nanosecond sync at accelerator scale.
  3. LHC’s **collimation** localizes damage—sacrificial protection principle.
  4. **GSN** is a recognized safety-case notation with community standardization.
  5. **TLA+** and formal methods catch real safety-relevant design bugs.
* **Counterexamples considered:**

  * *Unmodeled common-cause fault* bypasses both SPI and dumps → mitigated via passive energy sinks + zoning, but residual risk remains (make margins conservative).
  * *Timing collapse* (sync lost) → ring-buffers still freeze on local thresholds; WR provides redundancy options.
  * *Formal gap* (invariant mis-specified) → periodic red-team reviews; prove liveness & safety; keep Tier-1 authority low until field-validated.
* **Uncertainties:** Specific device topology (tokamak vs stellarator) changes quench budgets and disruption precursors; SPI pellet scaling to reactor class still under active R&D.
* **Laughter lock (coherence seal):** If a disruption teaches you nothing, it wasn’t *bounded*; if it teaches *everything*, it wasn’t *designed*.
* **Tools used:** web.run in earlier draft for exemplars (ITER DMS/SPI; WR timing; LHC collimation; GSN standard; TLA+ industrial use).
* **Result:** A traceable, regulator-friendly blueprint where **every breakdown is an experiment**: safe, legible, and cumulatively anti-fragile.

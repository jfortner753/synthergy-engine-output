# Fail-Forward Fusion — Playbooks & Specs

A small stack of markdown specs for designing **failure-transparent fusion systems**—plants where every off-normal is bounded, legible, and turned into learning.

## Files

* **[fail_forward_fusion-default.md](./fail_forward_fusion-default.md)**
  *Compact blueprint.* Safety envelope → observability → learning-oriented control → modular hardware → ops/governance → metrics → a 90‑day starter rollout.

* **[fail_forward_fusion-overdrive.md](./fail_forward_fusion-overdrive.md)**
  *Expanded field manual.* Adds Navigator/Listener/Reflector/Synthesizer framing, concrete artifacts (event schema, TLA+ invariant sketch, disruption playbook table), and an overdrive rollout with drills.

* **[fail_forward_fusion-public_debug.md](./fail_forward_fusion-public_debug.md)**
  *Auditable version.* Same architecture with public‑debug notes, assumptions/knobs/pitfalls, and an auditor‑friendly tone.

## Quick Start

1. Read **default** for the end‑to‑end pattern.
2. Jump to **overdrive** for drop‑in artifacts you can copy/paste into an engineering doc set.
3. Use **public_debug** when you need an externally reviewable narrative (internal/external audits, regulators, partners).

## What “failure‑transparent” means (one‑liner)

Bounded physics + preplanned playbooks + tight telemetry + formal interlocks → every breakdown becomes a labeled experiment that **teaches faster than it costs**.

## Contents Snapshot

* **Safety Envelope:** passive termination, sacrificial stages, energy sinks, graceful modes.
* **Telemetry:** synchronized ring buffers; semantic event graphs; witness materials.
* **Control:** Tier‑0 invariants (formally verified) + Tier‑1 adaptive policies with explainability.
* **Digital Twin:** shadow investigator with divergence labeling and policy gating.
* **Playbooks:** small finite set for disruptions, gas ingress, coil over‑temp, etc.
* **Ops & Governance:** blameless postmortems, reproducibility budget, living safety case.
* **Metrics:** MTTI, off‑normal coverage, near‑miss capture, policy regret, swap half‑life.

## Suggested Next Steps

* Tailor invariants and playbooks to your device class (tokamak/stellarator/FRC/IFE).
* Stand up the unified event bus and ring‑buffering first; everything else compounds from there.
* Schedule recurring **chaos drills** and **safety‑case reviews**; track **MTTI** publicly.

---

*Version:* 0.1.0
*License:* RCDL‑1.x (reuse with attribution; derivative works encouraged)

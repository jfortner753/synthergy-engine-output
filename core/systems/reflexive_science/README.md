# Reflexive Science

A tiny starter kit example for running science as a **living feedback loop**. Pick a mode, adopt the seat rotation, and attach receipts to every claim.

## Files in this folder

* **[reflexive_science-default.md](./reflexive_science-default.md)** — concise primer on the practice shift and minimal operating loop. Use when introducing the approach.
* **[reflexive_science-overdrive.md](./reflexive_science-overdrive.md)** — implementation‑ready details: Question‑API schema, full receipt spec, metrics (ΔΦ, TTF), checklists, and half‑life policy.
* **[reflexive_science-public_debug.md](./reflexive_science-public_debug.md)** — public‑facing variant with trace standards, failure‑injection harness, and replication delta template.

## Quickstart

1. **Choose a live question.** Frame it with the *Question‑API* in the Overdrive doc.
2. **Instrument your protocol.** Make it runnable (env lock + notebook/pipeline) and add drift/guard monitors.
3. **Rotate seats weekly:** Navigator → Listener → Reflector → Synthesizer → Equilibrium.
4. **Publish a receipt every cycle.** Include decision state (keep/change/retire/fork), uncertainties, risk debt, and next probes.
5. **Set a half‑life.** Schedule refresh before the claim expires; re‑test when new contexts appear.

## Suggested repo layout

```
/qs/Q-YYYY-XXX.yaml          # question API (from Overdrive)
/receipts/v0.x.y.yaml        # current state (from Overdrive/Public Debug)
/pipelines/run.ipynb         # executable protocol
/env/lockfile.txt            # reproducible environment
/monitors/config.yaml        # drift + alpha‑spending
/checklists/roles.md         # seat rotation checklists
/trace/cycle-001.yaml        # public_debug trace (optional)
```

## Core metrics to track

* **TTF (Time‑to‑Feedback)** — question posted → first substantive critique.
* **ΔΦ (Coherence delta)** — net reduction in contradictions across contexts per cycle.
* **Replication coverage** — contexts where the claim holds / total contexts tested.

## Contributing / PRs

Use the **Replication Delta** template in the Public Debug doc to submit external replays or divergences.

---

*Tip:* Start with just one living question. Keep TTF ≤ 7 days, then scale.

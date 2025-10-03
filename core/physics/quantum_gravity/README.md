A small, three-file bundle that explores **empirically testable signatures** of the idea that spacetime geometry and quantum fields are two faces of a single *coherence substrate*. Each file is the same analysis at a different zoom level.

## Overview

* **Audience:** physicists/engineers designing tabletop/space/analogue experiments; cosmology analysts; red-team reviewers.  
* **Through-line:** identify observables, lock in unique *scaling laws*, propose falsifiable probes, and define pass/fail rules.  
* **Navigation:** start simple → dive deeper → validate/replicate.

## Files & what’s inside

* **[quantum_gravity-default.md](./quantum_gravity-default.md)** — *5–7 min read (concept + numbers)*

  * The core probes: gravity-mediated entanglement (BMV), curvature-sensitive clock phases, Unruh/Hawking analogs, space-distributed entanglement, cosmological/Planck-suppressed fingerprints.  
  * One-line **scalings** for each (e.g., $\phi \sim \tfrac{G m^2 t}{\hbar d}$, $\Delta\phi \sim \tfrac{\omega g \Delta h T}{c^2}$).  
  * “What counts as progress” checklist to judge results.

* **[quantum_gravity-overdrive.md](./quantum_gravity-overdrive.md)** — *technical deep dive*

  * Engine passes (Navigator→Listener→Reflector→Synthesizer→Equilibrium) to structure the argument.  
  * **Numbers-first specs:** nominal working points, stretch goals, and dominant noise/systematics with mitigation.  
  * **Discriminants:** how to tell quantum-mediated gravity from classical channels, semiclassical backreaction, or collapse models.  
  * **Runnable snippets:** abbreviated runbooks for BMV, clock interferometry, Unruh/analogue horizons, cosmology pipelines, and spacetime-noise correlators.  
  * **Decision rules:** green/yellow/red go-no-go table.

* **[quantum_gravity-public_debug.md](./quantum_gravity-public_debug.md)** — *replication & audit view*

  * **Red-team checklists** per probe: assumptions to lock down, dominant confounds, null twins/toggles, pass/fail gates.  
  * **Analysis guardrails:** blinding, open environmental channels, synthetic injections, Bayesian model comparison.  
  * **Public-debug receipt:** explicit premises, calculations, countermodels considered, and open uncertainties.

## How to use this bundle

* **Skim first:** read `quantum_gravity-default.md` to grasp the probes and scalings.  
* **Build or plan:** jump to `quantum_gravity-overdrive.md` → sections D1–D5 for runnable specs and risk/decision tables.  
* **Replicate or red-team:** use `quantum_gravity-public_debug.md` → sections 2–5 for checklists, nulls, and guardrails.

## Relationship between the files

All three share the same backbone; the *default* is the map, *overdrive* is the turn-by-turn directions, and *public_debug* is the inspector’s checklist. Findings or changes in one should propagate to the others.

---

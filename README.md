<div align="center">

![Dataset](https://img.shields.io/badge/Dataset-beta--0.1-4ade80?style=flat-square&labelColor=0d1f15)
![Interactions](https://img.shields.io/badge/Interactions-~794-67e8f9?style=flat-square&labelColor=0d1f15)
![Substances](https://img.shields.io/badge/Substances-~41-fbbf24?style=flat-square&labelColor=0d1f15)
![App data](https://img.shields.io/badge/App%20data-static%20JSON%20snapshot-6366f1?style=flat-square&labelColor=0d1f15)
![TypeScript](https://img.shields.io/badge/TypeScript-compile%20pass-4ade80?style=flat-square&labelColor=0d1f15)
[![License: MIT](https://img.shields.io/badge/License-MIT-fbbf24?style=flat-square&labelColor=0d1f15)](LICENSE)

# EntheoGen

### A calm, evidence-grounded plant medicine interaction guide

**Deterministic, harm-reduction-oriented interaction readouts for intentional, informed psychedelic contexts.**

[→ Open the app](https://entheogen.azurewebsites.net) · [entheogen.newpsychonaut.com](https://www.entheogen.newpsychonaut.com/) · [Project wiki](https://github.com/EntheoGen-Development-Hub/EntheoGen/wiki) · [Discussions](https://github.com/EntheoGen-Development-Hub/EntheoGen/discussions)

</div>

---

> [!IMPORTANT]
> **EntheoGen is educational, not clinical advice.** Interaction data is curated for harm-reduction awareness. For medical decisions, consult a qualified healthcare professional.

---

## What EntheoGen is

EntheoGen is a **static, client-side interaction guide** built from a curated dataset of plant medicine and psychedelic substance pairs. It is not a medical application. It does not diagnose, prescribe, or recommend dosing.

The design goal is **quiet scientific credibility**: dark-forest foundations, glassy panels, luminous emerald/cyan/amber accents, and precise editorial language — a tool you can trust to give you the facts without alarm or marketing.

**Beta-0-1 (app)** ships as **static JSON** built from curated CSVs — no live database required for the public interaction guide.

> See [Beta-0-1 release notes →](https://github.com/EntheoGen-Development-Hub/EntheoGen/wiki/EntheoGen-Beta%E2%80%900%E2%80%901)

Since that baseline the repo has gained clearer automation and data-operation docs, optional **Supabase Phase 1** alignment for analytics and exports (not a runtime dependency for the SPA), and operational notes for parallel programmes (e.g. private beta launch) — without changing the core "snapshot in, UI out" contract.

---

## Data flow

| Artifact | Role |
|---|---|
| `interactions.csv`, `substances.csv` | Workspace inputs for regeneration |
| `npm run dataset:build-beta -- .` | Builds `src/data/substances_snapshot.json`, `src/exports/interaction_pairs.json` |
| `src/data/uiInteractions.ts` | Adapter layer: normalises CSV data to `UIInteraction` shape for the UI |

> After CSV edits, rebuild snapshots and commit JSON before treating a branch as release-ready.

---

## Developer quickstart

```bash
npm install
npm run dataset:build-beta -- .
npm run typecheck
npm test
```

Broader CI-style gate:

```bash
npm run ci:checks
```

See [`docs/automation/QUALITY_AND_RELIABILITY.md`](docs/automation/QUALITY_AND_RELIABILITY.md) for the full gate definition.

---

## Where to read more

| Topic | Location |
|---|---|
| **Supabase:** install `interactions_enriched` view | `docs/metabase/supabase-install-interactions-enriched-view.sql` |
| **Analytics:** Metabase pair-analysis model | `docs/metabase/interactions_enriched.sql` |
| **Analytics:** Metabase wiki dashboard embed | `docs/metabase/wiki-dashboard-embed.md` |
| Automation roles and safety | `docs/automation/AUTOMATION_AGENTS.md` · `docs/automation/AGENT_AND_SAFETY_OUTPUTS.md` |
| Intake and submissions | `docs/automation/INTAKE_AND_INTEGRATION.md` · `docs/automation/SUBMISSION_HOW_TO.md` |
| Backend / data foundations | `docs/automation/BACKEND_AND_DATA_FOUNDATIONS.md` |
| Repo layout | `docs/REPO_LAYOUT.md` |
| Private student beta (ops) | `docs/private-student-beta/README.md` |
| Contributor / agent rules | `AGENTS.md` |

**Wiki and community**

- [Project wiki](https://github.com/EntheoGen-Development-Hub/EntheoGen/wiki) — release notes and narrative history
- [Discussions](https://github.com/EntheoGen-Development-Hub/EntheoGen/discussions) — feedback and community input

---

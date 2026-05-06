# Copilot Instructions

Use this repository as the operating source for EntheoGen changes.

## Design system

When editing GitHub-facing pages, docs, templates, or public web surfaces,
preserve the EntheoGen design language from `src/index.css`, `src/App.tsx`,
and `public/public.html`.

EntheoGen should feel **calm, luminous, evidence-grounded, and harm-reduction
oriented**. The visual foundation is deep forest/obsidian (`#050D08`), with
glassy panels (`rgba(20,30,24,0.4)`), subtle emerald (`#73f0b1`), cyan
(`#96f4ff`), and amber (`#ffd582`) accents, careful spacing, and precise
educational language.

Do not make it look like a generic SaaS landing page, psychedelic poster,
wellness brand, or clinical hospital dashboard. Avoid overclaiming medical
authority. Keep copy educational and safety-aware.

For GitHub Markdown surfaces, approximate the brand through structure, wording,
badges, tables, callouts, diagrams, and linked visual assets rather than
unsupported custom CSS.

## Scope

- App UI and adapters live under `src/`, especially `src/data/uiInteractions.ts`.
- Knowledge-base sources, claim artifacts, schemas, and indexes live under
  `knowledge-base/`.
- Repeatable data and validation work lives under `scripts/` and is exposed
  through `package.json` when it is part of the standard workflow.
- Repository layout notes live in `docs/REPO_LAYOUT.md`.

## Automation role

Automation may draft scoped changes, run local checks, and summarize residual
risks in PR-ready form. Humans retain final authority over safety
interpretation, publication, dataset acceptance, and high-impact product
decisions.

Do not treat external workspace playbooks, local cache folders, or absent paths
as operational facts for this repo. If a path, script, or workflow is not
present here, describe it as proposed work instead of relying on it.

Keep technical verification separate from project-management ceremony. Tests,
CI, scripts, and build checks should prove implementation behavior, data
validity, or build health. They must not fail because a PR lacks a Linear issue,
because provenance/checklist/template fields are incomplete, because a branch is
named differently, or because an agent/delegate label is absent. Treat those
fields as optional traceability notes unless a human explicitly requests
enforcement.

Before adding any test, script, CI check, or package command, confirm it proves
runtime, code, data, schema, build, or executable workflow behavior. Do not add
checks that assert Linear references, PR-template wording, branch names,
checklist completion, provenance fields, issue labels, agent identity, or
documentation anchors.

## Repo-local verification

Prefer the narrowest command that proves the change:

```sh
npm run test:submission-intake
npm run typecheck
npm run validate:interactions:v2
npm run kb:validate
npm test
```

For documentation-only edits, at minimum check Markdown diffs for stale paths,
commands that are not in `package.json`, and claims that imply autonomous
publication or medical authority.

For rapid manual submissions or natural-language report intake, use
`docs/automation/SUBMISSION_HOW_TO.md` as a reference. It does not replace the
existing parser, workflow transition scripts, prompt contracts, or review
gates.

# Software Factory

Independent, advisory engineering Planner extracted from Relay `main` at `5dc67c27904cede5d1c9db53104cd7bb6ebc07e7` for [Issue #1](https://github.com/putman44/software-factory/issues/1). It selects bounded source context, validates issue and response identities, and produces an advisory handoff. It does not dispatch an Implementer.

## Offline verification

Use Node 24 and npm. From this checkout:

```sh
npm ci
npm run smoke:offline
git diff --check
```

The smoke command typechecks and runs focused tests with in-memory provider stubs and temporary local Git repositories. It requires no Relay checkout, database, application runtime, API key, or live provider. CI checks the exact pull request head SHA.

## Planner boundary

The `prepare-planner-handoff.ts` command supports context preview with `--issue N --repo owner/repo --checkout path --preview-context`; it reads the issue using `gh` and inspects the selected local checkout. Preview does not call a model. A live handoff requires `--allow-live-api`, `--output path`, a valid API key, and separate per-request human approval. The direct `run-api-planner.ts` entry point has the same explicit live flag. Neither is part of the offline smoke test or CI.

The output is advisory: `READY` does not grant implementation authority. Consult [AGENTS.md](AGENTS.md) for execution gates and [docs/extraction-map.md](docs/extraction-map.md) for provenance and Relay cleanup steps.

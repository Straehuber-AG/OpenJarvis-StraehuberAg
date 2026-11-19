# Straehuber AG fork of OpenJarvis

This fork is the Jarvis engine for the Straehuber platform (Baustellen-App, `Straehuber-AG/baustellen-app`).
Upstream: `open-jarvis/OpenJarvis` (Apache 2.0). Plan and rules on the app side:
`docs/specs/jarvis.md` and `docs/plan/baustelle-build-plan.md` in the Baustellen-App repo.

## Role in the platform
- Runs only on the EU worker as a provider behind the Baustellen-App's `LanguageProvider` interface.
- Never reads the app database, never talks to a screen, never stores customer data. Facts come in through
  the app's tool layer under the claims of the person Jarvis serves; answers go back as KI-Entwurf.
- Two roles: worker Jarvis and project manager Jarvis (see the app's `docs/specs/jarvis.md`).
- Local models first (Ollama or vLLM on the EU GPU server); a cloud model only through the platform's
  approved, EU-hosted provider.

## What lives where
| Content | Where |
|---|---|
| Upstream engine | everything outside `straehuber/`, kept as close to upstream as possible |
| Construction skills (generic, no company data) | `straehuber/skills/` (agentskills format) |
| Role profiles, tool list, guardrail tests | `straehuber/` |
| Company-specific prompts, tenant settings, any data | never here; they live in the Baustellen-App |

This repository is public. Nothing company-specific, no prompts with internal rules, no data.

## Rules for agents
1. Change only `straehuber/` and the files listed in `straehuber/PATCHES.md`; every change to upstream code
   is listed there with the reason, so upstream syncs stay simple.
2. Upstream sync: weekly, on a branch `sync/upstream-<date>`, tests green before merge.
3. Licence check on every dependency added: MIT, Apache, BSD, ISC only.
4. No telemetry or traces leave the server; local SQLite telemetry only.
5. Seed data only in tests.

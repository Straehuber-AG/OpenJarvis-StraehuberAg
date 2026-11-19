# straehuber/

Straehuber-specific parts of the Jarvis engine, kept apart from upstream code.

Planned (ticket M3-04 and M6-01/M6-02 in the Baustellen-App):
- `skills/`: generic construction skills in agentskills format (room briefing, Nachtrag draft, Tagesbericht
  draft, delivery note reading, material shortage note). No company data.
- `roles/worker.md`, `roles/project-manager.md`: tone, language handling, allowed tools, fixed refusals.
- `adapter/`: the small HTTP entry point the Baustellen-App worker calls (request in, KI-Entwurf with
  sources out), plus a fake mode for the app's tests.
- `tests/`: guardrail tests (refusals, no invented numbers, every statement has a source).

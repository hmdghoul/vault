---
tags: [engineering, conventions, code-review, tickets, writing]
read-when: Before writing a code-review finding, bug writeup, or explanation of how something works, or drafting ticket text.
---
# Review and Ticket Writing

Applies when drafting ticket text and when writing a code-review finding, bug writeup, or explanation of how something works. The ticket-premise procedure itself stays in `~/.claude/CLAUDE.md` under *Workflow*; this note covers only how the text is written.

## Ticket text
- Leave generated artefacts and the pipeline steps that produce them out of ticket text — descriptions, rollout sections, "done when" lists, PR checklists and hand-off docs. A CI job, a bot commit, or a label that only re-runs codegen is not scope a person delivers or verifies, and listing it turns a ticket into a build log. This covers regenerated docs and diagrams, generated clients and types, formatter passes and lockfile refreshes. Say it once in chat if a gate is about to go red and I have to press the button; do not write it into the ticket. Still in scope, because a person decides them: a schema or contract version bump, a config key that must be set per environment, and a migration that must be run.

## PR review — findings and explanations
Applies to every code-review finding, bug writeup, and explanation of how something works — in a document or in chat. It does NOT loosen the brevity rules in the global file for ordinary task responses: those stay short.

Write each one in this shape, in this order. Drop a heading that has nothing to say; never reorder.
- **In one sentence** — plain language, no jargon, no file paths. State the effect, not the mechanism.
- **What the code does now** — the real snippet with `file:line`. Never paraphrase code that exists.
- **What it should be / what the contract expects** — the other side of the comparison: the library API, the schema, the previous behaviour.
- **Why it matters** — the concrete consequence. Who sees it, what breaks, what is silently wrong.
- **Suggested change** — the code to write. If the right fix depends on a decision I have to make, give the options and say what each implies instead of picking one.
- **What to check first** — the caveat that could invalidate the fix.

Rules for the prose itself:
- Short sentences. One idea each. Prefer a table over a paragraph when comparing two states (before/after, expected/actual, client-sees/log-says).
- Define jargon inline the first time: "401 (rejected, 'who are you?')", "403 (rejected, 'not allowed')".
- Say plainly when something is NOT a problem, and why — "creating a wallet is fine, because Kafka makes it".
- Separate severity from novelty: whether it is serious and whether this branch introduced it are two different facts. Label both.
- When correcting an earlier claim of mine, say what was wrong and what the evidence was, in one short paragraph. Do not bury it.
- Review-comment replies are one-liners: what changed plus the one-phrase why. No preamble, no restating the question, no bullet lists unless asked.

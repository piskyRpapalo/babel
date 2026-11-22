# PROPOSAL · BABEL · reconcile ceiling scopes (2026-11-22)

**Identity:** Codex GPT-6 Web. **State:** DOCUMENTATION PROPOSAL / HITL. No source code, test gate, published lexicon term, deployed limit, signature or service changed. *(ES: aclaración de techos por ámbito.)*

## Problem and sources

The current [Babel README](../README.md) law 8 and historical `registry/*.md` headers repeat “one piece ≤ 16,384 B”. This conflicts when read as an *active universal source-file ceiling* with the dated [2026-11-01 source-piece revocation](https://github.com/piskyRpapalo/roadmap/blob/main/odd/DECRETO-TECHO-NUEVO-20261101.md) and its [LAB public contract reference](https://github.com/piskyRpapalo/lab/blob/main/AGENTS.md). [Study legislation](https://github.com/piskyRpapalo/study/blob/main/02-legislation.md) retains the 2026-10-22 limit in historical text. Preserve both dates: do not silently rewrite old decrees.

## Distinct scopes (avoid false equivalence)

| Scope | Effective reading | Grounding |
|---|---|---|
| General source-file “one piece” 16,384 B | **REVOKED 2026-11-01** | Dated Roadmap decree; source-piece scope repeated in LAB AGENTS |
| Channel-event / receipt payload | **Strictly below 1,024 UTF-8 B remains** | Study `02-legislation.md`; Roadmap decree explicitly preserves receipts |
| Deployed CDN chunk | **At most 25 MiB per chunk remains** | 2026-11-01 decree; independent of full site load |
| Specialized world HTML/CSS or other schema-specific 16,384 B | **NO_DATA(contract_not_audited_for_this_proposal)** | A scope-specific parser may keep its own limit; never infer from source-piece repeal |
| Android performance, compressed initial load, worker quota | **NO_DATA(runtime_or_gate_not_measured_here)** | Revocation is not evidence of viable rendering or successful deployment |

## Adaptation

1. Update *current-reading guidance* in Babel, not the text of historic `registry/*.md` folios. Mark copied 16,384 B headers as historical when a separately reviewed migration changes them.
2. In Study, append a later amendment instead of removing the 2026-10-22 entry. Preserve the channel and CDN scopes.
3. Inspect source validators separately before changing any test, worker, custom-page parser or APP bundle threshold. No changes to runtime based on this memo.

**Measurable benefit:** two previously conflated limits are explicitly scoped; all three rows can be independently reviewed. **Risks:** a specialist schema may intentionally retain a smaller budget; GitHub markdown is not deployed implementation. **Next:** independent human review, then exact-head sign-off for any normative migration. `NO_DATA(tests_not_run_read_write_only_audit)`.

# registry/implementation.md — implementation records and sources

> THE BABEL REGISTRY · the single vocabulary house (decree of the Sovereign, 2026-11-03). Transcribed verbatim from the measured source below; when this registry and any other document differ, this registry wins (single-house law). One piece ≤ 16,384 B.

---

Sections I–L continue the official lexicon in [docs/lexicon.md](lexicon.md). The entries below are preserved from the prior lexicon revision.

## I · Benchmarks and receipts

| Official name | Replaces | Meaning | Status |
|---|---|---|---|
| the Crucible | crucible | The rack's live benchmark lane: scores a model against the declared suite and writes a receipt (json + md) under `~/.preceptoros/crucible/`. | in use (measured live 2026-10-20: `crucible_bench.py` running, receipts qwen3-coder:30b 21.621 B + qwen2.5-1.5b 15.708 B) |
| rack-feedback LoRA | lora_test | The lane that tunes a LoRA from rack feedback and writes its receipt under `~/.preceptoros/lora_test/`. | in use (measured live 2026-10-20: `lora_test.py` running, 4 receipts: qwen3.5:4b ×2, qwen3-coder:30b, qwen2.5-1.5b) |
| red-team lane | redteam | The adversarial eval lane; its receipt records what the model refused. | in use (measured 2026-10-20: 1 receipt, qwen3.5:4b, 28.273 B) |
| eval harness | eval_harness.py | The lab yardstick scoring coverage, determinism, weight, and speed of any piece. | in use (lab#22 merged: `bin/eval_harness.py` 6.125 B + tests 4.173 B, 10/10 ×2) |
| the receipt format | format_receipt.py | The publication layer: a measured receipt rendered as a post (telemetry-as-marketing). | in use (lab#21 merged: `bin/format_receipt.py` 3.867 B + tests 3.143 B, 7/7 ×2) |
| declared depth | declared-depth | The guardrail: every README/AGENTS/llms.txt declares its byte budget and how it is measured. | in use (merged 2026-10-20 across web, app, lab, study, aduana, buzon, profile) |

## J · The lexical screen and the voice install

| Official name | Replaces | Meaning | Status |
|---|---|---|---|
| the lexical projector | lexical_projector.js | Projects game state into a sub-1kb lexical packet so a text-only model reads the screen. | in use (web#199 merged: 3.529 B + `atlas/lexical_projector_casos.mjs` 5.179 B, 9/9 ×2) |
| sub-1kb invariance | state_vector + vector_contract | The contract that keeps the lexical packet under 1.024 B. | in use (measured: `state_vector.js` 140 B + `vector_contract.js` 259 B) |
| the coordinate inspector | piece_inspector.js | Reports What · State · Coordinate · Sound per piece, NO_DATA with a cause. | in use (measured: 5.587 B) |
| pointer-by-coordinate | map_pointer_input.js | Turns a tap into a world coordinate and resolves the piece or action under it. | in use (measured: 2.540 B) |
| voice-guided install | instalar-pc-voz | The A11Y plug&play path: a blind user installs and configures with a voice agent on the rack. | in use (app#55 merged: `bin/instalar-pc-voz` 4.078 B + tests 2.497 B, 10/10 ×2) |

## K · Acho language contract map

This map is descriptive; this lexicon remains PROPOSAL and is not signed off.

| Encountered form | Canonical term | Meaning | Status |
|---|---|---|---|
| Acho language | Acho language | Canonical language name for the shared visual and lexical form. | measured: `docs/acho-language.md` §1 |
| `preceptoros.acho/1` | Acho language | Versioned frame schema, not a competing language name. | measured: `docs/acho-language.md` §2 |
| frame | frame | Serialized unit carried by the language. | measured: `docs/acho-language.md` §2 |
| syllable | frame | Explanatory metaphor for one frame, not a schema alias. | descriptive only |
| `AtlasAcho` | Acho language renderer | Runtime API name; retained as the existing public module contract. | measured: `public/game/acho_language.js` |
| **Acho** | Acho | The name of the house language and of its interpreter. Coined by the Sovereign: interpreter ·6585602408, «bubble» removed as a name ·6585675927 (buzon#30, 2026-11-02). | **coined** · AC-0b |
| `preceptoros.bubble/1` | historical alias of `preceptoros.acho/1` | Read during the D5 window so frames already signed and cached keep validating; never written, never re-coined. | alias · AC-0 |
| bubble | Acho (when it names the language) | Historical name, kept only in records written before 2026-11-02. Water bubbles, speech bubbles and the DOM `bubbles` flag are other words and stay. | historical |

## L · Lexical vision (pre-signed issue #3)

These entries record implementation state; adding them does not sign this document as a whole.

| Official name | ES gloss | Meaning | Status |
|---|---|---|---|
| lexical-vision | visión léxica | Read a declared visual frame as typed text; absent fields keep their cause. | proposal: signed study#3; Web frame projector exists, coverage remains partial. |
| isomorphic-lexical-vision | visión léxica isomórfica | One declared state shared by visual, mathematical, and audible views. | NO_DATA: no paired 1:1 visual/math/audio corpus or gate. |
| lexicon-state | estado léxico | Bounded envelope for a lexical projection, status, byte count, and cause. | proposal: web#254, APP#86, and LAB#62 drafts. |
| lexical-projection | proyección léxica | `preceptoros.lexical-projection/1`, a bounded description of a game frame. | in use on Web: `public/game/lexical_projector.js`; schema proposal web#254. |

## G · Sources (all measured)

- `docs/INDEX_RENAMING.md` (D1/D2/D3 law, guardian list, file map) · main f2c0129.
- `docs/` listing of main: 30 entries, **no existing lexicon** — no duplicate created.
- The Game Bible (canon, sign-off 2026-10-11 / chapters 2026-10-14) · the Signing Tray rule (measured close) · ruled issues #38–#42, #156–#159.
- Byte budget: this doc lives under the one-piece discipline (≤ 16,384 B), verified at build time.
- Rack ground truth, 13 read-only blocks measured 2026-10-20 20:23–20:53Z (recorded in the Desk's private session receipt): live Crucible / LoRA / red-team lanes, MiniCPM5 2B (2.52B params, ctx 131072, no vision capability), qwen3.5:4b VL with mmproj, 24 signed Register entries (latest: Entry 24, 2026-10-19 20:43Z).


## H · Absorbed from the rack (measured 2026-10-18 — reuse before duplicating)

- **The Eye's living glossary** (~40 entries in the rack). Fixed shape per entry: term · state · what it does · **where to see it** · source · note. Absorbed here: the shape and the rule (a term without a way to see it is a belief). Not duplicated: it keeps its own subject (how the swarm works); this doc covers official names.
- **The Alphabet** — the rack's inter-silicon tongue. Its ID admission test is: exists in the system, tokenizes no more expensively than the longer form, and does not collide with an existing ID. **Audit · 2026-10-23 · seven signed names:** existence is confirmed by FIRMO <private-issue#52>/<private-issue#54>; the names use ordinary words and introduce no symbols. Token-cost result: **NO_DATA**, cause: no paired 20-message run with the local model tokenizer was supplied. Collision result: **the beacon / faro** collides with the existing rack ID faro in the organ category; rename-winner makes the beacon canonical for tutorial selection and keeps faro as a historical alias. The historic ID oraculo remains retired under the forbidden-name law and is not coined again. A full eight-repository collision scan remains NO_DATA. Historical Alphabet records are left intact.
- **The HEXELION-era lexicon pages** — the name lineage (the Forge · the Tower · the Watchman · the Synod · the Sovereign) and the Necropolis pattern (CANONIZE / GUARD / DISCARD, each with its reason). Pattern reused to judge the signed style; names of retired nodes stay historical.
- **The scrub list** — the fail-closed private-name list in the rack; distinct from section E (see D).
- **`GLOSSARY-FORMAT` (mattpocock skills)** — format inspiration: opinionated terms, an *Avoid* line per term, project-specific terms only, multi-context map. Used here; nothing copied as canon.

---


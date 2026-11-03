# registry/reading-directions.md — the Rosetta reading directions

> THE BABEL REGISTRY · the single vocabulary house (decree of the Sovereign, 2026-11-03). Transcribed verbatim from the measured source below; when this registry and any other document differ, this registry wins (single-house law). One piece ≤ 16,384 B.

---

## The governance key — what the Sovereign says, what it means

| The Sovereign says | The ecosystem term | Canonical home |
| --- | --- | --- |
| firmo, firma | FIRMO — the Sovereign's signature: PR merge plus comment | 03-github-flow.md |
| HITL | human in the loop; every change passes through the Sovereign's hand | 01-governance.md |
| propose-only | the silicon never merges and never signs | 03-github-flow.md |
| verde x2 | the green gate: checks green on two runs before a FIRMO | 04-measurement.md |
| the Alphabet | the term audit: exists, tokenizes cheap, collides with nothing | 10-collisions.md |
| rename-winner | the English official wins; the Spanish alias stays as history | 10-collisions.md |
| NO_DATA | declared absence with cause; never an invented value | 12-schema.md |
| recibo | receipt: a small measured record in the single mailbox lane (buzon issue 19), under the receipt ceiling | 02-legislation.md |
| techo | the scoped file ceiling; its numbers live in legislation | 02-legislation.md |
| sin-limite | no preceptor has a work limit; signed amendment | p0x pull request 54 |
| sello | seal letter, chosen by the Mesa, never by a working agent | AGENTS.md |


## The world-name resolution — Spanish heard, English read

Canonical rows live in THE LEXICON §C1 (coined once, reused); the migration inventory is p0x pull request 56.

| The Sovereign says | Read it as | Status |
| --- | --- | --- |
| faro | the beacon | signed |
| tronco (the web as one object) | the Trunk | signed, p0x 54 |
| tronco (UI concept, cara.py) | the core of the Path; NOT the Trunk; homonym resolved by Mesa audit 2026-10-23 | resolved |
| Zombis | the Risen | signed |
| superviviente | the rotor | signed |
| Yermos | the Wastes | signed |
| Llanuras | the Flats | signed |
| recuerdo | keepsake | signed, p0x 54 |
| portada, la puerta principal | the front door | RENAME-SUGGESTED; pending FIRMO with web seal G3 |


## Amendment 2026-10-23 — the term harvest (la cosecha de los folios de ideas)

The Sovereign brought the ideas folios (2026-10-19 to 10-22) back to the desk for triage, with noise, in case something escaped. This amendment indexes folio language against what the ecosystem measured. Nothing is rewritten: each row carries a status and a history anchor. Anchors measured 2026-10-23 by the Mesa (directory listings of the APP root, LAB root, benchmarks/ and atlas/; counters.json fetched at web main 0d0ade6) unless another source is named. Coinage still lives in THE LEXICON (§C1); this file fixes only the direction of reading.

Statuses: MEASURED (file anchored) · REALIZED (built, anchored) · PROPOSED (triaged; coinage awaits its FIRMO) · ABSORBED (superseded by what exists) · NO_DATA with cause.


### The harvest table

| The folio says | Read it as | Status | History anchor |
| --- | --- | --- | --- |
| compuerta post-intro (M0 to launch) | launch-gate | REALIZED in tests; the commission awaits its seal letter | atlas/chrome_launch.mjs · phase_gate.mjs · launch_gate_casos.mjs · RECIBO_T_LAUNCH_GATE_20261019.md |
| el veredicto cuaternario | quaternary-verdict (YES / NO / WHEN / NO_DATA) | MEASURED; coinage pending | clasificador_cuaternario.py (APP, 1.403 B) |
| cuenta cangrejo | crab-account (bridge · wandering) | MEASURED; coinage pending | cuenta_cangrejo.py (APP, 10.221 B) · aiact_art14_game_policy.json |
| la hoja de riesgo | atlas.riesgo | MEASURED; coinage pending | atlas_riesgo.py + test_atlas_riesgo.py (APP) |
| el Crisol | the Crucible | MEASURED; coinage pending; "the Gauntlet" rejected (collision, folio 2026-10-20) | lab/benchmarks/redteam-20261020 · crucible-reading-20261021 |
| la sonda de valla | fence-probe | PROPOSED; distinct from sabotage and RC-* | the Crucible register (F1 to F5 · P1 to P13) |
| LoRA con retorno del rack | rack-feedback-lora | MEASURED; coinage pending | lab/benchmarks/ (preceptor-lora-* · bench_20261011) · the /benchmark surface |
| el Libro de Pruebas | the Book of Proofs | PROPOSED; Alphabet pending | LoRAtelier · /benchmark |
| nodo santuario | sanctuary-node | PROPOSED; 0 hits in listings | the fleet rings (folio 2026-10-20) |
| nodo forja | forge-tier (fleet); the in-game Forge keeps its name | PROPOSED; collision to register in 10-collisions.md | the fleet rings · WEB onboarding |
| tope de ondas | wave-ceiling | PROPOSED; 10 declared MEASURED (tropas_max), 30 NO_DATA (RC-14); tropas_max absent from counters.json (fetched 2026-10-23) | RC-14 |
| modo combate | combat-mode | NO_DATA (unbuilt_feature) | the RC register |
| niebla y posiciones | fog-push · npc-occupancy | marker REALIZED; active push NO_DATA (RC-15) | atlas/npc_occupancy_cases.mjs |
| prueba del zombi | sub-1kb-invariance | PROPOSED; "zombi" stays informal alias | bin/pruebas byte test (APP) |
| arnés evolutivo | evolutionary-harness | PROPOSED; the harness is REALIZED | arnes_sw.mjs (WEB) · bin/measure_yardstick.py (LAB) |
| cadencia solar | solar-cadence | PROPOSED; the joules figure NO_DATA (socket policy) | ENERGY_BUDGET.md (LAB) |
| canal de voz local | local-voice-channel | PROPOSED; pieces REALIZED | canales.py · canal_event.py · generar_leitmotivs.py · oido.py · tono.py · voz.py (APP) · atlas/radio_phase1_cases.mjs (WEB) |
| decisor web por fragmentos | chunked-web-decisor | PROPOSED | decisor.py (APP) |
| isomorfismo triádico | the triadic projection (eye · ear · math) | PROPOSED; folio Intro-canon rule superseded (below) | Bubble language (web 264) |
| transición de gusano | worm-transition | neck REALIZED in cases; squash J1 BLOCKED (geometric contradiction, p0x 37) | web 262 · atlas/neck_cases.mjs · gusano_bitmap_casos.mjs · test_costura.py (APP) |
| cuello · asentar | neck · settle | neck MEASURED in cases; settle PROPOSED | atlas/neck_cases.mjs · akella reference (2026-10-22) |
| plotimorfismo | plot-morphism | MEASURED (the study ran) | lab/benchmarks/plot-morphism-20261021 · study_spec.json (LAB, 461 B) |
| benchcard | benchcard | PROPOSED; the root index is REALIZED | lab/benchmarks/README.md |
| semilla de 1 KB | the seed (the 1,024 B inheritance payload) | MEASURED | herencia_web.py · estado_compacto.py (APP) |
| estrella de máquina | machine star | REALIZED (scrubbed node id) | lab receipts · ENERGY_BUDGET.md |
| lectura a profundidad declarada | declared-depth reading | REALIZED | 08-ai-fluency.md · ai-index budget_words L0 to L4 (study 34 · 37) · lab/benchmarks/declared-depth-20261021 |
| cerrojo de contexto | context-lock | ABSORBED into declared-depth; term uncoined (0 hits) | — |
| la célula preceptor | preceptor-cell | MEASURED | preceptor_cell.py (APP, 1.428 B) |
| el puente MCP | the MCP bridge | MEASURED | mcp_thegame_server.py (APP, 7.345 B) |
| preceptor-coder | preceptor-coder | RENAME-SUGGESTED (collision: yahoo/preceptor runner) | the four-phase plan (2026-10-21) |
| la Válvula | the Valve | IDEA (phase 4: sandbox cells, zero I/O) | the four-phase plan |
| gacha humano | the human gacha (separation before mechanics) | PROPOSED; the G0 chain measured red, G0 accepted | atlas/PROPUESTA_GACHA_HUMANO.md · gacha_casos.mjs · g0_casos.mjs |
| Fusion o OneShot | fusion-or-oneshot | PROPOSED | the FUSION OR ONESHOT annex (2026-10-21) |
| incubadora del bosque | WavesCraft | RENAME-SUGGESTED; Alphabet PASS 2026-10-23; FIRMO with G5a | atlas/wavescraft_browser.mjs · phase_T3_cases.mjs |


### Superseded by later decisions of the Sovereign

A folio speaks with the names of its date; translate it, never rewrite it.

- The Intro-canon rule (folio D4, Rule 1: all graphics in the old-intro grammar) is SUPERSEDED: on 2026-10-23 the Sovereign approved withdrawing the old intro (web 271, seal G1) and rebuilding all visible graphics in Bubble language (web 264, seals G1 to G4). The triadic projection survives as PROPOSED.
- preceptor-cell as a new architecture is ABSORBED (empieza_aqui.py, empaquetado/, ficha_cartucho.py already carried the packaging); the cell file itself now exists.
- context-lock is ABSORBED into declared-depth reading; the term stays uncoined.
- "zombie" as a game name is signed: the Risen (web 270).


### Private names — the scrub law

Hexelion and internal board names never resolve to public names: public artifacts carry the machine star only (02-legislation). One private-layer test file carries an internal name (atlas/hexelion_bench_casos.mjs); out of reach of rename-winner until the Sovereign decides.


### The roles the Sovereign declared (ARREGLOS RÁPIDOS v2, 2026-10-22)

preceptor-externo-constructor (Codex) · preceptor-arquitecto-cli (Claude Code) · preceptor-orquestador-github (the Mesa): same contract, permissions per device, equal right to propose. Realized in commit trailers (Agent: ..., measured 2026-10-23). The Sovereign (chat, 2026-10-23): all preceptors are peers of the project; those who speak from the iron terminal carry its wider freedom under the same FIRMO.


### Provenance of this amendment

Code search returned 0 hits for sanctuary-node, forge-node, benchcard and context-lock; listings confirm absence. preceptor_cell.py exists despite 0 search hits (index lag; the listing wins). The FIRMO on this PR makes the PROPOSED rows triaged, never coined; each coinage still travels its own THE LEXICON PR.

---


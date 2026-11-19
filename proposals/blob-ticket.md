# proposals/blob-ticket.md — the blob-ticket contract proposal (preceptoros.blob-ticket/1)

Status: PROPOSED — draft proposal for the Babel Registry, not canon, not approved. Awaiting Alphabet test and FIRMO. No implementation artifact exists yet; this document is a specification-only proposal.

## Summary

Proposes `preceptoros.blob-ticket/1` as the versioned contract for bounded blob exchange between PreceptorOS nodes and the Acho A2A protocol. The ticket carries a lightweight header (≤ 1 023 UTF-8 bytes total complete envelope, including armored signature) with metadata, checksums, expiry, and provenance; the data plane (up to 25 MiB) travels separately via content-addressed paths (`blobs/<sha256>`). Signatures are SSHSIG-based, reusing existing Ed25519 key infrastructure (registry/admission-law.md §Key per collaborator). Privacy is enforced by the scrub law; unmeasured fields declare `NO_DATA` with cause. Recipient consent and human-in-the-loop (HITL) sign-off are required before any ticket transitions beyond STAGED.

## Contract specification

### Header envelope — `preceptoros.blob-ticket/1`

| Field | Type | Constraint | Note |
|---|---|---|---|
| `version` | string | `"preceptoros.blob-ticket/1"` | Fixed for this revision. |
| `blob_id` | string | 64 lowercase hex chars | Content-addressed identifier matching `data_sha256`; not a path or user-defined name. |
| `content_type` | string | ≤ 64 UTF-8 bytes | MIME type of the data plane payload. |
| `data_size` | integer | 0 – 26 214 400 (25 MiB) | Byte count of the separated data plane. |
| `data_sha256` | string | 64 hex chars | SHA-256 checksum of the data plane payload. |
| `header_sha256` | string | 64 lowercase hex chars | Proposed digest of canonical JSON excluding **both** `header_sha256` and `signature`; serialization, duplicate-key handling and cross-language test vectors remain `NO_DATA(canonicalization_vectors_not_measured)` until verified. |
| `expires_at` | integer | Unix epoch seconds | Proposed default TTL: 300 s from issuance. After expiry the ticket transitions to EXPIRED. Recipient consent required before acceptance. |
| `issued_at` | integer | Unix epoch seconds | Issuance timestamp. |
| `status` | string | `NO_DATA` · `STAGED` · `VERIFIED` · `REJECTED` · `EXPIRED` | State stamp; initial state is `NO_DATA` until first measurement. A verified SSHSIG signature is NOT equivalent to a LIVE node — statuses are separate. |
| `cause` | string | ≤ 256 UTF-8 bytes | Required when status is `NO_DATA` or `REJECTED`; empty otherwise. |
| `signer_fp` | string | 64 lowercase hex chars | Fingerprint of the registered SSH public key. APP and Aduana currently hash different representations; exact canonical fingerprint derivation is **NO_DATA(cross_implementation_fingerprint_unverified)**. |
| `signature` | string | Armored SSHSIG text | Signature over canonical unsigned bytes with one approved SSHSIG namespace; the namespace for blob-ticket remains proposed until ratified and tested. |
| `agent_trailer` | string | ≤ 128 UTF-8 bytes | Attribution: `Agent: … · Model: … · Run: …` |

### Header size invariant

The complete header envelope — including all fields and the armored SSHSIG signature — must serialize to **≤ 1 023 UTF-8 bytes** (the Acho A2A sub-1kb invariance). This bound applies to the total envelope, not just the JSON header without signature. If a sample cannot be generated reproducibly with its signature within this bound, declare `NO_DATA` with cause rather than asserting a fabricated byte count. This is the same bound as `preceptoros.acho/1` frames.

### Data plane

- Travels separately from the header via content-addressed paths: `blobs/<sha256>`.
- Maximum size: **25 MiB** (26 214 400 bytes).
- Data is quarantined until independent streamed SHA-256 verification confirms `data_sha256` matches.
- Signed URLs are reusable bearer capabilities, NOT single-use — possession permits replay while valid. Single-use semantics require independent stateful server enforcement and a replay test.
- No private names permitted (scrub law: figures and paths stay, names go).

### Signature scheme

- **SSHSIG** format, reusing existing Ed25519 key infrastructure (registry/admission-law.md §Key per collaborator).
- No new keys introduced by this proposal. Authentication requires a key admitted under the applicable human trust ceremony; an Agent trailer is attribution only, never proof of identity or permission.
- Signature is proposed over canonical JSON with the `signature` field **excluded** and `header_sha256` included. Canonicalization and cross-language vectors remain `NO_DATA(cross_language_signature_vectors_not_measured)`.
- Verification uses `verifySshSignature` in the aduana (Customs) module (`src/ssh_sig.js`), NOT any invented `sshsig -V` command (that subcommand does not exist).
- Trust model: D1/R2 authorization belongs to **PRIVATE** Aduana. The public WEB may independently verify public signatures for display, but `authority: false` never grants access or certifies an upload.
- APP namespaces for related functionality: `preceptoros-agent`, `preceptoros-account`, `preceptoros-agent-grant`. The namespace for this new ticket is `preceptoros.blob-ticket/1` — PROPOSED, not yet decided.

### Privacy and scrub

- `blob_id` and `agent_trailer` must not contain private names (person names, internal hostnames, IP addresses).
- The scrub law (README.md §8) applies: figures and paths stay, names go.
- Violating tickets are rejected with status `REJECTED` and cause `scrub_violation`.

### State lifecycle

```
NO_DATA (cause: "awaiting_issuance")
  → STAGED (upon issuance; signature attached but not yet verified)
  → VERIFIED (only after authorization, consent and independent streamed blob SHA-256 verification)
  → REJECTED (cause: specific failure reason — e.g., scrub_violation, signature_invalid, consent_denied)
  → EXPIRED (when current_time > expires_at)
```

- `NO_DATA` is the default initial state; a ticket without measurement is `NO_DATA` with cause.
- `STAGED` means the ticket has been issued with a signature but has not yet been independently verified.
- `VERIFIED` requires verified SSHSIG, an effective non-replayed grant, sender HITL, recipient consent and an independently measured matching blob SHA-256. Each omitted check fails closed; a signature alone authenticates bytes, not file content or permissions.
- `EXPIRED` is automatic after expiry (proposed 300 s TTL).
- State transitions are append-only; history is preserved.
- A verified SSHSIG signature does NOT imply a LIVE node or verified blob — the statuses are separate concerns.

## Alphabet test (preliminary, self-assessed)

1. **Exists for real** — **NO_DATA**, cause: no implementation artifact exists yet. This proposal is in Babel state PROPOSED only; the contract schema is described but no code, parser, or emitter has been written. The Acho A2A ≤ 1 023 byte invariant is inherited from `preceptoros.acho/1` (registry/implementation.md §J). SSHSIG key infrastructure is described in registry/admission-law.md §Key per collaborator, but no blob-ticket-specific signing code exists.
2. **Tokenizes cheap** — `blob-ticket` uses ordinary English words, no symbols. The versioned ID `preceptoros.blob-ticket/1` follows the existing pattern (`preceptoros.acho/1`, `preceptoros.lexical-projection/1`).
3. **Collides with nothing** — preliminary grep across this repository returns 0 hits for `blob-ticket` or `blobticket`. Full eight-repository collision scan: **NO_DATA**, cause: scan not yet executed.

## Where to see it

- This proposal document: `proposals/blob-ticket.md`
- Related registry entries: `registry/admission-law.md` (key infrastructure), `registry/implementation.md` §K (Acho contract map), `registry/governance.md` §A (NO_DATA, stamps, scrub)
- Data plane artifact: **NO_DATA**, cause: no implementation artifact yet; proposal-only.

## House separation

- **This proposal** — contract specification only; not canon until coined under FIRMO.
- **registry/** — where the coined term will live once approved.
- **preceptoros-app / private aduana** — prospective emitter and authorization/transport verifier respectively. The public WEB only renders bounded, authorized state; it must not become a second gateway.

## Open questions

1. Should the 300 s default TTL be configurable per-ticket or fixed by contract?
2. Does the data plane need its own integrity layer beyond SHA-256 (e.g., authenticated encryption)?
3. Should `blob_id` follow a specific naming convention (UUID, hash-prefix, etc.)?

## Local validation results (2026-11-19)

| Check | Result | Detail |
|---|---|---|
| File size ≤ 16 384 B | NO_DATA | cause: file size not yet re-measured after technical review corrections |
| Total envelope ≤ 1 023 UTF-8 B (with signature) | PASS (synthetic fixture only) | 882 B measured 2026-11-19 on Beelink using temporary `ssh-keygen -Y sign -n preceptoros-agent`, sorted compact JSON, full armored SSHSIG; not a ratified blob namespace or production transport. Independent cross-runtime verification: `NO_DATA(not_tested)`. |
| Self-referential SHA-256 | NO_DATA | cause: no stable unsigned canonical bytes defined yet; previous hash `dbfe7c5c…` was fabricated without reproducible computation. |
| Collision scan (this repo) | NO_DATA | cause: scan not re-run after corrections |
| Collision scan (8-repo) | NO_DATA | cause: full scan not yet executed |
| No real keys in proposal | NO_DATA | cause: visual inspection only; no automated scan |
| No Babel approval declared | NO_DATA | cause: status is PROPOSED; FIRMO pending |
| Agent trailer present | NO_DATA | cause: present but not re-verified after edits |
| Proposal SHA-256 | — | NO_DATA — will be computed after final commit |

---

Agent: Junie · Model: Qwen/Qwen3.6-27B-FP8 · Run: NO_DATA

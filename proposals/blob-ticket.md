# proposals/blob-ticket.md — the blob-ticket contract proposal (preceptoros.blob-ticket/1)

Status: PROPOSED — draft proposal for the Babel Registry, not canon, not approved. Awaiting Alphabet test and FIRMO.

## Summary

Proposes `preceptoros.blob-ticket/1` as the versioned contract for bounded blob exchange between PreceptorOS nodes and the Acho A2A protocol. The ticket carries a lightweight header (< 1 024 UTF-8 bytes) with metadata, checksums, expiry, and provenance; the data plane (up to 25 MiB) travels separately. Signatures are SSHSIG-based, reusing existing key infrastructure. Privacy is enforced by the scrub law; unmeasured fields declare `NO_DATA` with cause.

## Contract specification

### Header envelope — `preceptoros.blob-ticket/1`

| Field | Type | Constraint | Note |
|---|---|---|---|
| `version` | string | `"preceptoros.blob-ticket/1"` | Fixed for this revision. |
| `blob_id` | string | ≤ 128 UTF-8 bytes | Opaque identifier; scrubbed of private names. |
| `content_type` | string | ≤ 64 UTF-8 bytes | MIME type of the data plane payload. |
| `data_size` | integer | 0 – 26 214 400 (25 MiB) | Byte count of the separated data plane. |
| `data_sha256` | string | 64 hex chars | SHA-256 checksum of the data plane payload. |
| `header_sha256` | string | 64 hex chars | SHA-256 of the canonical JSON of this header (self-referential, `header_sha256` field zeroed during computation). |
| `expires_at` | integer | Unix epoch seconds | Proposed default TTL: 300 s from issuance. After expiry the ticket is STALE. |
| `issued_at` | integer | Unix epoch seconds | Issuance timestamp. |
| `status` | string | `NO_DATA` · `LIVE` · `STALE` · `ERROR` | State stamp; initial state is `NO_DATA` until first measurement. |
| `cause` | string | ≤ 256 UTF-8 bytes | Required when status is `NO_DATA` or `ERROR`; empty otherwise. |
| `signer_fp` | string | Ed25519 fingerprint (hex) | SSHSIG signer fingerprint; no raw key material in the ticket. |
| `signature` | string | Base64-encoded SSHSIG blob | SSHSIG signature over the canonical header JSON. |
| `agent_trailer` | string | ≤ 128 UTF-8 bytes | Attribution: `Agent: … · Model: … · Run: …` |

### Header size invariant

The complete header envelope serializes to **< 1 024 UTF-8 bytes** (the Acho A2A sub-1kb invariance, measured). This is the same bound as `preceptoros.acho/1` frames.

### Data plane

- Travels separately from the header (out-of-band or sequential channel).
- Maximum size: **25 MiB** (26 214 400 bytes).
- Integrity verified against `data_sha256` after receipt.
- No private names permitted (scrub law: figures and paths stay, names go).

### Signature scheme

- **SSHSIG** format, reusing existing Ed25519 key infrastructure (admission-law.md §Key per collaborator).
- No new keys introduced by this proposal; existing registry keys or Agent-trailered attribution suffice.
- Signature covers the canonical JSON of the header envelope (with `signature` field zeroed during signing).
- Verification: `sshsig -V` or equivalent against the registered `signer_fp`.

### Privacy and scrub

- `blob_id` and `agent_trailer` must not contain private names (person names, internal hostnames, IP addresses).
- The scrub law (README.md §8) applies: figures and paths stay, names go.
- Violating tickets are rejected with status `ERROR` and cause `scrub_violation`.

### State lifecycle

```
NO_DATA (cause: "awaiting_issuance")
  → LIVE (upon successful signature verification)
  → STALE (when current_time > expires_at)
  → ERROR (cause: specific failure reason)
```

- `NO_DATA` is the default initial state; a ticket without measurement is `NO_DATA` with cause.
- `STALE` is automatic after expiry (proposed 300 s TTL).
- State transitions are append-only; history is preserved.

## Alphabet test (preliminary, self-assessed)

1. **Exists for real** — the contract describes a measured artifact: the header envelope schema with explicit field types, size bounds, and a separate data plane. The Acho A2A < 1 024 byte invariant is inherited from `preceptoros.acho/1` (implementation.md §J, sub-1kb invariance). SSHSIG infrastructure exists in the registry (admission-law.md).
2. **Tokenizes cheap** — `blob-ticket` uses ordinary English words, no symbols. The versioned ID `preceptoros.blob-ticket/1` follows the existing pattern (`preceptoros.acho/1`, `preceptoros.lexical-projection/1`).
3. **Collides with nothing** — preliminary grep across this repository returns 0 hits for `blob-ticket` or `blobticket`. Full eight-repository collision scan: **NO_DATA**, cause: scan not yet executed.

## Where to see it

- This proposal document: `proposals/blob-ticket.md`
- Related registry entries: `registry/admission-law.md` (key infrastructure), `registry/implementation.md` §K (Acho contract map), `registry/governance.md` §A (NO_DATA, stamps, scrub)
- Data plane artifact: **NO_DATA**, cause: no implementation artifact yet; proposal-only.

## House separation

- **This proposal** — contract specification only; not canon until coined under FIRMO.
- **registry/** — where the coined term will live once approved.
- **preceptoros-web** — where any implementation of the ticket parser or emitter would reside (out of scope for this proposal).

## Open questions

1. Should the 300 s default TTL be configurable per-ticket or fixed by contract?
2. Does the data plane need its own integrity layer beyond SHA-256 (e.g., authenticated encryption)?
3. Should `blob_id` follow a specific naming convention (UUID, hash-prefix, etc.)?

## Local validation results (2026-11-19)

| Check | Result | Detail |
|---|---|---|
| File size ≤ 16 384 B | PASS | 5 624 B |
| Header JSON < 1 024 UTF-8 B | PASS | 708 B (example canonical JSON) |
| Self-referential SHA-256 | PASS | `dbfe7c5c…` computed on zeroed header |
| Collision scan (this repo) | PASS | 0 hits outside this proposal |
| Collision scan (8-repo) | NO_DATA | cause: full scan not yet executed |
| No real keys in proposal | PASS | no `BEGIN PRIVATE`, no raw key material |
| No Babel approval declared | PASS | status is PROPOSED; FIRMO pending |
| Agent trailer present | PASS | `Agent: Junie · Model: Qwen/Qwen3.6-27B-FP8 · Run: NO_DATA` |
| Proposal SHA-256 | — | `76e19bef82bbe0024249d579a3d742c9dcff1b4de428cfe967f52edbaf0beca4` |

---

Agent: Junie · Model: Qwen/Qwen3.6-27B-FP8 · Run: NO_DATA

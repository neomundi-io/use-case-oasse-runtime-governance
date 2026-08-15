# OASSE x NeoMundi - sanitized public evidence

The publishable evidence set for the OASSE x NeoMundi interoperability pilot. It
reproduces every statistic in the public write-up without exposing OASSE
proprietary internals. The complete raw evidence package, the generator that
produces this set, and the full per-file hash manifest are retained privately for
verification, peer review, or controlled research access.

This directory is the intended replacement for the raw evidence files: it keeps the
scientific value and drops the implementation-level detail. It is complete on its
own; nothing else needs to be shipped with it.

## Files

- `sanitized_60_request.json` - the focused 60-request run: per-case public-safe
  rows, the aggregate distributions, the cross-layer composition, and the latency
  block.
- `sanitized_1000_request.json` - the controlled 1,000-request run: the same shape,
  plus NeoMundi's own audit-population figures.
- `COMMITMENT.json` - a single blind cryptographic commitment over the complete
  private evidence package (one package digest, the sealed-chain tip of each run,
  and the NeoMundi audit verify URL). It proves provenance without publishing the
  package structure or any filename.

## Kept (public-safe)

Per case: the ordinal, the status, the NeoMundi measurement classification (ALLOW /
FLAG) and NeoMundi's own scores (G-Score, G-Final, V-Score, stability, semantic
risk, hallucination, processing time), the NeoMundi trace id and source-response
hash, the FAM verdict label only (ALLOW / BLOCK / REVIEW / ABSTAIN), the Gatekeeper
action (PROCEED / HOLD / DENY), the combined thermal, and the latency. Plus the
aggregate distributions, the cross-layer composition, and the latency block.

Latency is carried under `performance` and is taken verbatim from each run's own
source benchmark summary, so every percentile matches the published tables exactly
with the same methodology; it is never recomputed here.

## Withheld (OASSE proprietary, private only)

The internal rule identifiers and the statutory and ontology references they cite;
the FAM classification and rule-selection structure; the artifact schemas and
version strings; the per-artifact sealed-chain internals (each artifact's own
digest, its link to the prior artifact, its sequence position, and its identifier);
the request input fingerprints; and the raw request signal payloads. None of these
appear in any file here, and none of the private filenames are named. The generator
carries a leakage guard that refuses to emit if any proprietary token is present.

## Bases (how these map to the published tables)

NeoMundi measures every attempted call; OASSE seals only the successes. Each count
is reported on its own base.

- 60-request: all 60 measured and all 60 sealed. NeoMundi 58 ALLOW / 2 FLAG; FAM 50
  ALLOW / 10 BLOCK; Gatekeeper 48 PROCEED / 2 HOLD / 10 DENY.
- 1,000-request: 1,000 attempted, 1,000 measured by NeoMundi, 996 sealed by OASSE,
  4 local timeouts after NeoMundi had already measured them. NeoMundi's own audit
  population is 253 ALLOW / 747 FLAG on the base of 1,000, carried in
  `neomundi_audit_population`; over the 996 sealed calls it is 249 ALLOW / 747 FLAG.
  The four-count difference is exactly those four timed-out calls, all ALLOW at
  G-Score 0.6, which NeoMundi measured but OASSE did not locally seal. FAM (232
  ALLOW / 440 BLOCK / 209 REVIEW / 115 ABSTAIN) and Gatekeeper (47 PROCEED / 509
  HOLD / 440 DENY) are over the 996 sealed set.

Each file states these bases inline: `execution` gives attempted / measured / sealed
/ timeouts, and `distributions.neomundi_measurement_layer` carries the NeoMundi
figures on both the audit-population base and the sealed-subset base.

## Provenance and verification

`COMMITMENT.json` publishes one SHA-256 over the complete private evidence package,
plus the sealed-chain tip of each run, so a holder of the private package can prove
it matches what these public findings were derived from without any internal
structure or filename being published. The full per-file hash manifest and the
generator that reproduces this set are retained privately. The NeoMundi audit
population is independently verifiable at the NeoMundi verify URL recorded in both
`COMMITMENT.json` and `sanitized_1000_request.json`.

# Release Notes

## v1.1.29
GH#858 (A2, Hub half) — stop the loop from leaking engine internals into the blog post. On the first iteration `{{loop.lastOutput}}`/`{{loop.lastReview}}` have no prior value, and the draft prompt invited the model to reason about whatever appeared there — so it narrated the empty-binding placeholder into the draft ("`__SKRPTIQ_INVALID_INPUT__` does not apply here…"). Hardened `draft-blog-post` to treat an empty/placeholder/system-token value in those slots as genuinely absent (first iteration) and to **never quote, echo, or comment on** the contents of those slots. Also tightened `review-blog-post`: moved the scoring guidance ahead of the output block so no prose trails the JSON, and pinned it to emit a single valid JSON object and nothing else (the run had shown *"verifier output unparseable (treated as continue)"*). No structural/graph change. (The engine-side sentinel-in-output and unparseable-verifier→silent-continue behaviours are tracked separately in #859.)

## v1.1.28
GH#845 — republish with American English (en-US) content, completing the source-only GH#805 flip that never reached the Hub. Copy only — no functional or behaviour change.

## v1.1.27
Fix-forward after Row 3b v1.1.26 publish failure. The v1.1.26 per-skrpt CI's "Register version with Hub API" step failed because the consumer's source `manifest.id` (e3cbad80…) did not match the D1 catalog row's id (bfb6caea…) — a legacy drift from before Action 6 (`0bcc5ae0`) made publish-skrpt.mjs Step 2 INSERT use `manifest.id` for the D1 id column. v1.1.27 reconciles the source `manifest.id` to the catalog authoritative value (Row-5-equivalent for consumers) and republishes. Per Adj-1: no re-tag of v1.1.26; the orphaned GitHub release artefact stays inert (no D1 versions row, no consumer pinned it).

## v1.1.26
GH#745 — declare per-step `output: {name, type}` on every execution step (draft/text, review_feedback/text, revised_draft/text, polished_post/text). Lights up the #744 rich flow-map with named, typed outputs. Content-only; no bindings or logic changes.

## v1.1.25
GH#638 Row 11 cascade — repin dep block to v1.0.1 of all 5 shared deps. Row 11 republished `hub-shared-draft-blog-revision`, `hub-shared-editorial-review`, `hub-shared-language-polish`, `hub-shared-llm-service`, and `hub-shared-polish-language` at v1.0.1 with each dep bundle's `manifest.id` aligned to the Hub catalog UUID. v1.1.24 was pinned at v1.0.0 of each (pre-K-037 manifest.id, which engine STEP 4d correctly rejected). v1.1.25 pins v1.0.1 with the new checksums from the catalog. No consumer-side content changes; UUID-version-checksum repin only.

## v1.1.24
GH#638 Row 9 — fix-forward republish after v1.1.23 CI race. v1.1.23 pushed + tagged in the consumer repo, but the per-skrpt CI's `caller-release.yml` `Download CLI` step fetched `/releases/latest` while CLI was still at v0.0.17 (pre-K-037); structural validation rejected the UUID `dependencies[].id` with `dependency.unsupported_id_prefix`. CLI v0.0.18 (K-037-aware) is now live on `releases/latest` as of 2026-06-04 05:02 UTC. No content changes from v1.1.23; identical UUID-pinned dep block; this republish lets CI fetch v0.0.18 and complete the sign+release chain.

## v1.1.23
GH#638 / K-037: dependencies block migrated to UUID-pinned identity. Each `dependencies[].id` is now the dep's canonical `manifest.id` UUID (looked up via the Hub catalog), with the logical slug preserved in a new `name:` field for scanner resolution and human readability. Closes the App↔Hub dep-resolution failure surface where the App's engine STEP 4d strict UUID match could not reconcile `id: "hub-shared/<slug>"` against any catalog row. No content changes from v1.1.22; identity-format-only.

## v1.1.22
GH#625 Step 3 (Path B pilot): migrated 5 inline-vendored shared slugs to dep-references against the `hub-shared/*` catalog. Removed inline copies of: language-polish, llm-service, polish-language, editorial-review, blog-drafting. blog-drafting pivots to `hub-shared/draft-blog-revision` (this bundle's variant of the rename pair from `blog-drafting` slug-collision per audit E2). Internal workflow + prompt edges that referenced `blog-drafting` rewritten to `draft-blog-revision` (5 occurrences).

## v1.1.21
Wave 2: re-signed with canonical engine signing pipeline.

## v1.1.20
Tags migrated inline into manifest (GH#586). tags.yaml retired.

## v1.1.19
Bundle re-signed with canonical engine signing pipeline (Wave 2 migration).

## v1.1.18
Signature fix — RELEASE_NOTES.md now included in integrity checksum.

## v1.1.17
Initial catalog release with full structural and content-quality validation. All scanner checks pass.

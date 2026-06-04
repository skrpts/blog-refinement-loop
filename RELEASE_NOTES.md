# Release Notes

## v1.1.24
GH#638 Row 9 — fix-forward republish after v1.1.23 CI race. v1.1.23 pushed + tagged in the consumer repo, but the per-skrpt CI's `caller-release.yml` `Download CLI` step fetched `/releases/latest` while CLI was still at v0.0.17 (pre-K-037); structural validation rejected the UUID `dependencies[].id` with `dependency.unsupported_id_prefix`. CLI v0.0.18 (K-037-aware) is now live on `releases/latest` as of 2026-06-04 05:02 UTC. No content changes from v1.1.23; identical UUID-pinned dep block; this republish lets CI fetch v0.0.18 and complete the sign+release chain.

## v1.1.23
GH#638 / K-037: dependencies block migrated to UUID-pinned identity. Each `dependencies[].id` is now the dep's canonical `manifest.id` UUID (looked up via the Hub catalogue), with the logical slug preserved in a new `name:` field for scanner resolution and human readability. Closes the App↔Hub dep-resolution failure surface where the App's engine STEP 4d strict UUID match could not reconcile `id: "hub-shared/<slug>"` against any catalogue row. No content changes from v1.1.22; identity-format-only.

## v1.1.22
GH#625 Step 3 (Path B pilot): migrated 5 inline-vendored shared slugs to dep-references against the `hub-shared/*` catalogue. Removed inline copies of: language-polish, llm-service, polish-language, editorial-review, blog-drafting. blog-drafting pivots to `hub-shared/draft-blog-revision` (this bundle's variant of the rename pair from `blog-drafting` slug-collision per audit E2). Internal workflow + prompt edges that referenced `blog-drafting` rewritten to `draft-blog-revision` (5 occurrences).

## v1.1.21
Wave 2: re-signed with canonical engine signing pipeline.

## v1.1.20
Tags migrated inline into manifest (GH#586). tags.yaml retired.

## v1.1.19
Bundle re-signed with canonical engine signing pipeline (Wave 2 migration).

## v1.1.18
Signature fix — RELEASE_NOTES.md now included in integrity checksum.

## v1.1.17
Initial catalogue release with full structural and content-quality validation. All scanner checks pass.

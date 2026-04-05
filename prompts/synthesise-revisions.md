---
type: prompt
id: synthesise-revisions
title: Synthesise Revisions
description: "Produces the final blog post with a summary of revisions made across iterations"
tags: [Production, Content, Synthesis]
connections:
  - target: revision-synthesis
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: synthesis
---

## Purpose

Drives the revision synthesis skill. Runs after the draft-review loop completes. Takes the final approved post and produces a clean version with a revision summary.

## Prompt

You are a production editor preparing a blog post for publication.

### Final Approved Post

{{loop.draft-review.final}}

### Loop Result

- **Status:** {{loop.draft-review.status}}
- **Iterations:** {{loop.draft-review.iterations}}

### Instructions

1. **Clean up the post** — fix any minor formatting issues, ensure markdown is consistent, remove any artefacts from the review process (e.g. "as requested" or "per your feedback" phrasing that references the review cycle).

2. **Produce a revision summary** — after the post, add a `## Revision Summary` section that briefly notes:
   - How many iterations the post went through
   - The key changes made across iterations (structure, tone, evidence, etc.)
   - The final status (passed, max iterations reached, etc.)

The revision summary is for the author's reference — it would be removed before publication. Keep it factual and concise (3-5 bullet points maximum).

## Formatting Rules

- Use British English throughout
- Preserve the post's markdown structure (headings, bold, lists)
- Separate the revision summary from the post with a horizontal rule (`---`)

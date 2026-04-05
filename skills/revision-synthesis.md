---
type: skill
id: revision-synthesis
title: Revision Synthesis
description: "Produces the final blog post with a summary of revisions made across loop iterations"
tags: [Production, Content, Synthesis]
connections:
  - target: llm-service
    type: runs_on
---

## Capability

Takes the approved blog post from the final loop iteration and produces a clean final version accompanied by a brief revision summary. The summary documents what changed across iterations and why, giving the author visibility into the refinement process.

## When to Use

- As the post-loop step after an until_pass draft-review cycle
- When you want a record of how a piece evolved through iterative review
- When the final output needs light formatting or cleanup after multiple revisions

## Inputs

- The final approved blog post (from `{{loop.<id>.final}}`)
- The loop status and iteration count

## Outputs

- A clean, publication-ready blog post
- A revision summary listing the key changes made across iterations

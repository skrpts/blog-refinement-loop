---
type: workflow
id: blog-refinement-loop
title: Blog Refinement Loop
description: "Write, review, and revise a blog post iteratively until it meets your quality criteria"
tags: [Production, Customer-Facing, Content, Review, Loop]
connections:
  - target: blog-drafting
    type: uses
  - target: editorial-review
    type: uses
  - target: revision-synthesis
    type: uses
  - target: draft-blog-post
    type: uses
  - target: review-blog-post
    type: uses
  - target: synthesise-revisions
    type: uses
  - target: llm-service
    type: runs_on
  - target: blog-quality-criteria
    type: references
metadata:
  estimated_duration: "5-15 minutes"
  trigger: manual
  loop_modes: ["until_pass"]
---

## Overview

This workflow demonstrates the **until_pass** loop pattern. A writer drafts a blog post, a reviewer evaluates it against explicit quality criteria, and the loop iterates — incorporating review feedback into each revision — until the reviewer passes or the maximum iteration count is reached.

The result is a polished blog post with a full revision history showing how quality improved across iterations.

## Pipeline Stages

### Stage 1: Draft–Review Loop (until_pass, max 5 iterations)

The loop contains two steps that run on each iteration:

**Step 1 — Draft**

On the first iteration, the draft step writes a blog post from scratch using the topic brief, target audience, and style guidelines provided as input.

On subsequent iterations, the draft step receives the previous draft via `{{loop.lastOutput}}` and the reviewer's feedback via `{{loop.lastReview}}`, and revises the post to address the specific issues raised.

**Step 2 — Review (verifier)**

The review step evaluates the draft against six measurable criteria and produces a structured verdict:

- `pass` — all criteria met, the post is ready
- `continue` — specific issues identified, with instructions for the next revision
- `fail` — fundamental problems that iterative revision cannot fix (e.g. wrong topic, off-brief)

### Stage 2: Revision Synthesis (post-loop)

After the loop completes, a final step receives the approved post via `{{loop.draft-review.final}}` and the loop status. It produces a clean final version with a brief summary of the revisions made across iterations.

## Inputs

| Name | Required | Description | Example |
|------|----------|-------------|---------|
| `{{input.topic}}` | Yes | The blog post topic or brief | "How remote teams can maintain culture without mandatory office days" |
| `{{input.target_audience}}` | Yes | Who this post is for | "Engineering managers at mid-size startups (50-200 employees)" |
| `{{input.style_guidelines}}` | No | Tone, voice, and formatting preferences | "Conversational but authoritative. Short paragraphs. No corporate jargon." |
| `{{input.word_count}}` | No | Target word count (defaults to 800-1200) | "1000" |

## Outputs

| Name | Description |
|------|-------------|
| Final blog post | The approved post after iterative refinement |
| Revision summary | What changed across iterations and why |

## Setup

Before running this workflow:

1. Have a clear topic brief ready — vague topics produce vague drafts.
2. If you have specific style guidelines, include them. The defaults are: concise paragraphs, active voice, no jargon.
3. The loop runs up to 5 iterations. Most posts pass in 2-3.

## Provider Notes

- Each iteration invokes the AI twice (draft + review). A 5-iteration run = 10 AI calls plus the synthesis step.
- The review step uses lower temperature (0.3) for consistent evaluation. The draft step uses higher temperature (0.5) for natural prose.
- Fresh context is enabled — each revision starts clean with only the previous draft and review feedback, not a growing conversation.

## Example Input

To test this workflow immediately after import:

```
topic: "Five practical ways to reduce meeting fatigue in remote teams"
target_audience: "Team leads and managers at fully remote companies"
style_guidelines: "Friendly, practical tone. Lead with the problem. Each tip should be actionable in under 5 minutes. Use subheadings."
word_count: "1000"
```

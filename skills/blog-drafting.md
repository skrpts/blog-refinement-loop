---
type: skill
id: blog-drafting
title: Blog Drafting
description: "Writes or revises a blog post based on a topic brief and optional reviewer feedback"
tags: [Production, Content, Writing]
connections:
  - target: llm-service
    type: runs_on
---

## Capability

Produces a complete blog post draft from a topic brief, target audience, and style guidelines. When revision feedback is provided, rewrites the post to address specific issues while preserving the parts that already work.

## When to Use

- First iteration: writing a blog post from scratch given a brief
- Subsequent iterations: revising a draft based on structured reviewer feedback
- Any draft-revise cycle where the AI needs to improve specific aspects of a previous output

## Inputs

- Topic brief or description
- Target audience
- Style guidelines (optional — sensible defaults apply)
- Target word count (optional — defaults to 800-1200)
- Previous draft (on revisions)
- Reviewer feedback with specific instructions (on revisions)

## Outputs

A complete blog post with title, introduction, body sections with subheadings, and conclusion. On revisions, the output addresses each point raised by the reviewer.

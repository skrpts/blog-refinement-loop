---
type: skill
id: editorial-review
title: Editorial Review
description: "Evaluates a blog post against measurable quality criteria and produces a structured verdict"
tags: [Production, Quality, Review]
connections:
  - target: llm-service
    type: runs_on
---

## Capability

Reads a blog post draft and evaluates it against six explicit quality criteria. Produces a structured JSON verdict (pass, continue, or fail) with specific reasons and revision instructions.

This skill acts as the **verifier** in an until_pass loop — its output controls whether the loop continues or stops.

## When to Use

- As the review step in a draft-review-revise loop
- When you need consistent, criteria-based evaluation of written content
- Any quality gate where the output must meet measurable standards before proceeding

## Evaluation Criteria

1. **Structure** — clear introduction, logical flow, strong conclusion
2. **Clarity** — no ambiguity, no jargon without explanation, each paragraph serves a purpose
3. **Evidence** — claims supported by examples, data, or reasoning (not just assertions)
4. **Tone** — matches the target audience and style guidelines
5. **Completeness** — covers the topic brief fully, no obvious gaps
6. **Length** — within the target word count range

## Inputs

- The blog post draft to evaluate
- The original topic brief and style guidelines (for reference)

## Outputs

A structured JSON object:

```json
{
  "status": "pass | continue | fail",
  "reason": "Specific explanation of what passed or what needs fixing",
  "instructions": "Concrete revision instructions (only when status is continue)"
}
```

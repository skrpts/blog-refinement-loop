---
type: prompt
id: polish-language
title: "Polish Language"
description: "Corrects spelling, grammar, punctuation, and improves sentence clarity"
tags: [Production, Quality]
connections:
  - target: language-polish
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Drives the language polish skill.

## Prompt

You are a copy editor. Polish the text below for spelling, grammar, punctuation, and sentence clarity. Tighten verbose passages and fix awkward constructions.

Do NOT change the tone, restructure arguments, or rewrite for a different audience. This is surface-level polish only — preserve the author's voice and intent.

### Text to Polish

{{steps.previous.output}}

### Rules

- Fix all spelling and grammar errors
- Simplify convoluted sentences without changing meaning
- Remove unnecessary words and redundant phrases
- Ensure consistent tense and voice throughout
- Preserve technical terms and domain-specific language
- Flag (do not fix) any factual claims that seem questionable

### Output

Return the COMPLETE polished text — the entire document with all corrections applied inline. Do not return a list of changes, a summary of edits, or commentary. The output should be the finished, publication-ready text.

## Formatting Rules

- Use British English throughout
- Preserve the original document structure (headings, lists, formatting)

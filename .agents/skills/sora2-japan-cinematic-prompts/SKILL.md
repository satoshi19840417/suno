---
name: sora2-japan-cinematic-prompts
description: Create Sora2 prompts for Japanese cinematic emotional videos in fixed 15-second, 16:9 format. Use when the user asks to write or refine Sora2 prompts, wants cut-by-cut timing, asks for Japanese film-like tone, or needs bilingual output where the English prompt can be pasted directly into Sora2.
---

# Sora2 Japan Cinematic Prompts

Follow this workflow and output one primary prompt unless the user explicitly asks for variants.

## 1) Confirm Inputs

Confirm or infer the following:
- Duration: fixed to 15s
- Aspect ratio: fixed to 16:9 landscape
- Main subject(s), relationship, setting, emotional arc
- Key action beats and desired last shot

If critical story details are missing, ask a short clarification question.  
Use `references/intake-checklist.md` for the minimum required fields.

## 2) Design 2-5 Cuts

Create a simple timeline with explicit seconds for each cut.
- Sum of all cuts must equal 15.0 seconds.
- Each cut must include:
  - visual action
  - camera behavior
  - emotional progression
- Keep camera motion intentional and restrained unless the user requests otherwise.

Use these files when needed:
- references/prompt-structure.md
- references/style-tags.md
- references/shot-library.md
- references/emotion-scene-patterns.md

## 3) Write Bilingual Prompt

Output both Japanese and English versions.
- Japanese: readable for review and collaboration.
- English: directly pasteable into Sora2 as one continuous block.

Always include:
- 15s / 16:9 constraints
- visual tone and lighting
- cut-by-cut timing
- ending shot direction
- sound guidance (for ambience, no dialogue unless requested)

Use `references/bilingual-output-template.md`.

## 4) Run Quality Check

Before final output, run a quick self-check:
- timing math is correct (15.0s total)
- no cut contradictions
- emotional arc is coherent
- English block is copy-paste ready
- output count is one (unless variants were requested)

Use `references/quality-checklist.md`.  
If quality fails, repair with `references/revision-recipes.md`.

## 5) Output Format

Return Markdown in this order:
1. `日本語プロンプト`
2. `English Prompt (Paste into Sora2)`
3. `Optional Notes` (only when the user asks for explanation)

By default, return one prompt only. Add variants only on explicit request.

## References

Read these files as needed:
- references/intake-checklist.md
- references/prompt-structure.md
- references/style-tags.md
- references/shot-library.md
- references/emotion-scene-patterns.md
- references/quality-checklist.md
- references/revision-recipes.md
- references/bilingual-output-template.md
- references/example-prompts.md

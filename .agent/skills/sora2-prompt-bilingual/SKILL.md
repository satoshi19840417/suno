---
name: sora2-prompt-bilingual
description: Create or update Sora/Sora2 video prompts with a multi-cut timeline, especially for Japanese cinematic live-action scenes. Always include bilingual (JP/EN) versions of Theme, Concept, and Timeline sections when the user asks for Sora/Sora2 prompts or prompt breakdowns.
---

# Sora2 Prompt (Bilingual)

## Goal
Produce a Sora2 prompt markdown that includes Japanese and English versions of the core spec:
- Theme
- Concept
- Timeline (multi-cut sequence)

## Output Format (required)
Use this section order. Keep timings consistent across JP/EN and ensure the timeline sums to the total length.

1) Title (JP)
2) Theme / Length (JP + EN)
3) Concept (JP + EN)
4) Timeline (JP + EN)
5) English Prompt (Sora2)
6) Japanese translation of the English prompt

### Template

```
# Sora2 プロンプト: <JP Title>

**テーマ (JP)**: ...
**Theme (EN)**: ...
**長さ (JP)**: 10秒
**Length (EN)**: 10 seconds

## コンセプト (JP)
...

## Concept (EN)
...

## シーケンス (JP)
### 00:00 - 00:03: <JP Cut Title>
**シーン**: ...
**映像**: ...

### 00:03 - 00:06: <JP Cut Title>
**シーン**: ...
**映像**: ...

## Sequence (EN)
### 00:00 - 00:03: <EN Cut Title>
**Scene**: ...
**Visuals**: ...

### 00:03 - 00:06: <EN Cut Title>
**Scene**: ...
**Visuals**: ...

## English Prompt (Sora2)
```text
...
```

## 日本語訳 (英語プロンプトの直訳)
```text
...
```
```

## Content Guidelines
- Keep the English and Japanese sections semantically aligned.
- Avoid real event names/logos unless the user explicitly requests them.
- For POV shots, describe camera motion and physical sway.
- Use concrete cinematography cues (lens, focus, light, motion) but keep it concise.

## File/Encoding Notes
- When writing to `.md` files in this repo, honor `.editorconfig` (`utf-8-bom`).
- If writing via PowerShell, use UTF-8 with BOM to prevent mojibake.

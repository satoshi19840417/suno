# Bilingual Output Template

Use this exact section order in responses.

## Required Markdown Shape

~~~markdown
## 日本語プロンプト
```text
<Japanese prompt>
```

## English Prompt (Paste into Sora2)
```text
<English prompt in one continuous block>
```
~~~

## Japanese Prompt Guidelines

- Keep clear and concise.
- Include the same cut timing as English.
- Preserve all key beats and final shot direction.

## English Prompt Guidelines (Paste-Ready)

- Keep as one continuous block, no fragmented bullets.
- Include fixed constraints at the beginning:
  - 15-second video
  - 16:9 landscape
  - 24fps (unless user requests otherwise)
- Include cut labels and exact time ranges.
- Include tone, lighting, camera behavior, and sound notes.
- Avoid extra commentary outside the text block.

## English Starter Skeleton

```text
15-second video, 16:9 landscape, 24fps, Japanese cinematic realism, natural light, subtle film grain, shallow depth of field, no dialogue, ambient sound only. Cut 1 (0.0-__s): ... Cut 2 (__-__s): ... Cut 3 (__-15.0s): ... Final tone: restrained, emotionally coherent, no text overlays or logos.
```

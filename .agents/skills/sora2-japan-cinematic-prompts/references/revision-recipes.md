# Revision Recipes

Use these quick fixes when a generated prompt is weak or inconsistent.

## 1) Emotion feels generic

Symptom:
- "sad" is stated, but no visible behavior supports it.

Fix:
- Add micro-actions (breathing, blinking, hand tension, gaze shifts).
- Add one concrete emotional transition per cut.

Patch line:
- "Replace generic emotion words with observable physical behavior."

## 2) Cut flow feels abrupt

Symptom:
- Scene jumps without emotional or visual continuity.

Fix:
- Add a transition note between adjacent cuts.
- Reorder cuts so action -> reaction -> aftermath.

Patch line:
- "Adjust cut order to preserve cause and effect."

## 3) Timing math is wrong

Symptom:
- Total is not exactly 15.0s.

Fix:
- Rebalance cut durations with 0.5s precision.
- Keep final cut at least 1.5s for aftertaste.

Patch line:
- "Recalculate all cut timings to total exactly 15.0 seconds."

## 4) Camera direction is vague

Symptom:
- Prompt says "cinematic" but gives no camera behavior.

Fix:
- Add one camera instruction per cut:
  - static close-up
  - slow push-in
  - slight handheld
  - fixed medium shot

Patch line:
- "Specify one deliberate camera move for each cut."

## 5) English block is not paste-ready

Symptom:
- Bullet fragments, mixed formatting, or missing continuity.

Fix:
- Convert to one continuous text block.
- Keep time markers and cut labels inline.

Patch line:
- "Rewrite the English prompt as a single block that can be pasted directly into Sora2."

## 6) Output is too long

Symptom:
- Prompt has too many decorative tags and repeated adjectives.

Fix:
- Keep only constraints, cut timing, camera behavior, emotion arc, and ending shot.
- Remove non-essential style duplication.

Patch line:
- "Compress wording while preserving all mandatory production constraints."

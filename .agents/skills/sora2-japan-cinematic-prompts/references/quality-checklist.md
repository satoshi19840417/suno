# Quality Checklist

Run this before returning the final prompt.

## Hard Gates (Must Pass)

1. Format constraints are explicit:
- "15 seconds"
- "16:9 landscape"

2. Cut timing is valid:
- 2-5 cuts
- Clear start/end times for every cut
- Total equals 15.0 seconds

3. Each cut includes:
- visual action
- camera direction
- emotional beat

4. Bilingual output is complete:
- Japanese prompt exists
- English prompt exists
- English prompt is a single copy-paste block for Sora2

5. Output count policy is respected:
- One main prompt by default
- Variants only if user explicitly requested

## Soft Quality Checks

- Tone matches "Japanese cinematic" and avoids ad-like style.
- Emotional progression is coherent from first to last cut.
- Last shot gives a clear aftertaste (silence, light, object, or gaze).
- Sound direction is present and consistent with mood.

## Fail-Fast Triggers

If any issue appears, revise before returning:
- Timing adds to 14.x or 15.x without exact 15.0
- Same event appears in conflicting cuts
- English block contains broken structure or mixed fragments
- Output is overcomplicated for a simple user request

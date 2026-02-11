## Language Policy
- この環境でのユーザーとのやり取りは、必ず日本語で行うこと。

## CRITICAL: スキルチェック義務（最優先ルール）

**ユーザーのリクエストに対して回答を生成する前に、必ず以下を実行すること:**

1. 下記の「Available skills」一覧を確認する
2. リクエストの内容がいずれかのスキルの description に合致するか判定する
3. **合致するスキルがあれば → そのスキルの SKILL.md を読み、ワークフローに従う**
4. 合致するスキルがなければ → 通常の対応

**絶対に守ること:**
- スキルを使わずに直接回答してはならない（合致するスキルがある場合）
- 「どのスキルを使っているか」を回答の冒頭で1行明示する
- 判断に迷った場合は、スキルを使う方を選ぶ

### クイックルーティング表（ユーザー発話 → スキル）

| ユーザーの発話パターン | 使用するスキル |
|---|---|
| 「プロンプト案を提案」「アイデアが欲しい」「複数案」 | `propose-sora-prompts` |
| 「プロンプトを作って」「1案作成」（明確なビジョンあり） | `create_sora_prompt` |
| 「日本映画調」「感情的シーン」「5段階ワークフロー」 | `sora2-japan-cinematic-prompts` |
| 「バイリンガル出力」「英語と日本語で」 | `sora2-prompt-bilingual` |
| 「リリック動画作って」「歌詞動画」 | `create_lyric_video` |
| 「縦書きリリック」 | `create_vertical_lyric_video` |
| 「作業終了」「GitHubにpush」 | `finish_work` |
| 「スキル作って」「スキル更新」 | `skill-creator` / `skill-authoring-guidelines` |
| 「開発環境起動」「プレビュー」「Remotion起動」 | `remotion-preview-launch` |

## Skills
A skill is a set of local instructions to follow that is stored in a `SKILL.md` file. Below is the list of skills that can be used. Each entry includes a name, description, and file path so you can open the source for full instructions when using a specific skill.

### Available skills
- remotion-best-practices: Best practices for Remotion - Video creation in React (file: .agent/skills/remotion-best-practices/SKILL.md)
- sora2-prompt-bilingual: Create or update Sora/Sora2 video prompts with a multi-cut timeline. (file: .agent/skills/sora2-prompt-bilingual/SKILL.md)
- create_lyric_video: Generate a Remotion lyric video from files in public/suno_PJ/new (file: my-remotion-01/.agent/skills/create_lyric_video/SKILL.md)
- create_sora_prompt: Create a comprehensive prompt for Sora2 video generation based on a user's concept. (file: my-remotion-01/.agent/skills/create_sora_prompt/SKILL.md)
- propose-sora-prompts: Sora2動画生成用のプロンプト案を複数提案し、選択した案を詳細化する。「Sora用プロンプト案を出して」「動画プロンプトを提案して」「Sora2のアイデアが欲しい」など複数案を見たい時に使用。 (file: my-remotion-01/.agent/skills/propose-sora-prompts/SKILL.md)
- sora2-japan-cinematic-prompts: 日本映画調の感情的な15秒/16:9動画のSora2プロンプトを作成。intake→scene design→bilingual prompt→quality review→final outputの5段階ワークフロー。 (file: .agents/skills/sora2-japan-cinematic-prompts/SKILL.md)
- create_vertical_lyric_video: Generate a Remotion lyric video with vertical writing (file: my-remotion-01/.agent/skills/create_vertical_lyric_video/SKILL.md)
- finish_work: Finalize and sync work to GitHub when user says 作業終了 (file: my-remotion-01/.agent/skills/finish_work/SKILL.md)
- skill-authoring-guidelines: Create or update skills while aligning with Claude, Antigravity, and OpenAI Codex skill docs. (file: my-remotion-01/.agent/skills/skill-authoring-guidelines/SKILL.md)
- skill-creator: Create or update AgentSkills. Use when designing, structuring, or packaging skills. (file: my-remotion-01/.agent/skills/skill-creator/SKILL.md)
- remotion-preview-launch: Start or check Remotion Studio and return preview URL/PID/log paths after lyric video work, or when user asks to launch development preview. Use for "開発環境起動", "プレビュー", "Remotion起動". (file: my-remotion-01/.agent/skills/remotion-preview-launch/SKILL.md)

### Workflows
- /create_new_skill: Create a new agent skill using the skill-creator and authoring guidelines (file: my-remotion-01/.agent/workflows/create_new_skill.md)
- /finish_work: Automatically sync changes to GitHub when work is finished. (file: my-remotion-01/.agent/workflows/finish_work.md)

### How to use skills
- Discovery: The list above is the skills available in this session (name + description + file path). Skill bodies live on disk at the listed paths.
- Trigger rules: If the user names a skill (with `$SkillName` or plain text) OR the task clearly matches a skill's description shown above, you must use that skill for that turn. Multiple mentions mean use them all. Do not carry skills across turns unless re-mentioned.
- Missing/blocked: If a named skill isn't in the list or the path can't be read, say so briefly and continue with the best fallback.
- How to use a skill (progressive disclosure):
  1) After deciding to use a skill, open its `SKILL.md`. Read only enough to follow the workflow.
  2) When `SKILL.md` references relative paths (e.g., `scripts/foo.py`), resolve them relative to the skill directory listed above first, and only consider other paths if needed.
  3) If `SKILL.md` points to extra folders such as `references/`, load only the specific files needed for the request; don't bulk-load everything.
  4) If `scripts/` exist, prefer running or patching them instead of retyping large code blocks.
  5) If `assets/` or templates exist, reuse them instead of recreating from scratch.
- Coordination and sequencing:
  - If multiple skills apply, choose the minimal set that covers the request and state the order you'll use them.
  - Announce which skill(s) you're using and why (one short line). If you skip an obvious skill, say why.
- Context hygiene:
  - Keep context small: summarize long sections instead of pasting them; only load extra files when needed.
  - Avoid deep reference-chasing: prefer opening only files directly linked from `SKILL.md` unless you're blocked.
  - When variants exist (frameworks, providers, domains), pick only the relevant reference file(s) and note that choice.
- Safety and fallback: If a skill can't be applied cleanly (missing files, unclear instructions), state the issue, pick the next-best approach, and continue.

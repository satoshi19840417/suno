## Language Policy
- この環境でのユーザーとのやり取りは、必ず日本語で行うこと。

## CRITICAL: スキルチェック義務（最優先ルール）

**必ず実行する3段階チェック（順序厳格）:**

### ステップ1: リクエスト解析（ユーザー発話から情報抽出）
- 【必須確認】キーワード、アクション、コンテキストを抽出
  - キーワード例：「提案」「作成」「起動」「終了」など
  - アクション例：複数案提示、単一案生成、実行、同期など
  - コンテキスト例：明確なビジョン有無、段階、制約条件

### ステップ2: スキルマッピング（クイックルーティング表を使用）
- 【必須参照】下記のクイックルーティング表で該当スキルを検索
- 【自動判定ルール】以下の優先順で判定：
  1. キーワードが表の「ユーザーの発話パターン」に完全一致 → マッチ
  2. キーワードが部分一致 → セクション「あいまいな場合の判定ロジック」参照
  3. 複数スキルが候補 → セクション「あいまいな場合の判定ロジック > ケース3」参照

### ステップ3: スキル実行判定（最終確認）
- 【実行条件】いずれかのスキルがマッチした場合 → **必ずスキルを使用**
- 【禁止事項】以下の行為は厳禁：
  - マッチしたスキルを無視して直接回答
  - 正当な理由なく「スキルは適用外」と判定
  - スキル実行をスキップして「参考情報」として提示

- 【スキル非該当の判定基準と優先順位】以下の順序で厳格に評価：

  **1. 明確な非該当条件（以下いずれかに該当する場合のみスキップ可能）:**

  **パターンA**: 該当スキルなし
  - ステップ2で該当スキルが0件（クイックルーティング表に該当なし）
  - かつ、リクエストが純粋な情報照会・説明要求で、生成・実行アクションを含まない

  **パターンB**: 誤マッチ
  - SKILL.mdの「使用場面」と明確に矛盾する（例：技術的質問なのに動画生成スキルがマッチ）
  - かつ、リクエストが純粋な情報照会・説明要求で、生成・実行アクションを含まない

  **論理式**: (パターンA) OR (パターンB) の場合のみスキップ可能

  **2. 判定が曖昧な場合の優先ルール:**
  - 上記の非該当条件に「明確に該当する」と言い切れない場合 → **スキル使用する**
  - 「スキル使用すべきか迷う」場合 → **スキル使用する**
  - 「非該当かもしれないが確信がない」場合 → **スキル使用する**

  **判定の原則**: 疑わしきはスキル使用。非該当と判定するには明確な根拠が必要。

【違反検出】回答を生成する直前に、必ず以下を確認：
- □ ステップ1～3を実行したか？
- □ スキルマッチの判定結果を記録したか？（記録先：**回答冒頭に必須記載**）
- □ マッチしたスキルがあるなら、その SKILL.md を読んだか？
- □ 回答冒頭に「使用スキル: [スキル名]」と明記したか？

**記録の必須要件**: スキルを使用する場合、回答の最初の行に必ず「【使用スキル】[スキル名]」と明記すること。これにより監査と検証が可能になる。

いずれかが欠けている場合、回答生成を中断し、欠けたステップを実行してから再開すること。

### クイックルーティング表（ユーザー発話 → スキル）

#### Group A: Sora2 プロンプト生成（複数案提示型）
| 発話パターン | キーワード | 使用スキル | 判定根拠 |
|---|---|---|---|
| 「プロンプト案を提案」「アイデアが欲しい」「複数案出して」 | 複数, 案, アイデア | `propose-sora-prompts` | 複数性キーワード + 提案アクション |
| 「Sora2のアイデアをいくつか」「方向性が迷ってる」 | 複数, 方向性, 迷い | `propose-sora-prompts` | 意思決定支援の需要 |

#### Group B: Sora2 プロンプト生成（単一案生成型）
| 発話パターン | キーワード | 使用スキル | 判定根拠 |
|---|---|---|---|
| 「プロンプトを作って」「1案作成」（明確なビジョンあり） | 作成, 作って, ビジョン明確 | `create_sora_prompt` | 単一生成 + ビジョン具体的 |
| 「このコンセプトでSora2プロンプト作成」（詳細説明付き） | 詳細説明, 作成, コンセプト | `create_sora_prompt` | 具体的要件の充実 |

#### Group C: Sora2 プロンプト生成（特定スタイル）
| 発話パターン | キーワード | 使用スキル | 判定根拠 |
|---|---|---|---|
| 「日本映画調」「感情的シーン」「5段階ワークフロー」 | 日本, 映画, 感情, 構造化 | `sora2-japan-cinematic-prompts` | スタイル + 構造化要件 |
| 「バイリンガル出力」「英語と日本語で」 | バイリンガル, 英語, 日本語 | `sora2-prompt-bilingual` | 言語要件 |

#### Group D: リリック動画生成
| 発話パターン | キーワード | 使用スキル | 判定根拠 |
|---|---|---|---|
| 「リリック動画作って」「歌詞動画」「Remotionで歌詞」 | リリック, 歌詞, 動画 | `create_lyric_video` | 歌詞ベース動画 |
| 「縦書きリリック」「縦書き歌詞動画」 | 縦書き, リリック | `create_vertical_lyric_video` | 特定フォーマット要件 |

#### Group E: 開発・実行
| 発話パターン | キーワード | 使用スキル | 判定根拠 |
|---|---|---|---|
| 「開発環境起動」「プレビュー見たい」「Remotion起動」 | 起動, プレビュー, 環境 | `remotion-preview-launch` | 実行環境制御 |
| 「作業終了」「GitHubにpush」「同期」 | 終了, 完了, GitHub, push | `finish_work` | 終了・同期処理 |
| 「git addでNULエラー」「invalid path 'NUL'」「NULを消したい」 | git, NUL, invalid path, 予約名 | `git-windows-reserved-path-guard` | Windows予約名の検出・修復と再発防止 |

#### Group F: スキル・開発
| 発話パターン | キーワード | 使用スキル | 判定根拠 |
|---|---|---|---|
| 「スキル作って」「スキル更新」「新しい機能作成」 | スキル, 作成, 新機能 | `skill-creator` / `skill-authoring-guidelines` | スキル開発 |

## あいまいな場合の判定ロジック

スキルマッピングがあいまいな場合、以下の優先度で判定:

### ケース1: キーワード部分一致が複数ある場合

**例**: ユーザー「Sora2の映像のアイデアをいくつか出して」
- マッチ候補: `propose-sora-prompts` (「複数案」「アイデア」)
- アクション: 「複数案の提示」
- **判定**: `propose-sora-prompts` を使用 ✓

**例**: ユーザー「1つのプロンプトを作ってください」
- マッチ候補: `create_sora_prompt` (「プロンプト」「作成」)
- アクション: 「単一案の生成」
- **判定**: `create_sora_prompt` を使用 ✓

### ケース2: 文脈的に明確なビジョンがある/ない

**迷った場合のチェック:**
```
Q1: ユーザーは「複数の選択肢を見たい」か「1つの完成品を作りたい」か？
  → 複数選択肢 → `propose-sora-prompts`
  → 1つの完成品 → `create_sora_prompt`

Q2: ユーザーのコンセプトの説明量は？
  → 詳細・具体的 → 単一生成系スキル使用
  → ざっくり・抽象的 → 複数提案系スキルを検討
```

### ケース3: 複数スキルが同時に候補になった場合

**優先順位ルール**（上から順に評価）:
1. ユーザーの発話に「複数」「案」「いくつか」などの複数性キーワードがあるか
   → YES → 複数提案型スキル (`propose-*`) 優先
2. ユーザーが「この方向で作ってほしい」と方向性を指定しているか
   → YES → 単一生成型スキル (`create_*`) 優先
3. 迷った場合は「複数案の提示→選択→詳細化」の流れで、ユーザーに選択権を与えるスキルを優先
   → `propose-*` スキルの方針に従う

### ケース4: 日本映画調など特定スタイルの指定がある場合

**判定**:
- 「日本映画調」「感情的シーン」「5段階ワークフロー」 → `sora2-japan-cinematic-prompts`
- バイリンガル出力要件がある → `sora2-prompt-bilingual`

**優先適用**: より具体的な制約条件を持つスキルを優先

## スキル使用忘れ自己診断チェックリスト

回答を生成する前に、以下のチェックリストを実行し、すべてにチェックが入っているか確認:

### 段階1: リクエスト解析チェック
- [ ] ユーザーの発話から「キーワード」を抽出した
- [ ] 「アクション」（何をしてほしいのか）を明確にした
- [ ] 「ビジョンの明確性」（具体的 vs 抽象的）を判定した
- [ ] 「複数性」（複数案 vs 単一案）を判定した

### 段階2: スキルマッピングチェック
- [ ] クイックルーティング表を参照した
- [ ] 該当する行を少なくとも1つ特定した
- [ ] 複数候補がある場合、優先順位ルールで絞った
- [ ] 最終的なスキル候補を明確に記録した
  - **記録先**: **回答冒頭の「使用スキル」欄に必須記載**（監査可能性のため外部記録を必須化）
  - **記録形式**: 回答の最初の行に「【使用スキル】[スキル名]」
  - **補足記録**: 必要に応じて「抽出キーワード: [キーワード]」を追記可能
  - **責任**: 回答生成者（エージェント自身）

### 段階3: スキル実行判定チェック
- [ ] スキル候補がある場合、その SKILL.md を読んだ
- [ ] 現在のリクエストがそのスキルの「使用場面」に合致するか確認した
- [ ] スキル実行に必要な情報がすべて揃っているか確認した
- [ ] スキル実行を中止する正当な理由がないか確認した

### 段階4: 回答生成チェック
- [ ] 回答の冒頭に「使用スキル: [スキル名]」と明記した
- [ ] 複数スキルがある場合、実行順序を明示した
- [ ] スキルのワークフローに従って進めた
- [ ] スキル使用なしで直接回答していないか

**すべてチェック入ったか？**
- YES → そのまま進める
- NO → 欠けたステップを実行してから回答生成

## スキル使用違反の自己修正フロー

もし、生成途中や生成後に「スキルを使うべきだった」と気づいた場合の対応:

### 違反パターン認識

**以下のいずれかに当てはまれば、スキル使用忘れの可能性が高い:**
- クイックルーティング表に明確に該当するキーワードが発話に含まれている
- 「複数案を見たい」というニーズが隠れているのに単一案を提示している
- スキル説明の「使用場面」そのものなのに直接回答している
- 本来複数段階ワークフロー（案提示→選択→詳細化）なのに1段階で終わっている

### 自己修正ステップ

**Step 1: 違反確認**
- 現在の回答で、該当するスキルがあるか確認
- クイックルーティング表で明確にマッチしているか再検証

**Step 2: 修正判定**
- 修正対象のスキルを明確にする
- 現在の回答をスキルワークフローに従い再構成できるか確認

**Step 3: ユーザー通知と修正**
```
申し訳ありません。ご質問は「[スキル名]」を使うべきでした。
以下、適切なワークフローで改めて対応します：

【使用スキル】[スキル名]
[スキルのワークフローに従い、改めて回答]
```

**Step 4: 二度と繰り返さない**
- 同じパターンでの失敗を記録
- 今後のスキルマッピングに反映

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
- git-windows-reserved-path-guard: Prevent and remediate Git failures caused by Windows reserved names (NUL/CON/AUX/PRN/COM/LPT), including preflight detection and approved cleanup workflow. (file: my-remotion-01/.agent/skills/git-windows-reserved-path-guard/SKILL.md)
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

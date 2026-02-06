# Sora2動画作成スキル化 計画書

## 0. 確定方針

1. 既存拡張で進める（対象: `.agents/skills/sora2-japan-cinematic-prompts/`）
2. 対応レンジは当面 `15秒・16:9` 固定
3. 出力は日英併記（英語版は Sora2 へそのまま貼り付け可能）
4. シーン範囲は限定しない（恋愛ドラマ専用にはしない）
5. 表現ガイドライン（暴力/グロ等の禁止条項）は今回入れない
6. バリエーション標準本数は `1本`
7. 完了条件は `quick_validate通過 + 3ユースケース試験` で確定

## 1. 目的

Sora2で「日本映画のような15秒・16:9動画」を安定して作る手順を、再利用可能なスキルとして整備する。  
対象は、現在のプロンプト作成フロー（カット分割、感情描写、映像トーン指定）を標準化し、短時間で品質を揃えること。

## 2. 現状整理

- 既存スキル: `.agents/skills/sora2-japan-cinematic-prompts/`
- 既存内容:
1. `SKILL.md` に基本ワークフロー（15秒/16:9、カット構造、最終出力形式）
2. `references/` に `prompt-structure.md`, `style-tags.md`, `shot-library.md`, `example-prompts.md`
- 課題:
1. ユーザー要望を整理するヒアリング手順が不足
2. 感情シーン（喪失、涙、別れ等）の自然な描写ガイドが不足
3. 出力前の品質チェック項目（尺、構図、カット接続）が不足
4. 失敗時の修正手順（再生成用の指示テンプレート）が不足
5. 日英併記での出力ルールが不足

## 3. スキル化方針

既存スキルを拡張し、以下の5段階ワークフローに統一する。

1. 要件確定
- 尺、アスペクト比、登場人物、舞台、感情、ラストカットを確認

2. シーン設計
- 15秒を2-5カットへ分解し、各カットに秒数・被写体・カメラ動作・感情変化を割り当て

3. プロンプト生成
- 出力は日英併記
- 英語版はSora2に貼り付け可能な1ブロック形式で生成
- 必須: 時間配分、視覚トーン、音の扱い、過剰演出回避

4. 自己レビュー
- 尺合計15秒、整合性、自然な因果、映像的余韻をチェック

5. 最終出力
- 標準は1本のみ出力
- バリエーションはユーザー明示要求時のみ追加

## 4. 成果物（更新対象）

1. 更新
- `.agents/skills/sora2-japan-cinematic-prompts/SKILL.md`
  - トリガー条件の明確化
  - 5段階ワークフローを明記
  - 日英併記の出力仕様を明記

2. 追加（references）
- `.agents/skills/sora2-japan-cinematic-prompts/references/intake-checklist.md`
  - ヒアリング項目と不足情報の確認テンプレート
- `.agents/skills/sora2-japan-cinematic-prompts/references/emotion-scene-patterns.md`
  - 涙、対立、別れ、再起などのカット設計パターン
- `.agents/skills/sora2-japan-cinematic-prompts/references/quality-checklist.md`
  - 出力前の最終確認チェックリスト
- `.agents/skills/sora2-japan-cinematic-prompts/references/revision-recipes.md`
  - 破綻しやすい点と修正指示テンプレート
- `.agents/skills/sora2-japan-cinematic-prompts/references/bilingual-output-template.md`
  - 日本語版＋英語版（Sora2貼り付け用）テンプレート

3. 必要に応じて更新
- `.agents/skills/sora2-japan-cinematic-prompts/agents/openai.yaml`
  - `SKILL.md` と齟齬が出た場合のみ再生成

## 5. 実行ステップ

1. 要件サンプル収集
- 既存会話（受験生、涙、カップル喪失）をユースケースとして整理

2. スキル本文更新
- `SKILL.md` の説明文と実行手順を簡潔に再構成

3. 参照資料追加
- 5つの `references` ファイルを作成し、`SKILL.md` から直接リンク

4. 検証
- `C:/Users/sench/.codex/skills/.system/skill-creator/scripts/quick_validate.py` で構文検証

5. 試運用
- 3種類以上の依頼で試し、出力の一貫性を確認して微調整

## 6. 完了条件（Done）

1. 3つ以上の異なる依頼パターンで、15秒/16:9の構造化プロンプトを安定生成できる
2. 出力にカット秒数、感情遷移、映像トーン、ラスト演出が明示される
3. 日英併記が毎回維持され、英語版はSora2へそのまま貼り付け可能
4. 標準出力が1本で運用される
5. 参照ファイルが冗長化せず、`SKILL.md` はナビゲーション中心で簡潔に保たれる
6. バリデーションが通る

## 7. リスクと対策

1. リスク: 特定シーンに偏り、汎用性が下がる  
対策: 日常系、失恋系、再起系の3カテゴリで例を持つ

2. リスク: 感情表現が過剰になり不自然化  
対策: 「抑制された演技」「過剰演出回避」をチェック項目化

3. リスク: 日英併記で文字量が増え、可読性が下がる  
対策: 日本語説明を短くし、英語版は固定テンプレートで簡潔化

## 8. 次フェーズ（任意）

運用後、必要であれば以下を追加する。

1. カメラ演出プリセット（固定、スライド、手持ち風）
2. 感情トーン別プリセット（悲哀、再起、余韻）
3. 長さ違いテンプレート（8秒、10秒、30秒）

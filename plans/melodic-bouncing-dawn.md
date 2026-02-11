# プラン: remotion-preview-launch スキルの登録と create_lyric_video との連携強化

## Context

「リリック動画作成後にRemotion Studioを起動する」という運用がスキル化されていなかった。

調査の結果、`remotion-preview-launch` スキル自体は **既に存在する**（`.agent/skills/remotion-preview-launch/SKILL.md` + PowerShellスクリプト群）。`create_lyric_video` のStep 8でも参照されている。

**しかし、`remotion-preview-launch` が AGENTS.md の Available skills に未登録**であるため、スキルとして認識・実行されていなかった。これが根本原因。

## 変更内容

### 1. AGENTS.md に `remotion-preview-launch` を登録

**ファイル**: `c:\Users\sench\remotion-test-work\AGENTS.md`

- **Available skills セクション**に以下を追加:
  ```
  - remotion-preview-launch: Start or check Remotion Studio and return preview URL/PID/log paths after lyric video work, or when user asks to launch development preview. (file: my-remotion-01/.agent/skills/remotion-preview-launch/SKILL.md)
  ```

- **クイックルーティング表**に以下を追加:
  ```
  | 「開発環境起動」「プレビュー」「Remotion起動」 | `remotion-preview-launch` |
  ```

### 2. Layer 4 CLAUDE.md のルーティング表を更新

**ファイル**: `c:\Users\sench\.claude\projects\c--Users-sench-remotion-test-work\CLAUDE.md`

- ルーティング表に追加:
  ```
  | 開発環境、プレビュー、Remotion起動 | `remotion-preview-launch` |
  ```

### 3. MEMORY.md のルーティング表を更新

**ファイル**: `c:\Users\sench\.claude\projects\c--Users-sench-remotion-test-work\memory\MEMORY.md`

- 全スキル・ルーティング表に追加:
  ```
  | 「開発環境起動」「プレビュー」「Remotion起動」 | `remotion-preview-launch` |
  ```

### 4. create_lyric_video の Step 8 を強化

**ファイル**: `c:\Users\sench\remotion-test-work\my-remotion-01\.agent\skills\create_lyric_video\SKILL.md`

- Step 8 を「CRITICAL」に格上げし、スキルの呼び出し方法を明確化:
  ```markdown
  8.  **Launch Preview Via Dedicated Skill (CRITICAL — 必ず実行)**
      *   **必ず** `remotion-preview-launch` スキルの SKILL.md を読み、そのワークフローに従って起動する。
      *   PowerShellスクリプト: `.agent/skills/remotion-preview-launch/scripts/start_remotion_dev.ps1`
      *   Return the detected Remotion URL, PID, and stop command.
      *   Do not assume `http://localhost:3000`; always report the detected URL.
  ```

## 変更対象ファイル一覧

| ファイル | 変更内容 |
|---------|---------|
| `AGENTS.md` | Available skills + ルーティング表に追加 |
| `~/.claude/projects/.../CLAUDE.md` | ルーティング表に追加 |
| `~/.claude/projects/.../memory/MEMORY.md` | ルーティング表に追加 |
| `my-remotion-01/.agent/skills/create_lyric_video/SKILL.md` | Step 8 を強化 |

## 検証方法

1. AGENTS.md の Available skills に `remotion-preview-launch` が表示されていることを確認
2. クイックルーティング表に「開発環境起動」→ `remotion-preview-launch` が存在することを確認
3. 全4ファイルの整合性を目視確認（ルーティング表が一致していること）

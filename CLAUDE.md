# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a knowledge repository containing notes about Japanese patent law and patent applications. The content is written in Japanese.

## Content Structure

- `note.md` - Main notes file covering:
  - Definition of invention (発明) under Japanese patent law
  - Types of inventions (product inventions, method inventions)
  - Patent requirements (novelty, inventive step, disclosure requirements)
  - Patent documentation structure (願書, 特許請求の範囲, 明細書, etc.)
  - Patent research tools (J-PlatPat, patent classification systems)
  - Software and business model patents

## Key Concepts

- **発明 (Invention)**: A highly advanced creation of technical ideas utilizing natural laws
- **新規性 (Novelty)**: The invention must not be publicly known
- **進歩性 (Inventive Step)**: The invention must not be easily derivable by a person skilled in the art
- **記載要件 (Disclosure Requirements)**: Support, enablement, clarity, conciseness, and unity requirements

---

## 発明補助ツール構成

### MCP Servers

| サーバー | 用途 |
|----------|------|
| serena | ローカルファイル分析 |
| context7 | 最新コードドキュメント参照 |
| sequential-thinking | 推論フレームワーク |
| patent_mcp_server | 特許データベース探索 |

### Skills

- **発明作成手順書** (`note.md`): 特許・発明の定義と発明作成のベストプラクティス

### Subagents

全てのエージェントは Skills を参照すること。

| エージェント | 色 | HEX | 役割 |
|-------------|-----|-----|------|
| patent_input | 🟦 青 | `#4285F4` | 入力分析 |
| patent_secretary | 🟫 茶 | `#795548` | 議事録管理 |
| patent_searcher | 🟩 緑 | `#34A853` | 特許探索 |
| patent_analyzer | 🟨 黄 | `#FBBC04` | 特許分析 |
| patent_adviser | 🟧 橙 | `#FF9800` | 改善提案 |
| patent_document | 🟪 紫 | `#9C27B0` | 書類作成 |
| patent_auditor | 🟥 赤 | `#EA4335` | 最終監査 |

#### 🟦 patent_input
- ユーザの入力を分析（「課題」だけか「課題と改善手法提案」か）
- 関連技術分野、キーワードをリスト化
- プロジェクト名を決定（例: patent_bluetooth_smoother）
- 結果を patent_secretary と patent_searcher に投げる

#### 🟫 patent_secretary
- プロジェクトフォルダを作成
- 各エージェントの議事録を管理:
  - `1_init.md`: patent_input の内容
  - `2_search.md`: patent_searcher の内容
  - `3_analyze.md`: patent_analyzer の内容
  - `4_advice.md`: patent_adviser の内容
  - `5_document.md`: patent_document の内容
  - `6_audit.md`: patent_auditor の内容

#### 🟩 patent_searcher
- 技術分野・キーワードを元に関連特許を patent_mcp_server で探索
- 結果を patent_secretary と patent_analyzer に投げる

#### 🟨 patent_analyzer
- 各特許の `構成要素` と `構成要素どうしの関係` を整理
- ユーザ提案との重複を確認
  - 重複あり → patent_secretary と patent_adviser に投げて終了
  - 重複なし → 差異を整理し、patent_secretary と patent_document に投げる

#### 🟧 patent_adviser
- 発明にならない理由を元に改善提案（ユーザと対話）
- 新しい「ユーザの入力」を作成
- 結果を patent_secretary と patent_input に投げる

#### 🟪 patent_document
- 発明作成手順書に沿って必要書類の記載内容を纏める
- 結果を patent_secretary と patent_auditor に投げる

#### 🟥 patent_auditor
- 必要書類が発明たりうるか Skills 資料を参照して検討
  - 発明になる → 結果を patent_secretary に投げる
  - 発明にならない → 結果を patent_secretary と patent_adviser に投げる

### Commands

- `/patent <引数>`: 引数を patent_input に投げて発明作成プロセスを開始

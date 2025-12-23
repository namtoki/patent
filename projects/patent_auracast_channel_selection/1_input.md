# 1. 入力分析 (patent_input)

**日時**: 2025-12-23
**プロジェクト名**: patent_auracast_channel_selection

---

## 元の入力

> Auracast Assistant が Auracast Receiver の特性を鑑みて適切な BIG チャンネルを選択できるようにしたい

---

## 入力タイプ

**課題のみ**（具体的な解決手段は未指定）

---

## 課題の整理

| 項目 | 内容 |
|------|------|
| 対象システム | Auracast（Bluetooth LE Audio のブロードキャスト機能） |
| 登場要素 | Auracast Assistant、Auracast Receiver、BIG（Broadcast Isochronous Group）チャンネル |
| 課題 | Receiver の特性に基づいて適切な BIG チャンネルを選択する仕組みがない |
| 現状の問題点 | Receiver の能力（コーデック対応、チャンネル数、品質設定等）を考慮せずにチャンネル選択している可能性 |

---

## 技術分野・キーワード

### 通信規格
- Bluetooth LE Audio
- Auracast
- BIS (Broadcast Isochronous Stream)
- BIG (Broadcast Isochronous Group)

### プロトコル
- BAP (Basic Audio Profile)
- BASS (Broadcast Audio Scan Service)
- PACS (Published Audio Capabilities Service)

### 技術要素
- ブロードキャストオーディオ
- チャンネル選択
- デバイス能力交換
- コーデック（LC3）

### CPC分類候補
- H04W 4/80: オーディオストリーミング
- H04W 76/: 接続管理
- H04R 5/: ステレオ・マルチチャンネル

---

## 想定される解決手段の方向性

1. **Receiver 特性の取得**: PACS (Published Audio Capabilities) から Receiver のオーディオ能力を取得
2. **BIG パラメータとのマッチング**: Receiver が対応可能な BIG/BIS パラメータを判定
3. **チャンネル選択アルゴリズム**: 複数の BIG から最適なものを選択するロジック
4. **動的な切り替え**: Receiver の状態変化に応じた再選択

---

## 次のステップ

→ patent_searcher: 関連特許の探索

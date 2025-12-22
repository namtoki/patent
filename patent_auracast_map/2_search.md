# 発明作成プロセス - 先行技術調査

## プロジェクト情報
- **プロジェクト名**: patent_auracast_map
- **作成日**: 2025-12-22
- **ステータス**: 先行技術調査完了

---

## 1. 調査概要

### 調査対象
- USPTO Patent Public Search (PPUBS)
- 検索対象: 米国特許（Granted Patents）

### 検索クエリ
1. `"Auracast" OR "Bluetooth LE Audio" OR "broadcast audio" AND map`
2. `"Bluetooth broadcast" AND location AND server`
3. `"audio broadcast" AND "geographic" AND display`
4. `"LE Audio" OR "broadcast audio" AND (location OR position) AND (map OR display)`
5. `Bluetooth AND beacon AND server AND (aggregat* OR collect*) AND map`

---

## 2. 関連特許一覧

### 最も関連性の高い特許

#### US 12,476,725 B2
- **タイトル**: Broadcast signal playback method, map generation method, and apparatus
- **出願人**: Shenzhen Yinwang Intelligent Technology Co., Ltd.
- **発行日**: 2024-12-31
- **関連度**: ★★★★★（非常に高い）

**概要**:
ブロードキャスト信号の再生方法と地図生成方法に関する特許。位置情報とブロードキャスト信号を組み合わせた技術。

**本発明との比較**:
- 共通点: ブロードキャスト信号と地図の組み合わせ
- 相違点: Auracast特有の情報処理、サーバ蓄積アーキテクチャの詳細

---

### Bluetooth LE Audio関連特許

#### US 12,445,777 B2
- **タイトル**: Methods and arrangements for a broadcast audio receiver feedback channel
- **出願人**: Intel Corporation
- **発行日**: 2024年
- **関連度**: ★★★☆☆（中程度）

**概要**:
ブロードキャストオーディオ受信機のフィードバックチャネルに関する方法。受信側から送信側への情報伝達。

**本発明との比較**:
- 共通点: Bluetooth LE Audio / ブロードキャストオーディオ技術
- 相違点: 本発明はサーバ蓄積と地図表示が主眼、フィードバックチャネルではない

---

#### US 12,483,970 B2
- **タイトル**: Method for transmitting and receiving data and device for same in short-range wireless communication system
- **出願人**: LG Electronics Inc.
- **発行日**: 2024年
- **関連度**: ★★★☆☆（中程度）

**概要**:
短距離無線通信システムにおけるデータ送受信方法とデバイス。

**本発明との比較**:
- 共通点: 短距離無線通信（Bluetooth関連）
- 相違点: 地図表示やサーバ蓄積の概念なし

---

#### US 12,474,887 B2
- **タイトル**: Method and system for sharing audio stream
- **出願人**: Beijing Xiaomi Mobile Software Co., Ltd.
- **発行日**: 2024年
- **関連度**: ★★★☆☆（中程度）

**概要**:
オーディオストリームを共有するための方法とシステム。

**本発明との比較**:
- 共通点: オーディオストリーム共有
- 相違点: 位置情報との紐付け、地図表示機能なし

---

#### US 12,477,285 B2
- **タイトル**: Transmitting audio streams to auditory devices based on user preferences
- **出願人**: Sony Group Corporation
- **発行日**: 2024年
- **関連度**: ★★☆☆☆（低〜中程度）

**概要**:
ユーザの好みに基づいてオーディオストリームを聴覚デバイスに送信。

**本発明との比較**:
- 共通点: オーディオストリーム送信
- 相違点: サーバ蓄積、地図表示の概念なし

---

### Bluetoothビーコン・位置情報関連

#### 関連技術分野の既存特許
- Bluetoothビーコンによる位置情報サービス
- サーバでのビーコン情報集約
- 地図アプリでのPOI表示

これらの技術は個別に多数の特許が存在するが、**Auracast（Bluetooth LE Audio ブロードキャスト）の情報をサーバに蓄積し地図表示する**という組み合わせは確認されなかった。

---

## 3. 調査結果の分析

### 先行技術の状況

| 技術要素 | 先行技術の有無 | 備考 |
|----------|--------------|------|
| Auracast/LE Audio ブロードキャスト | あり | Bluetooth SIG規格、複数社が特許保有 |
| サーバへの情報蓄積 | あり | クラウドサービス一般技術 |
| 地図上のPOI表示 | あり | Google Maps等で一般的 |
| ブロードキャスト信号と地図の組み合わせ | 一部あり | US 12,476,725 B2 |
| **Auracast情報のサーバ蓄積＋地図表示** | **未確認** | 本発明の核心部分 |

### 最も近い先行技術

**US 12,476,725 B2** (Shenzhen Yinwang)
- ブロードキャスト信号と地図生成を組み合わせた最も近い先行技術
- ただし、Auracast（Bluetooth LE Audio）に特化した構成ではない可能性
- サーバ側での情報蓄積・管理アーキテクチャの詳細は不明

---

## 4. 新規性・進歩性の予備評価

### 新規性について
- 個々の技術要素（Auracast、サーバ蓄積、地図表示）は既存
- **組み合わせとしての新規性**を主張できる可能性あり
- US 12,476,725 B2 との差別化が重要

### 進歩性について
- 単純な技術の組み合わせと見なされるリスクあり
- 以下の点で進歩性を主張可能:
  1. **Auracast特有のメタデータ活用**: BAP/BASS規格に基づく詳細情報
  2. **動的更新機構**: クライアント端末からのリアルタイム情報収集
  3. **クラウドソーシング型データ収集**: 多数のユーザ端末から情報を集約

---

## 5. 次のステップへの推奨事項

### patent_analyzer への引継ぎ事項

1. **US 12,476,725 B2 の詳細分析が必要**
   - クレーム内容の確認
   - 本発明との技術的差異の明確化

2. **新規性確保のための検討ポイント**
   - Auracast固有の技術要素（BIS、BAP、BASS）の活用
   - サーバ側の処理アーキテクチャの特徴化
   - クライアント端末の協調動作

3. **進歩性確保のための検討ポイント**
   - 技術的課題と解決手段の関係性の明確化
   - 従来技術では達成できなかった効果の特定

---

## 議事録

| 日時 | エージェント | 内容 |
|------|------------|------|
| 2025-12-22 | patent_input | 入力分析完了、プロジェクト名決定: patent_auracast_map |
| 2025-12-22 | patent_secretary | プロジェクトフォルダ作成、初期分析文書作成 |
| 2025-12-22 | patent_searcher | USPTO検索完了、関連特許5件特定、最重要: US 12,476,725 B2 |

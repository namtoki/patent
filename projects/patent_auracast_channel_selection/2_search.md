# 2. 特許探索結果 (patent_searcher)

**日時**: 2025-12-23
**プロジェクト名**: patent_auracast_channel_selection

---

## 検索条件

### キーワード
- Auracast, Bluetooth LE Audio, broadcast audio
- BIG (Broadcast Isochronous Group), BIS (Broadcast Isochronous Stream)
- receiver capability, channel selection
- PACS (Published Audio Capabilities Service)

### CPC分類
- H04W 4/80: オーディオストリーミング
- H04W 76/: 接続管理
- H04R 5/: ステレオ・マルチチャンネル

### 検索範囲
- USPTO PPUBS（特許・公開出願）
- PatentsView

---

## 関連特許一覧

### 特許1: US-20250374018-A1 (Google)

| 項目 | 内容 |
|------|------|
| 特許番号 | US 2025/0374018 A1 |
| 発明の名称 | RECEPTION-BASED BROADCAST TEMPLATE ADJUSTMENT |
| 出願人 | Google LLC |
| 出願日 | 2024-05-09 |
| 公開日 | 2025-11-13 |

#### 要約
受信デバイスからの受信データに基づいてブロードキャストパラメータを調整するシステム。UEがBluetooth LEを介してオーディオ信号をブロードキャストし、受信デバイスが受信品質データを返送し、それに基づいてブロードキャストテンプレート（再送回数、チャンネル数等）を調整する。

#### クレーム概要
1. 受信デバイスからの受信データの受信
2. 受信データに基づくブロードキャストパラメータの調整
3. 調整後のテンプレートでのブロードキャスト継続

#### 関連度: **高**

#### 選定理由
- Auracast/BLE Audio のブロードキャストパラメータ調整に関する発明
- 受信デバイスからのフィードバックに基づく動的調整という点で類似
- **差異点**: 受信品質データ（受信状態）に基づく調整であり、受信デバイスの「能力」（コーデック対応、チャンネル構成対応等）に基づく選択ではない

---

### 特許2: US-12483970-B2 (LG Electronics)

| 項目 | 内容 |
|------|------|
| 特許番号 | US 12,483,970 B2 |
| 発明の名称 | Method for data transmission in short-range wireless systems |
| 出願人 | LG Electronics Inc. |
| 発行日 | 2025-09-22 |

#### 要約
短距離無線システム（Bluetooth LE Audio含む）におけるデータ伝送方法に関する発明。

#### 関連度: **中**

#### 選定理由
- Bluetooth LE Audioの基盤技術に関連
- 直接的なチャンネル選択アルゴリズムではない

---

### 特許3: US-12445777-B2 (Intel)

| 項目 | 内容 |
|------|------|
| 特許番号 | US 12,445,777 B2 |
| 発明の名称 | Methods and arrangements for a broadcast audio receiver feedback channel |
| 出願人 | Intel Corporation |
| 発行日 | 2025年 |

#### 要約
ブロードキャストオーディオ受信機からのフィードバックチャンネルに関する方法と装置。

#### 関連度: **高**

#### 選定理由
- Auracast受信機からのフィードバック機構に関連
- 受信機からBroadcasterへの情報伝達という概念が類似
- **差異点**: フィードバックチャンネルの確立方法であり、能力に基づくBIG選択ロジックではない

---

### 特許4: US-12349031-B2 (LG Electronics)

| 項目 | 内容 |
|------|------|
| 特許番号 | US 12,349,031 B2 |
| 発明の名称 | Audio data reception method using short-range wireless communication in wireless communication system, and apparatus therefor |
| 出願人 | LG Electronics Inc. |
| 公開日 | 2025-07-01 |

#### 要約
短距離無線通信（Bluetooth LE Audio）を使用したオーディオデータ受信方法。CPC分類にH04W4/80（オーディオストリーミング）を含む。

#### 関連度: **中**

#### 選定理由
- LE Audio のオーディオ受信に関する基盤技術
- 直接的なBIG選択メカニズムではない

---

### 特許5: US-12127140-B2 (LG Electronics)

| 項目 | 内容 |
|------|------|
| 特許番号 | US 12,127,140 B2 |
| 発明の名称 | Audio data transmission method using short-range wireless communication in wireless communication system and apparatus therefor |
| 出願人 | LG Electronics Inc. |
| 公開日 | 2024-10-22 |

#### 要約
短距離無線通信を使用したオーディオデータ伝送方法。H04W4/80（オーディオストリーミング）関連。

#### 関連度: **中**

#### 選定理由
- LE Audio の送信側技術
- BIG/BIS パラメータ設定に関連する可能性

---

## 探索サマリー

| 項目 | 結果 |
|------|------|
| 検索件数 | 約100件以上 |
| 選定件数 | 5件 |
| 最関連特許 | US-20250374018-A1 (Google) |

### 主要な技術トレンド

1. **受信品質フィードバック**: 受信デバイスからの受信品質データに基づくパラメータ調整（Google特許）
2. **フィードバックチャンネル**: ブロードキャスト受信機からの上りリンク確立（Intel特許）
3. **LE Audio基盤技術**: オーディオ伝送・受信の基本メカニズム（LG特許群）

### 発見された技術的ギャップ

提案発明「Receiver の能力（PACS情報）に基づくBIGチャンネル選択」に関して：

| 既存技術 | 提案発明の差異 |
|----------|----------------|
| 受信品質に基づく調整 | **能力**（コーデック対応、チャンネル構成）に基づく選択 |
| ブロードキャストパラメータの動的調整 | **事前の能力マッチング**によるBIG選択 |
| フィードバックチャンネルの確立 | **PACS情報の活用**による能力交換 |

**新規性のポイント**:
- 既存特許は「受信品質」（reception quality）に基づく調整
- 提案発明は「受信能力」（receiver capabilities）に基づく事前選択
- PACSを活用した能力情報取得と、BIGパラメータとのマッチングアルゴリズム

---

## 次のステップ

→ patent_analyzer: 新規性・進歩性の詳細分析

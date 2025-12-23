# 5. 発明提案書 (patent_document)

**日時**: 2025-12-23
**プロジェクト名**: patent_auracast_channel_selection
**ドキュメントバージョン**: 1.0

---

# 発明提案書

## 1. 発明の名称

**Auracast受信機の能力に基づくブロードキャストオーディオストリーム選択方法、システム、および電子機器**

英語名称案: Method, System, and Electronic Device for Selecting Broadcast Audio Stream Based on Auracast Receiver Capabilities

---

## 2. 技術分野

本発明は、Bluetooth Low Energy (BLE) Audio技術に基づくブロードキャストオーディオ配信システムに関し、特にAuracast規格に準拠したブロードキャストオーディオストリームの選択技術に関する。

---

## 3. 背景技術

### 3.1 Auracastの概要

Auracast は Bluetooth SIG が策定した LE Audio のブロードキャスト機能の商標名であり、1つの音源から複数の受信機に同時にオーディオを配信することができる。Auracast は以下の要素で構成される：

- **Broadcast Source**: オーディオをブロードキャストする送信機
- **Broadcast Assistant**: ブロードキャストの発見と受信機への接続支援を行う制御機器
- **Broadcast Sink (Receiver)**: ブロードキャストオーディオを受信する機器

### 3.2 BIG/BISの構造

Auracast では、オーディオストリームは以下の階層構造で配信される：

- **BIG (Broadcast Isochronous Group)**: ブロードキャストストリームのグループ
- **BIS (Broadcast Isochronous Stream)**: 個別のオーディオストリーム

1つのBroadcast Sourceは複数のBIGを持つことができ、各BIGは異なるオーディオパラメータ（コーデック設定、チャンネル構成、品質レベル等）を持つことができる。

### 3.3 関連プロトコル

- **BASS (Broadcast Audio Scan Service)**: ブロードキャストソースの発見と同期
- **PACS (Published Audio Capabilities Service)**: 機器のオーディオ能力の公開

### 3.4 従来技術の課題

従来のBroadcast Assistantは、利用可能なBIGを検出した際に、以下のいずれかの方法でストリームを選択していた：

1. **最初に検出したBIGを選択**: 能力の適合性を考慮しない
2. **ユーザーによる手動選択**: ユーザー負担が大きい
3. **固定的なルールによる選択**: 個々のReceiverの能力を考慮しない

これらの方法では、Receiverが対応できないBIGに接続しようとして失敗したり、Receiverの能力を活かせないBIGを選択したりする問題があった。

---

## 4. 発明が解決しようとする課題

本発明は、Auracast受信機（Broadcast Sink）の実際の能力に基づいて、最適なBIGを自動的に選択することで、以下の課題を解決する：

1. 能力不適合なBIGへの接続失敗の回避
2. Receiverの能力を最大限に活かしたオーディオ体験の提供
3. ユーザーの操作負担軽減
4. システムリソースの効率的な利用

---

## 5. 課題を解決するための手段

### 5.1 発明の概要

本発明は、Broadcast Assistantが以下の処理を実行することで課題を解決する：

1. **能力情報取得**: Receiverから PACS を介してオーディオ能力情報を取得
2. **BIG情報解析**: 利用可能なBIGのオーディオパラメータを取得
3. **能力マッチング**: Receiverの能力とBIGパラメータを比較し適合性を判定
4. **最適選択**: 複数の適合BIGから最適なものを選択
5. **接続指示**: 選択したBIGへの接続をReceiverに指示

### 5.2 システム構成

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│  Broadcast      │     │   Broadcast     │     │   Broadcast     │
│   Source        │────▶│   Assistant     │◀───▶│   Sink          │
│                 │     │                 │     │  (Receiver)     │
└─────────────────┘     └─────────────────┘     └─────────────────┘
        │                       │                       │
        │  BASE/BIG情報         │  PACS能力情報         │
        │  ブロードキャスト     │  接続指示             │
        ▼                       ▼                       ▼
   ┌─────────┐           ┌─────────────┐         ┌─────────┐
   │ BIG 1   │           │  マッチング │         │  能力   │
   │ BIG 2   │           │  アルゴリズム│         │  情報   │
   │ BIG 3   │           └─────────────┘         └─────────┘
   └─────────┘
```

### 5.3 能力マッチングアルゴリズム

#### 5.3.1 マッチング対象パラメータ

| パラメータ | Receiver側（PACS） | BIG側（BASE） |
|------------|-------------------|---------------|
| コーデック | Supported_Audio_Contexts | Codec_ID |
| サンプリングレート | Sampling_Frequency | Sampling_Frequency |
| フレーム時間 | Supported_Frame_Durations | Frame_Duration |
| チャンネル構成 | Audio_Channel_Counts | Audio_Channel_Allocation |
| ビットレート | Supported_Octets_Per_Codec_Frame | Octets_Per_Codec_Frame |

#### 5.3.2 マッチング処理フロー

```
開始
  ↓
[1] ReceiverのPACS情報を取得
  ↓
[2] 利用可能な全BIGのBASE情報を取得
  ↓
[3] 各BIGについてループ
  │  ├─ [3.1] コーデック適合性チェック
  │  ├─ [3.2] サンプリングレート適合性チェック
  │  ├─ [3.3] チャンネル構成適合性チェック
  │  └─ [3.4] 全チェック通過 → 適合BIGリストに追加
  ↓
[4] 適合BIGリストから最適BIGを選択
  │  ├─ 品質優先モード: 最高品質のBIGを選択
  │  ├─ 省電力モード: 最低消費電力のBIGを選択
  │  └─ バランスモード: 品質と電力のバランスで選択
  ↓
[5] 選択したBIGへの接続をReceiverに指示
  ↓
終了
```

### 5.4 動的再選択機能

以下の状況変化を検出した場合、BIGの再選択を実行する：

1. **新規BIGの検出**: より適合度の高いBIGが利用可能になった場合
2. **バッテリー残量低下**: 省電力BIGへの切替を検討
3. **接続品質低下**: 代替BIGへの切替を検討
4. **ユーザー設定変更**: 新しい優先度に基づく再選択

---

## 6. 発明の効果

### 6.1 技術的効果

1. **接続成功率の向上**: 能力不適合による接続失敗を事前に回避
2. **最適なオーディオ体験**: Receiverの能力を最大限に活用
3. **自動化**: ユーザーの手動選択不要
4. **リソース効率化**: 無駄な接続試行の削減

### 6.2 ユーザー体験の改善

1. シームレスな接続体験
2. デバイス能力に応じた最適な音質
3. バッテリー寿命の最適化

---

## 7. 実施形態

### 7.1 基本実施形態

スマートフォン（Broadcast Assistant）が、ワイヤレスイヤホン（Broadcast Sink）をカフェのAuracastストリーム（Broadcast Source）に接続する場合：

1. スマートフォンがイヤホンのPACS情報を取得（LC3対応、48kHz対応、ステレオ対応）
2. カフェのAuracastから3つのBIGを検出
   - BIG 1: LC3, 48kHz, ステレオ, 高品質
   - BIG 2: LC3, 24kHz, モノラル, 省電力
   - BIG 3: LC3, 16kHz, モノラル, 超省電力
3. イヤホンの能力とマッチング → BIG 1, 2 が適合
4. 品質優先設定 → BIG 1 を選択
5. イヤホンにBIG 1への接続を指示

### 7.2 複数Receiver実施形態

1台のスマートフォン（Assistant）が、2台の異なるイヤホン（Receiver A, B）を同じBroadcast Sourceに接続する場合：

- Receiver A: 高性能イヤホン（48kHz, ステレオ対応）
- Receiver B: 低価格イヤホン（24kHz, モノラル対応）

それぞれの能力に応じて、Receiver AにはBIG 1（高品質）、Receiver BにはBIG 2（省電力）への接続を指示。

### 7.3 動的切替実施形態

イヤホンのバッテリー残量が20%以下になった場合：

1. バッテリー残量低下を検出
2. 現在のBIG 1（高品質）から省電力なBIG 2への切替を評価
3. ユーザーに切替を提案（または自動切替）
4. BIG 2への切替を実行

---

## 8. 特許請求の範囲（案）

### 請求項1（独立項・方法）

ブロードキャストオーディオシステムにおける制御装置によるストリーム選択方法であって、
(a) 受信装置から、前記受信装置のオーディオ能力情報を取得するステップと、
(b) ブロードキャスト送信装置から、利用可能な複数のブロードキャストストリームのパラメータ情報を取得するステップと、
(c) 前記オーディオ能力情報と前記パラメータ情報を比較し、前記受信装置が受信可能なブロードキャストストリームを判定するステップと、
(d) 前記受信可能なブロードキャストストリームから、所定の選択基準に基づいて最適なストリームを選択するステップと、
(e) 前記選択されたストリームへの接続を前記受信装置に指示するステップと、
を含むことを特徴とする方法。

### 請求項2

前記オーディオ能力情報は、Published Audio Capabilities Service (PACS)を介して取得される、請求項1に記載の方法。

### 請求項3

前記オーディオ能力情報は、対応コーデック、対応サンプリングレート、対応チャンネル構成、および対応ビットレートの少なくとも1つを含む、請求項1に記載の方法。

### 請求項4

前記パラメータ情報は、Broadcast Audio Source Endpoint (BASE)から取得される、請求項1に記載の方法。

### 請求項5

前記選択基準は、オーディオ品質優先、省電力優先、またはユーザー設定に基づく優先度の少なくとも1つを含む、請求項1に記載の方法。

### 請求項6

前記受信装置のバッテリー残量情報をさらに取得し、前記バッテリー残量が所定の閾値以下の場合、省電力ストリームを優先的に選択する、請求項1に記載の方法。

### 請求項7

新規ブロードキャストストリームの検出を監視するステップと、新規ストリーム検出時に前記判定するステップを再実行するステップと、をさらに含む、請求項1に記載の方法。

### 請求項8（独立項・システム）

ブロードキャストオーディオ選択システムであって、
受信装置のオーディオ能力情報を取得する能力取得部と、
ブロードキャストストリームのパラメータ情報を取得するストリーム情報取得部と、
前記オーディオ能力情報と前記パラメータ情報に基づいて、前記受信装置が受信可能なストリームを判定し、最適なストリームを選択する選択処理部と、
選択されたストリームへの接続を前記受信装置に指示する接続制御部と、
を備えることを特徴とするシステム。

### 請求項9（独立項・装置）

ブロードキャストオーディオの選択を支援する電子機器であって、
プロセッサと、メモリと、Bluetooth通信インターフェースとを備え、
前記プロセッサは、
受信装置からオーディオ能力情報を取得し、
利用可能なブロードキャストストリームを検出し、
前記オーディオ能力情報に基づいて前記受信装置に適合するストリームを判定し、
前記適合するストリームへの接続を前記受信装置に指示する、
処理を実行することを特徴とする電子機器。

---

## 9. 図面の説明

### 図1: システム構成図
Broadcast Source、Broadcast Assistant、Broadcast Sink の接続関係と情報の流れ

### 図2: 処理フローチャート
能力取得→BIG情報取得→マッチング→選択→接続指示の処理フロー

### 図3: シーケンス図
各デバイス間のメッセージシーケンス

### 図4: 能力マッチングの概念図
PACS情報とBASE情報の対応関係

### 図5: BIG選択アルゴリズムの詳細フローチャート
マッチング判定と最適選択の詳細処理

---

## 10. 先行技術文献

### 特許文献
1. US 2025/0374018 A1 (Google) - Reception-Based Broadcast Template Adjustment
2. US 12,445,777 B2 (Intel) - Methods and arrangements for a broadcast audio receiver feedback channel
3. US 12,349,031 B2 (LG Electronics) - Audio data reception method using short-range wireless communication

### 非特許文献
1. Bluetooth SIG, "Assigned Numbers", https://www.bluetooth.com/specifications/assigned-numbers/
2. Bluetooth SIG, "Basic Audio Profile Specification", Version 1.0
3. Bluetooth SIG, "Broadcast Audio Scan Service Specification", Version 1.0

---

## 11. 発明者情報

（記載予定）

---

## 12. 出願人情報

（記載予定）

---

## 付録A: 用語定義

| 用語 | 定義 |
|------|------|
| Auracast | Bluetooth LE Audioのブロードキャスト機能の商標名 |
| BIG | Broadcast Isochronous Group - ブロードキャストストリームのグループ |
| BIS | Broadcast Isochronous Stream - 個別のオーディオストリーム |
| BASS | Broadcast Audio Scan Service - ブロードキャスト発見サービス |
| PACS | Published Audio Capabilities Service - オーディオ能力公開サービス |
| BASE | Broadcast Audio Source Endpoint - ブロードキャストソース情報 |
| LC3 | Low Complexity Communication Codec - LE Audio標準コーデック |

---

## 付録B: CPC分類（案）

- H04W 4/80: Services using short range communication (audio streaming)
- H04W 76/14: Connection setup
- H04R 5/02: Arrangements for private hearing
- H04B 7/24: Radio communication systems

---

**ドキュメント終了**

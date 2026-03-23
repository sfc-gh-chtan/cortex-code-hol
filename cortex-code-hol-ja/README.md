# Cortex Code ハンズオンラボ v3 - 財務分析POCの構築

## 概要

このハンズオンラボでは、Cortex Codeを使用して組織の主要ステークホルダー向けの説得力のある**財務分析POC**を構築する方法を学びます。あなたはPinnacle Financial Servicesの**BIアナリスト**として、SnowflakeのAI機能が財務レポーティングをどのように変革できるかを実証する役割を担います。

1. **POCの構築** - Cortex AnalystとSnowflake Intelligenceで動作するデモを作成
2. **Cortex Codeスキルのマスター** - 組み込みスキルを使用し、チーム用カスタムスキルを作成
3. **ステークホルダー向けドキュメントの準備** - 経営陣向けのアーキテクチャドキュメントとガイドを生成

**所要時間:** 2.5〜3時間  
**前提条件:** Cortex Codeインストール済み、アクティブなSnowflake接続  
**ユースケース:** 財務分析 - 収益、経費、財務レポーティング

---

## ラボシナリオ: あなたはPinnacle Financial ServicesのBIアナリスト

あなたはPinnacle Financialのデータチームで**BIアナリスト**として働いています。CFOのMargaret Chenから、AI搭載の分析が経営陣の財務に関する質問により迅速に回答する方法を示すPOCの構築を依頼されました。

### あなたの会社

| 項目 | 詳細 |
|-------|---------|
| **会社名** | Pinnacle Financial Services |
| **業種** | 金融サービス / 資産運用 |
| **規模** | AUM 20億ドル、従業員150名、顧客口座5万件 |
| **現状** | 分断されたレポーティング（Excel、レガシーBI）、手動照合 |
| **目標** | AI搭載インサイトを備えた統合財務分析 |
| **主要ステークホルダー** | Margaret Chen（CFO）、David Park（オペレーション担当VP）、Sarah Martinez（コンプライアンス） |
| **あなたのゴール** | 経営陣を感動させ、本番承認を得るPOCを構築 |

### 経営陣が見たいこと

1. **収益分析** - AUM成長、手数料収益、顧客収益性の追跡
2. **経費管理** - 運営コスト、ベンダー支出、予算差異のモニタリング
3. **財務レポーティング** - 自動化されたP&L、貸借対照表、規制報告書
4. **AIインサイト** - 経営陣向け自然言語クエリ（「前四半期の収益成長の要因は？」）

---

## ラボ構成

| 演習 | 焦点領域 | 所要時間 | 構築するもの |
|----------|------------|----------|-------------------|
| [演習1](exercises/exercise-1-rapid-demo.md) | POCの構築 | 60分 | デモ用データベース、セマンティックビュー、Snowflake Intelligence |
| [演習2](exercises/exercise-2-skills.md) | Cortex Codeスキルのマスター | 60分 | バンドルスキルの使用、チーム固有スキルの作成 |
| [演習3](exercises/exercise-3-documentation.md) | ステークホルダー向けドキュメント | 45分 | アーキテクチャ図、経営陣向け統合ガイド |

---

## はじめに

### ステップ1: ラボアセットをアクセス可能な場所に移動

このフォルダをダウンロードディレクトリからCortex Codeがアクセスできる場所（Documentsフォルダや専用プロジェクトディレクトリなど）に移動します：

```bash
# 例: Documentsに移動
mv ~/Downloads/cortex-code-hol-v3 ~/Documents/

# またはprojectsフォルダを作成
mkdir -p ~/projects
mv ~/Downloads/cortex-code-hol-v3 ~/projects/
```

その後、Cortex Codeを起動する前にターミナルでフォルダに移動します。

### ステップ2: 環境のセットアップ

```bash
# ラボフォルダに移動
cd ~/Documents/cortex-code-hol-v3  # または移動先のパス

# Cortex Codeを起動
cortex
```

Cortex Codeで、Snowflake接続を確認：
```
利用可能なSnowflake接続を一覧表示
```

接続を追加する必要がある場合は、`/add-connection`を使用します。接続設定の詳細は[Cortex Code入門ガイド](https://docs.snowflake.com/LIMITEDACCESS/cortex-code/cortex-code-cli)を参照してください。

### ステップ2: 利用可能なスキルの確認

```
list skills
```

バンドルスキルに`semantic-view-optimization`が表示されるはずです。

### ステップ3: 会社コンテキストの読み込み

```
assets/customer-brief.mdから会社概要を読み込む
```

---

## 含まれるアセット

```
cortex-code-hol-v3/
├── README.md                           # このファイル
├── exercises/
│   ├── exercise-1-rapid-demo.md        # Cortex Analyst + Snowflake IntelligenceでPOCを構築
│   ├── exercise-2-skills.md            # スキルの使用と作成をマスター
│   └── exercise-3-documentation.md     # ステークホルダー向けドキュメントを生成
└── assets/
    ├── customer-brief.md               # 会社概要
    └── discovery-notes.md              # 経営陣との要件ミーティング議事録
```

**注:** 演習1では、会社のコンテキストに基づいてCortex CodeでPOCデータベースをゼロから生成します - 社内要件から構築する実際のシナリオをシミュレートしています。

---

## 主要コンセプト

### Cortex Analyst
AI搭載の自然言語からSQLへの変換。ユーザーが平易な英語で質問すると、Cortex AnalystがSQLを生成・実行します。

### セマンティックビュー
Cortex Analystにデータモデルを説明するレイヤー - テーブル、関係、指標、ビジネス定義を含みます。

### Snowflake Intelligence
Cortex Analystをベースに構築された対話型AIアシスタント。データ探索のためのチャットインターフェースを提供します。

### スキル
Cortex Codeに特定のタスクを完了する方法を教える、マークダウンファイルとしてパッケージ化された再利用可能なワークフローです。

---

## 成功のためのヒント

1. **適切なスキルを使用** - 手動作業の前にバンドルスキルが存在するか確認
2. **コンテキストを含める** - プロンプトに会社固有のニーズを参照
3. **反復** - 最初の出力は出発点；フォローアップで改善
4. **すべてを保存** - ステークホルダープレゼンテーション用に出力をファイルに書き込む
5. **パターンを把握** - 繰り返しワークフローをチーム用スキルに変換

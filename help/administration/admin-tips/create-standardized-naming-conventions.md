---
title: 標準化された命名規則の作成
description: 標準化された命名規則は、AA 管理 UI で有効にした場合の変数名自体と、ディメンションに渡される値の両方に適用されます。
feature: Implementation Basics
topic: Administration
role: Admin
level: Beginner
doc-type: article
thumbnail: 10531.jpg
kt: 10531
exl-id: 0fe3b981-0d9b-4f12-a6ca-63a4140f4baf
TQID: https://experienceleague.adobe.com/nnAluH2AvqNbWEPk3lbthk-xDl-tnqyW8uHg4Beurq0
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 677e5a22dab92be7ff021c8410525b9091975aef
workflow-type: tm+mt
source-wordcount: 331
ht-degree: 78%

---

# 標準化された命名規則の作成

**対象：**&#x200B;標準化された命名規則は、Adobe Analytics（AA）管理 UI で有効にした場合の変数名自体と、ディメンションに渡される値の両方に適用されます （つまり、ページ名は変数名として「ページ名（v1）」とし、渡されるページ名の値は「サイト名|ホームページ」や「サイト名|検索|検索結果」のように特定の構造と階層に従うように統一する必要があります）。

**理由：**&#x200B;命名規則は、すべてを統一し、ユーザーが理解しやすいインターフェイスを維持するための優れた方法です。 最初からこれらを作成し、プラットフォームとコードで強制すると、拡張が容易になります。

**方法：** インターフェイスとタグ付けドキュメントは、「名前」と「説明」の両方に一致する必要があります。これにより、ユーザーはExcel ドキュメントを取得する必要がなくなり、インターフェイスで直接データを理解できるようになります。 一貫性を保つため、常に小文字のみを使用することもお勧めします。

プラットフォーム全体でページ名の一貫性を保つことが常に最善です（アプリの画面名も同様です）。 例えば、`property:section:sub section:sub sub section:unique page name`を変数/ディメンションに設定できます。 これらがすべてデータレイヤーで別々のフィールドになっている場合は、JS ファイルまたは Launch で直接ページ名を作成することもできます。 これらの要素をすべて独自のディメンションに設定すると、サイトやアプリの特定のプロパティや領域をより簡単に分類し、トラフィックやフローをより深く理解できます。

命名規則のように単純なものを含め、ユーザーがデータを見つけて理解しやすくなれば、Adobe Analytics の使用率を高め、ビジネスにより有益なインサイトをもたらすことができます。

## 作成者

このドキュメントの共同作成者：

![Christel Guidon](assets/Christel-Headshot-150.png)

Christel Guidon氏（NortonLifeLock、デジタル分析プラットフォームマネージャー）
Adobe Analytics チャンピオン

![Rachel Fenwick](assets/Rachel-Fenwick-150.png)

Rachel Fenwick（アドビ のシニアコンサルタント）

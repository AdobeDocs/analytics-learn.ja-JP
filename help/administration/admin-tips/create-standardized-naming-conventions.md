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
source-git-commit: 54f9d15d705cd2d9dfa0fb177d14e2e602e35b7c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 80%

---

# 標準化された命名規則の作成

**対象：**&#x200B;標準化された命名規則は、Adobe Analytics（AA）管理 UI で有効にした場合の変数名自体と、ディメンションに渡される値の両方に適用されます（つまり、ページ名は変数名として「ページ名（v1）」とし、渡されるページ名の値は「サイト名|ホームページ」や「サイト名|検索|検索結果」のように特定の構造と階層に従うように統一する必要があります）。

**理由：**&#x200B;命名規則は、すべてを統一し、ユーザーが理解しやすいインターフェイスを維持するための優れた方法です。最初からこれらを作成し、プラットフォームとコードで強制すると、拡張が容易になります。

**方法：** 「名前」と「説明」の両方で、インターフェイスとタグ付けドキュメントが一致する必要があります。これにより、ユーザーは Excel ドキュメントを取り込む手間を省き、ユーザーがインターフェイスで直接データを把握できるようになります。 一貫性を保つため、常に小文字のみを使用することもお勧めします。

プラットフォーム全体でページ名（アプリの場合は画面名）の一貫性を保つのが常に最適です。 例えば、 `property:section:sub section:sub sub section:unique page name` を変数/ディメンションに追加します。 これらがすべてデータレイヤーで別々のフィールドになっている場合は、JS ファイルまたは Launch で直接ページ名を作成することもできます。これらの要素をすべて独自のディメンションに設定すると、サイトやアプリの特定のプロパティや領域をより簡単に分類し、トラフィックやフローをより深く理解できます。

命名規則のように単純なものを含め、ユーザーがデータを見つけて理解しやすくなれば、Adobe Analytics の使用率を高め、ビジネスにより有益なインサイトをもたらすことができます。

## 作成者

このドキュメントの共同作成者：

![Christel Guidon](assets/Christel-Headshot-150.png)

Christel Guidon（デジタル分析プラットフォームマネージャー、NortonLifeLock）
Adobe Analytics Champion

![Rachel Fenwick](assets/Rachel-Fenwick-150.png)

Rachel Fenwick（アドビ のシニアコンサルタント）

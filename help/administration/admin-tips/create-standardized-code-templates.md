---
title: 標準化されたコードテンプレートの作成
description: ベースライン実装の場合（つまり、会社がすべての Adobe Analytics サイトの必須 KPI と見なすものに対して）、可能な限り単一の実装方法を組織に用意する必要があります。
feature: Implementation Basics
topic: Administration
role: Admin
level: Beginner
doc-type: article
thumbnail: 10532.jpg
kt: 10532
exl-id: be00c8c0-a4bc-4380-98da-d1e2a3d31ec5
source-git-commit: df00d4fb8cc5093903ed4628dfe12f152294123a
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 100%

---

# 標準化されたコードテンプレートの作成

**対象：** 「ベースライン」実装の場合（つまり、会社がすべての Adobe Analytics サイトの必須 KPI と見なすものに対して）、可能な限り単一の実装方法を組織に用意する必要があります。 例えば、サイト全体で同じデータレイヤー構造を使用し、同じタグマネージャーのルール／カスタムコードを活用して、内部検索や訪問者プロファイル情報などを取り込みます。

**理由：** 繰り返し可能で拡張性の高いベースライン実装を使用すると、新しい要素や新しいサイト／アプリを追加する作業を合理化し、労力を費やすことなく、実装をクリーンでトラブルシューティングしやすくします。また、統一された方法を使用すると、新しい管理者やデベロッパーがオンライン上での作業を理解しやすくなります。

**方法：** 新規のサイトやタグ付けの強化がオンラインになった際に、デベロッパーに提供できるよう、単一形式テンプレートを採用します。 一般的に、次の項目の概要を説明できる Wordドキュメントは適切に機能します。

* 実装される変数、その目的および設定するタイミング。次に例を示します。

| AA 変数 | 説明 | 設定するタイミング／場所 | 設定方法 |
|--- |--- |--- |--- |
| eVar8 | 内部検索キーワード | 内部検索結果ページのランディング | データレイヤー |
| event8 | 内部検索のカウント | 内部検索結果ページのランディング | ローンチルール |

* 設定方法の詳細。 ここで、必要なデータレイヤーオブジェクトとその構文、設定が必要な TMS ルール、ルール設定の詳細を指定します。
* 確認するテストケースは、QA および成功したテストケースで予想されるすべての変数で説明しています。デベロッパーがこの機能強化をテストする際に、実装が成功した場合に含めるべき内容の概要を示します。

理想的には、プロパティ名、ページ命名規則などの基本事項を更新する次のサイトでは、このドキュメントを調整するだけで済みます。毎回作り直す必要がないため、時間を節約できます。

## 作成者

このドキュメントの共同作成者：

![Christel Guidon](assets/Christel-Headshot-150.png)

Christel Guidon（デジタル分析プラットフォームマネージャー、NortonLifeLock）
Adobe Analytics Champion

![Rachel Fenwick](assets/Rachel-Fenwick-150.png)

Rachel Fenwick（アドビ のシニアコンサルタント）

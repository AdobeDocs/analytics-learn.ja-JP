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
TQID: 'https://experienceleague.adobe.com/rmLhZbO6hYtpj1P0q0ZVwXglHVBC-KaHIkxyAF-7i-U'
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
    internal-label: Reports
  - id: a421fb65-2c82-457a-921c-28c46b697a39
    internal-label: Analytics basics
subfeature_v2:
  - id: c24fe15a-643a-47bd-8278-5e027df49785
    internal-label: Implementation basics
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
source-git-commit: 3e00cf9416ba2c6886e5a7efb952cac8ce370930
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 87%
---
# 標準化されたコードテンプレートの作成

**対象：** 「ベースライン」実装の場合（つまり、会社がすべての Adobe Analytics サイトの必須 KPI と見なすものに対して）、可能な限り単一の実装方法を組織に用意する必要があります。 例えば、サイト全体で同じデータレイヤー構造を使用し、同じタグマネージャーのルール／カスタムコードを活用して、内部検索や訪問者プロファイル情報などを取り込みます。

**理由：** 繰り返し可能で拡張性の高いベースライン実装を使用すると、新しい要素や新しいサイト／アプリを追加する作業を合理化し、労力を費やすことなく、実装をクリーンでトラブルシューティングしやすくします。 また、統一された方法を使用すると、新しい管理者やデベロッパーがオンライン上での作業を理解しやすくなります。

**方法：** 新規のサイトやタグ付けの強化がオンラインになった際に、デベロッパーに提供できるよう、単一形式テンプレートを採用します。 一般的には、次の項目を整理して記載できる Word ドキュメントを用意するとよいでしょう。

* 実装される変数、その目的および設定するタイミング。 次に例を示します。

| AA 変数 | 説明 | 設定するタイミング／場所 | 設定方法 |
|--- |--- |--- |--- |
| eVar8 | 内部検索キーワード | 内部検索結果ページへの到達時 | データレイヤー |
| event8 | 内部検索のカウント | 内部検索結果ページのランディング | ローンチルール |

* 設定方法の詳細。 ここで、必要なデータレイヤーオブジェクトとその構文、設定が必要な TMS ルール、ルール設定の詳細を指定します。
* QA で確実にカバーされるようにすべきテストケースと、テストが成功した場合に確認したいすべての変数を記載します。 デベロッパーがこの機能強化をテストする際に、実装が成功した場合に含めるべき内容の概要を示します。

理想的には、このドキュメントは、プロパティ名やページ命名規則などの基本を更新する次のサイトのために調整する必要があります。毎回車輪を再発明する必要はなく、より多くの時間を節約できます。

## 作成者

このドキュメントの共同作成者：

![Christel Guidon](assets/Christel-Headshot-150.png)

Christel Guidon氏（NortonLifeLock、デジタル分析プラットフォームマネージャー）
Adobe Analytics チャンピオン

![Rachel Fenwick](assets/Rachel-Fenwick-150.png)

Rachel Fenwick（アドビのシニアコンサルタント）

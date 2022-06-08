---
title: 標準化された命名規則の作成
description: AA Admin UI で有効にした場合、変数名自体とディメンションに渡された値の両方に、標準化された命名規則が適用されます。
feature: Implementation Basics
topic: Administration
role: Admin
level: Beginner
doc-type: article
thumbnail: 10531.jpg
kt: 10531
source-git-commit: 160df6c23acb67f1b07f2fcd25f1eca96eb6dee7
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---


# 標準化された命名規則の作成

**対象：** Adobe Analytics(AA) 管理 UI で有効にした場合、変数名自体と、ディメンションに渡された値の両方に、標準化された命名規則が適用されます。 ( 例：ページ名は「ページ名 (v1)」を変数名とし、渡されるページ名の値は一様で、「sitename|homepage」や「sitename|search|searchresults」のような特定の構造/階層に従う必要があります )。

**理由：** 命名規則は、すべてを統一し、ユーザーが理解しやすいインターフェイスを維持する優れた方法です。 最初からこれらを作成し、プラットフォームとコードで適用すると、拡張が容易になります。

**方法：** 「名前」と「説明」の両方で、インターフェイスとタグ付けドキュメントが一致する必要があります。これにより、ユーザーは Excel ドキュメントを取り込む手間を省き、ユーザーがインターフェイスで直接データを把握できるようになります。 一貫性を保つため、すべてを小文字に保つこともお勧めします。

プラットフォーム全体でページ名（アプリの場合は画面名）の一貫性を保つことをお勧めします。 例えば、「プロパティ」:section:サブセクション：サブセクション：一意のページ名&quot;を変数/ディメンションに追加します。 これらすべてがデータレイヤーで別々のフィールドになっている場合は、JS ファイル/Launch で直接ページ名を作成することもできます。 これらの要素をすべて独自のディメンションに設定すると、サイトやアプリの特定のプロパティや領域をより簡単に分類し、トラフィックやフローをより深く理解できます。

命名規則と同じくらい簡単なものを含め、ユーザーがデータを見つけ、理解しやすくするあらゆる要素は、Adobe Analyticsの使用率を高め、ビジネスに関するより優れたインサイトを提供します。

## 発言者

このドキュメントは次のユーザーによって共同で作成されました：

![Christel Guidon](assets/Christel-Headshot-150.png)

NortonLifeLock Adobe Analyticsチャンピオンの Digital Analytics Platform Manager、Christel Guidon 氏

![レイチェルフェンウィック](assets/Rachel-Fenwick-150.png)

レイチェル・フェンウィック、Adobeのシニアコンサルタント

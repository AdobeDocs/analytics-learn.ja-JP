---
title: グローバルレポートスイートの使用
description: 1 つのグローバルなレポートスイートにすると、様々な点で役に立ち、実装をとても簡素化できます。
feature: Implementation Basics
topic: Administration
role: Admin
level: Beginner
doc-type: article
thumbnail: 10536.jpg
kt: 10536
exl-id: 490addfd-b810-4f15-b065-e0e58048c882
source-git-commit: df00d4fb8cc5093903ed4628dfe12f152294123a
workflow-type: ht
source-wordcount: '763'
ht-degree: 100%

---

# グローバルレポートスイートの使用

**対象：**&#x200B;サイトごとにレポートスイートを作成することは魅力的ですが、レポートだけなく、実装も複雑になるため、すぐに後悔することになる可能性があります。1 つのグローバルなレポートスイートにすると、様々な点で役に立ち、実装をとても簡素化できます。

**理由：**&#x200B;デジタルプロパティ群と、各プロパティをまたいだユーザーのジャーニーを統一的に把握するためには、グローバルレポートスイートを作成することが唯一の選択肢です。モバイルアプリと web サイトがある場合、クロスデバイスジャーニーの利点を活用するには、アプリデータと web データを常に 1 つのレポートスイートにまとめる必要があります。各プロパティを訪問した人を 1 人の訪問者として把握するためです。別々のレポートスイートでは、各プロパティに 1 人ずつ（2 人の訪問者）が表示されたつながりのないデータセットとなり、クロスオーバーしていることを把握できなくなります。

レポートスイートを 1 つにすることのメリットとデメリットを次に示します。選択肢を検討する際の参考にしてください。

* 利点：
   * デジタル環境全体を理解しやすくなります。他のヒントで参照した「プロパティ」ディメンション（eVar）を実装すると、すべてのサイトとアプリ、トラフィックおよびコンバージョンをとても簡単に一覧できます。このような大きな視野を持つことは、ビジネス全体を理解する上で重要です。
   * 同じ意味で、ユーザーが各プロパティをまたいでどのように移動しているかを把握し、デジタル環境全体でのユーザーのジャーニーを理解できるようになります。
   * 管理が容易です。 複数のレポートスイートを使用する場合、複数の場所にインターフェイスを維持し、タグ付けドキュメントを複数（または複雑なドキュメントを 1 つ）を維持する必要があります。すべてを 1 箇所にまとめておくと、更新も 1 箇所で済ませることができます。また、アクセス権限の付与も非常に簡単になります。
   * インターフェイスの操作性が向上します。ユーザーの目的が 1 つだけであれば、どのレポートスイートを選択するか考える必要はありません。同じワークスペースパネル内では複数のレポートスイートを使用できないので、レポートスイートが複数あるとユーザーを混乱させる可能性があることに注意が必要です。
   * サーバーの呼び出し数が少ないほど、コストを削減できます。複数のレポートスイートに対して呼び出しを行うと、コストが増加します。実装をシンプルに保つことも、コストの抑制につながります。
   * 仮想レポートスイート（VRS）を活用すると、グローバルレポートスイート内でサイト固有のデータを分割し、必要に応じてユーザー権限を VRS に基づいて絞り込むことができます。個別のレポートスイートに分割したデータは後でまとめることはできませんが、あらかじめ 1 つに結合されたデータセット（グローバル RS）を分割することは容易です。
* 欠点：
   * 各プロパティが非常に独立していて、ユーザーが一方から他方へ移動することがなく、予想もされない場合は、別々のレポートスイートを維持することができます。
   * タグ付けとレポーティングの要件がプロパティによって大幅に異なる場合は、変更できる効率さを考慮して、レポートスイートを別々に設定することが有効な場合があります。別々のレポートスイートを持つと、カスタム変数（より多くの eVar）を柔軟に使用できます。
   * ユニーク数が超過する可能性があります。Adobe Analytics インターフェイスで表示できる一意の値は、特定の期間に対して、1 つのディメンション内で 500,000 個までです。この制限を超えると、「ユニーク数超過」または「低トラフィック」として、値はインターフェイス内でグループ化されます。これらの値は、バックエンド（Data Warehouse やデータフィード）では引き続き使用できますが、インターフェイス内で視覚化することはできません。非常に粒度の高いデータ（ユーザー ID、PSN など）がある場合は、このレベルに容易に到達します。別のレポートスイートがあると、この問題に対処できます。

**方法：**&#x200B;新しい AA の実装から始めて、1 つのグローバルレポートスイートを使用する方法は、シンプルで簡単です。AA 管理 UI でグローバルレポートスイート（開発用に 1 つ、実稼動用に 1 つ）を作成し、すべてのプロパティに同じレポートスイート ID（RSID）値を適用するだけです。

プロパティごとに個別のレポートスイートを使用しているマルチタグ付けの方針から移行する場合は、戦略と計画をよく考える必要があります。次の点に注意する必要があります。

* 変数を揃える（つまり、プロパティ A の eVar1 とプロパティ B の eVar1 は、同じデータポイントを取り込む必要があります）
* 処理ルール、マーケティングチャネルルール、分類を統合する（SAINT とルールビルダー）
* すべてのデータフィードとデータソースを移行する
* カットオーバー日を決定し、すべてのビジネスユーザーに伝える

## 作成者

このドキュメントの共同作成者：

![Christel Guidon](assets/Christel-Headshot-150.png)

Christel Guidon（デジタル分析プラットフォームマネージャー、NortonLifeLock）
Adobe Analytics Champion

![Rachel Fenwick](assets/Rachel-Fenwick-150.png)

Rachel Fenwick（アドビ のシニアコンサルタント）
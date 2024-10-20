---
title: カスタマージャーニーセグメントの作成
description: このステップバイステップのガイドに従って、Adobe Analyticsで行動ベースのカスタマージャーニーセグメントを作成し、Adobe Experience Cloudでのカスタマーエクスペリエンス（顧客体験）を向上させる方法を説明します。
feature: Segmentation
role: User
level: Experienced
doc-type: Article
last-substantial-update: 2023-05-02T00:00:00Z
jira: KT-13180
thumbnail: KT-13180.jpeg
exl-id: c06afc7b-e997-404d-82a4-e7ec5d5ba44d
source-git-commit: d95136a21c08312a81baba7673cb7135270af4bd
workflow-type: tm+mt
source-wordcount: '1243'
ht-degree: 1%

---

# カスタマージャーニーセグメントの作成

このステップバイステップのガイドに従って、Adobe Analyticsで行動ベースのカスタマージャーニーセグメントを作成し、Adobe Experience Cloudでのカスタマーエクスペリエンス（顧客体験）を向上させる方法を説明します。

より優れたカスタマージャーニーセグメントを作成しましょう。 このシリーズでは、Adobe Analyticsを使用して、行動ベースのセグメントを定義し、オーディエンスサイズを推定し、ユーザーの動きを追跡します。 最終的には、Adobe Experience Cloudでメディアをパーソナライズし、顧客体験を向上させることができます。 これらのセグメントは常に有効で、顧客の詳細を把握する際は更新する必要があります。 レポート作成にはいくつかの課題があるかもしれませんが、心配しないでください。ガイドをさせていただきます。 まず、「ワンヒットの驚異」セグメントから始まる、最初のカスタマージャーニーセグメントを作成します。

今日は、お客様ジャーニーセグメントの最初のセットのプレースホルダーを作成し、Adobe Analytics Workspaceを作成してセグメントの定義を支援し、最初のセグメントである「ワンヒットの驚異」を定義します。

このシリーズを終了すると、行動シグナルに基づいてAdobe Analyticsでカスタマージャーニーセグメントを作成できるようになります。 ジャーニーの各ステージでの各オーディエンスのサイズを推定し、ユーザーがこれらのステージ間をどのように移動したかを理解できます。 また、これらのカスタマージャーニーオーディエンスをAdobe Experience Cloudに書き出して、パーソナライゼーションとメディアターゲティングを有効にすることができます。

ビジネスはそれぞれ異なり、カスタマージャーニーセグメントは実際のセグメントとは異なって見えます。 したがって、セグメントに特定の数式を規定するのではなく、いくつかの考慮事項と、それらを構築するための全体的なプロセスを提案します。

また、カスタマージャーニーセグメントは、ライブセグメントであることに注意する必要があります。 これは 1 回きりの演習ではありません。 顧客に関する詳細を理解したら、これらのセグメントを更新しましょう。 これは、レポートに関するいくつかの課題を示しています。 人々はレポートの一貫性を求めています。セグメント定義が変更されると、レポートの数値も変更されます。

## 訪問インテントセグメントの概要

カスタマージャーニーセグメントを作成する最初の手順は、行動シグナルと、利用可能な場合は顧客の声データを使用して、ゲストが web サイトにアクセスしている理由を推測することです。 Web サイト上のすべての訪問を分類するための一連の訪問インテント セグメントを作成します。 この時点で、訪問意図セグメントは相互に排他的で、完全に完全である必要があります。 すべての訪問は、訪問インテント セグメントに属する必要があり、1 つだけである必要があります。

訪問の意図セグメントは訪問を記述するので、セグメント定義で訪問コンテナを使用します。

最初の訪問インテントセグメントには、次のセットが含まれています。

* ワンヒット不思議
* 認識
* 考慮事項
* 予約（購入）
* 保持（予約/購入の管理）

訪問インテントセグメントを使いやすくするために、セグメント名の前に「Intent:」を付け、並べ替えを有効にする番号を付け、「intent」というタグを付けました。 セグメントは下の図のようになります。

![ インテントセグメント ](assets/intent-segments.png)

**ページビュー >= 1 のプレースホルダー定義を含んだ訪問コンテナを使用して、訪問インテントセグメントを作成します**。

これからわかるように、これらのセグメントを構築することは、反復され相互に関係し合ったプロセスです。 今後の投稿で、これらのセグメントを作成するプロセスについて説明します。

## 訪問インテント セグメントのデータ品質Workspace

![ 訪問インテントワークスペース ](assets/visit-intent-workspace.png)

訪問インテントセグメントを適切に定義していることを確認するために、シンプルなワークスペースを使用しました。 各訪問は、1 つの訪問インテントセグメントに属する必要があり、1 つのみであることに注意してください。 設定したワークスペースにより、すべての訪問が考慮され、セグメント間で重複が発生しないようにします。

私はこのワークスペースを「データ品質：訪問の意図セグメント」と名付け、「データ品質」、「訪問の意図」、「カスタマージャーニー」というタグを付けました。 後で、「訪問インテントダッシュボード」を作成します。プレフィックス「DATA QUALITY」は、このワークスペースがセグメントの設定と保守のためのものであることを示します。 これは、ビジネスに関するインサイトがほとんどない管理ダッシュボードですが、セグメントを確実に維持するために重要です。 セグメントが正しく定義されていることを確認するために、定期的にこのダッシュボードに戻るか、アラートを設定することをお勧めします。

このワークスペースで最も重要なビジュアライゼーションは、左中央のセグメントの重複フリーフォームビジュアライゼーションです。 訪問指標を使用して、各訪問インテント セグメントの列フィルターに加え、右端の列にすべての訪問セグメントを作成します。 左側に、各訪問インテント セグメントの行を作成します。 これで、クロスタブビジュアライゼーションが作成されました。 セグメントが正しく設定されると、各訪問インテント セグメントとそれ自体の積集合に、1 列と 1 行のデータのみが表示されます。

次に重要なビジュアライゼーションは、左上の概要指標です。 セグメント化された訪問の概要は、のすぐ下にあるセグメント重複ビジュアライゼーションのすべての訪問列から値を取得します。 すべての訪問の概要には、独自の非表示テーブルがあります。

![ すべての訪問 ](assets/all-visits.png)

右上では、各セグメントに指標を追加して、セグメントの形成の仕方に「風味」を付けました。 特に、これらのセグメントは相互に排他的なので、予約インテントセグメントの予約のみが表示されると期待しています（ただし、これらの訪問インテントセグメントを訪問者ベースにすると、コンバージョン率が表示されます）。

プレースホルダーセグメントを作成しました。 したがって、最初はワークスペースが異常に見えます。 定義が同じなので、すべての訪問インテントセグメントが 100% 重複します。 これは正しく、プロセスのこの時点で確認したいものです。 セグメント定義を作成すると、これらのセグメントが形成され始めることがわかります。

![ 訪問インテントセグメントの定義 ](assets/visit-intent-segment-defs.png)

## 最初の訪問インテントセグメントの作成

訪問インテントのセグメントを定義することは、根絶プロセスの一部であり、それらの間には多くの相互依存関係があります。 したがって、これらのセグメントはジャーニーの順序に従って作成するのではなく、定義が最も簡単なものから、最も困難なものの順に作成しました。 それは私に次の命令を与えてくれた。

1. 意図：0 - 1 ヒットの驚異
1. インテント：3 – 予約
1. インテント：4 - リテンション
1. インテント：2 – 考慮事項
1. インテント：1 – 認識

ランダムか？ これらの訪問の意図を示すセグメントを定義することは、反復的で前後のプロセスであり、多くの場合、あるセグメントを調整するには他のセグメントを更新する必要がありました。 これは、私がこれらの各セグメントをどのように定義したかを説明する際に、より明確になります。

今日は、最初で最も簡単なセグメント「ワンヒットの驚異」を定義します

## 「ワンヒット・ワンダーズ」セグメントの構築

私の最初のセグメント「ワンヒット・ワンダーズ」は定義が簡単でした。 ページビューが 1 つだけの訪問にすぎません。 そのユーザーがバウンスしたので、そのユーザーが web サイトにアクセスした理由は本当にはわかりません。 エントリページから意図を推測できると思いますが、1 ページ表示では、意図を十分に推測するのに十分な情報がありません。

![ セグメント定義 ](assets/segment-def.png)

このセグメントを定義すると、訪問インテントWorkspaceが具体化していくのを確認できます。

![ その他のセグメント定義 ](assets/more-segment-defs.png)

Adobe Analyticsを使用してカスタマージャーニーセグメントを作成するプロセスは、困難ではあるが、やりがいがあります。 行動ベースのセグメントを作成し、オーディエンスサイズを予測し、ユーザーの動きを追跡することで、企業はメディアをパーソナライズし、顧客体験を向上させることができます。 各ビジネスは一意で、セグメントを作成するための特定の数式はありませんが、ガイドラインと従うプロセスがあります。 レポートの課題を抱えている企業が顧客についてより詳しく知るには、セグメントを更新する必要があります。 訪問インテント セグメントを構築するプロセスに従うことで、企業は全体的な顧客体験を向上させることができます。

## 作成者

このドキュメントの作成者：

![ アーロン・フォッサム ](assets/aaron-headshot.png)

**Aaron Fossum**、Director、デジタル分析

Adobe Analytics チャンピオン

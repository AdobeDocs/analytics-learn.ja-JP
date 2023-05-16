---
title: セグメントを待つだけです。セグメント化を使用して、Analysis Workspaceで新しいインサイトを見つけます
description: Adobe Analyticsでセグメントを使用して、Analysis Workspaceのビジュアライゼーションとフリーフォームテーブルから新しいインサイトを見つける方法を説明します。
feature: Segmentation
role: User
level: Beginner
doc-type: Article
last-substantial-update: 2023-05-16T00:00:00Z
jira: KT-13268
thumbnail: KT-13268.jpeg
source-git-commit: b11a329ca3f5c676aea08c7037e5ee87003edfe6
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 6%

---


# セグメントを待つだけです。セグメントを使用して、Analysis Workspaceで新しいインサイトを見つけます

新規のAdobe Analyticsユーザーであれ、ベテランのプロであれ、Analysis Workspaceプロジェクトでセグメントを大きく活用できます。 形式 [Adobe Experience League](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html?lang=ja) は、「セグメントを使用すると、特性や Web サイトでのインタラクションに基づいて訪問者のサブセットを識別できます」を表しています。 この機能の基本的な結果は、サイトへのユーザー、訪問回数、ヒット数のグループを分離することですが、自分などの鋭い意識を持つアナリストは、このツールを使用してクリエイティブになり、サイトのアクティビティに関する新しい洞察を得ることができます。 選択可能なオプションのリストは広大なので、自分で作成し、組織の他の人や、 [Adobe Analytics Community](https://experienceleaguecommunities.adobe.com/t5/adobe-analytics/ct-p/adobe-analytics-community?profile.language=ja) Experience League、または [#MeasureSlack](https://www.measure.chat/) コミュニティ

セグメントの作成方法に関するクイックリファレンスが必要な場合は、 [セグメントビルダー](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-build.html?lang=en) Analysis Workspace

## セグメントの比較と対照

Analysis Workspaceでは、「[セグメント比較](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/segment-comparison/segment-comparison.html?lang=ja)&quot;. セグメント比較は、左側のナビゲーションバーの「パネル」セクションにあります。

![Seg 01](assets/seg01.png)

ただし、主要なインサイトをエンドユーザーに提供するために、完全な比較パネルが必要ない場合があります。 ありがたいことに、一部の機能は標準パネルでも比較できます。

この [ベン図のビジュアライゼーション](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/venn.html?lang=ja) は、すばやく比較を作成する際に役立ち、重なり合うセッション、注文、ユーザーなどを 2 ～ 3 のカスタムセグメント 重なり合う任意のセクションを右クリックして、セグメントをすばやく作成することもできます。

![Seg 02](assets/s02.png)

重要な情報が重複するデータに含まれていないのに、重複しないデータに含まれる場合があります。 これを簡単に表示するには、1 つのセグメントのコピーを作成して、それを「除外」セグメントにします。

![Seg 03](assets/s03.png)

「除外」セグメントと他のセグメントを比較で積み重ねることで、同じセッションでホームページを表示することなく、メニューページをヒットした訪問数を簡単に計算できるようになりました。

![Seg 04](assets/s04.png)

## スタック攻撃

同様に、任意のセグメントを積み重ねるだけで、ベン図の交差するデータを作成できます。 積み重ねるセグメント数や個々のディメンション数に制限はありません。 例えば、先月、私のサイトが携帯電話、特に Samsung Galaxy A52s を訪問し、私のメニューと栄養ページを見たが、私のホームページを見なかった場合、私は次のようにすぐにそれを構築することができます：

![Seg 05](assets/s05.png)

さらに、ユーザーまたは訪問ベースの完全なサブセットが見つかったら、これらの値をすべて選択し、右クリックして、セグメントを即座に作成できます。

![Seg 06](assets/s06.png)

![Seg 07](assets/s07.png)

![Seg 08](assets/s08.png)

1 つのセグメントで大きな力を発揮します

## セグメント数のセグメント

多くのユーザーは、セグメントの作成時に、名目、序数、または間隔の値を調べます。例えば、訪問したページ、ユーザーの年齢範囲、過去にユーザーがおこなった訪問回数などです。 ただし、組織の標準ディメンション、標準指標、カスタム変数および指標のどれであるかに関わらず、これらの値をグループ化してセグメントを作成する際にも、比率データを使用できます。

例えば、ページでの滞在時間や訪問別滞在時間には、使用可能な事前定義済みのグループがあります。

![Seg 09](assets/s09.png)

ただし、これらは必ずしも組織のニーズに合わない場合があります。おそらく、サイトの訪問のほとんどが 10 分未満になるかもしれません。 粒度の指標を使用して、異なるサイズのグループを作成できます。 以下に、1 分、1 秒、1 分、30 秒の間の最後の訪問数を調べるために作成された値を示します。

![Seg 10](assets/s10.png)

作成したら、カスタマイズした様々なグループの訪問、注文、その他のイベントを確認できるようになります。

![Seg 11](assets/s11.png)

主要業績評価指標 (KPI) の変化を、ユーザーの滞在時間、訪問でのヒットページ数、過去に訪問した回数などの数値の要因として調べることもできます。基本的に、指標を別の指標の要素として見ることができます。

![Seg 12](assets/s12.png)

セグメントを使用して新しいインサイトを見つける方法は、無限です。 これは単なる出発点です。 自分でいくつか試して、コミュニティに何を発見したか知らせてください。 [Adobe Analytics Community](https://experienceleaguecommunities.adobe.com/t5/adobe-analytics/ct-p/adobe-analytics-community?profile.language=ja) Experience League、または [#MeasureSlack](https://www.measure.chat/) コミュニティ

幸せなセグメント化！

## 作成者

このドキュメントの作成者：

![ダン・カミングス](assets/seg13.png)

**ダン・カミングス**, McDonald&#39;s Corporation の Sr. Product Engineering Analytics Manager

Adobe Analytics チャンピオン


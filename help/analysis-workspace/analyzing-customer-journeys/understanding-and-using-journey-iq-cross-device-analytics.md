---
title: ジャーニー IQ の理解と使用 - クロスデバイス分析
description: ユーザーがブランドとやり取りする際は、様々な方法や複数のデバイスで行います。クロスデバイス分析は Adobe Experience Platform ID サービスと統合して、デバイスが人物にどのようにマッピングされるかを識別します。次に、このインテリジェンスを活用して、ユーザーの行動のクロスデバイス表示を作成します。その結果、デバイスではなく人物に対して分析を行うことができるようになります。
feature: CDA
topics: null
activity: use
doc-type: article
team: Technical Marketing
kt: 4138
role: User
level: Intermediate
exl-id: 3748d5d7-d250-4057-8131-afdc66c80200
source-git-commit: 01e6e84f748e359aeb42c9be3afa52088f41018b
workflow-type: tm+mt
source-wordcount: '1466'
ht-degree: 100%

---

# [!DNL Journey IQ] の理解と使用 - クロスデバイス分析

ユーザーがブランドとやり取りする際は、様々な方法や複数のデバイスで行います。クロスデバイス分析は [!DNL Adobe Experience Platform Identity Service] と統合して、デバイスが人物にどのようにマッピングされるかを識別します。次に、このインテリジェンスを活用して、ユーザーの行動のクロスデバイス表示を作成します。その結果、デバイスではなく人物に対して分析を行うことができるようになります。

## クロスデバイス分析の概要

### 自分のデバイスではない

ユーザーは、様々な方法や複数の「サーフェス」または「デバイス」でブランドとやり取りします。PC やモバイルデバイスで web ブラウザーを使用する場合もあれば、モバイルアプリを使用する場合もあります。cookie に基づくデータ収集で成長した従来のデジタル分析では、これらの各サーフェスは一意の「訪問者」として表されます。つまり、各人のユーザーは複数のユニーク訪問者として表されます。

次に例を示します。Isabelle が次のようにブランドとやり取りしたとします。

*Isabelle を 3 人の訪問者してカウント*
![従来の Analytics ジャーニー](assets/cda-isabelle-journey-traditional-analytics.png)

従来の分析を使用すると、Isabelle のジャーニーは 3 つの部分に分割されます。彼女は異なるデバイスを使用して孤立したタスクを実行する、3 人のユニーク訪問者として表されます。必要なのは、Isabelle のやり取りの、統一されたクロスデバイス表示です。[!DNL Journey IQ: Cross-Device Analytics] は、この表示を提供します。

*Isabelle を 1 人のユーザーとしてカウント*
![クロスデバイス分析ジャーニー](assets/cda-isabelle-journey-cross-device-analytics.png)

### クロスデバイス表示により、分析が向上

Isabelle の行動をユーザーを中心としたクロスデバイス表示にすることで、分析に大きな違いをもたらすことができます。例えば、従来の訪問者ベースのアプローチでは、マーケティングチャネルの有効性の全体像を把握することはできません。Isabelle の製品表示と購入に対し、どのチャネルにクレジットを割り当てられたかに注目して、彼女のジャーニーをもう一度見てみましょう。わかりやすくするために [!UICONTROL ラストタッチ] アトリビューションを使用しますが、Isabelle の行動を個別の訪問者に分割した場合は、アトリビューションモデルを使用しても同じ問題が発生します。従来の訪問者ベースの世界観を使用すると、非常に異なる、さらには誤解を招く結果が導かれます。

*従来の Analytics とクロスデバイス分析の比較*
![チャネルアトリビューション](assets/channel-attribution.png)

クロスデバイス表示では、メールチャネルは、製品表示と購入の両方のクレジットを受け取ります。これは、Isabelle の実際のエクスペリエンスをより正確に表しています。

次の情報をお読みください。

* [!DNL Cross-Device Analytics] のしくみ
* [!DNL Cross-Device Analytics] の前提条件
* クロスデバイスデータの解釈
* Analysis Workspace でのクロスデバイスデータの分析

## [!DNL Cross-Device Analytics] のしくみ

[!DNL Journey IQ: Cross-Device Analytics (CDA)] は、[!DNL Adobe Experience Platform Identity Service] と統合され、[!DNL Device Graph] を利用して、デバイスが人物にどのようにマッピングされるかを識別します。次に、このインテリジェンスを活用して、ユーザーの行動のクロスデバイス表示を作成します。CDA には、企業がマルチデバイスの使用法と、ブランドとのやり取りにおけるマルチデバイス全体のカスタマーエクスペリエンスを理解するのに役立つ、比類のない機能とツールが含まれています。Analysis Workspace の下のレイヤーとして機能し、[!UICONTROL フォールアウト]、[!DNL Flow]、[!DNL Cohort]、[!DNL Segment IQ]、[!DNL Attribution IQ] などの強力なツールを使用して、ユーザーベースのオーディエンス分析とクロスデバイスアトリビューション、セグメンテーション、ジャーニー分析に関する深いインサイトを提供します。

### [!DNL Cross-Device Virtual Report Suite]

CDA は、特別な種類のクロスデバイス [[!UICONTROL 仮想レポートスイート]](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-about.html?lang=ja) を通じて提供されます。これにより、組織にクロスデバイス分析を導入する際に、元のデバイスベースのレポートスイートを引き続き使用できます。CDA VRS の設定は簡単です。

VRS ビルダーの手順 1 で、アドビによって CDA 対応として設定された [!UICONTROL レポートスイート] を選択します。

*CDA 対応のベース（ソース） [!UICONTROL レポートスイート]*を選択する
![[!UICONTROL 仮想レポートスイート] 手順 1](assets/cda-vrs-step-one.png)

次に、「[!UICONTROL レポート時間処理]」をオンにして、 [!UICONTROL クロスデバイススティッチング] を有効にします。

*[!UICONTROL レポート時間処理] と [!UICONTROL クロスデバイススティッチング]* を有効にする 
![[!UICONTROL 仮想レポートスイート] 手順 2](assets/cda-vrs-step-two.png)

VRS の設定を完了し、保存します。CDA VRS は、次に示すように、Analysis Workspace に表示され、その横に特別なアイコンが表示されます。

*Analysis Workspace で CDA VRS を選択する*
![[!UICONTROL 仮想レポートスイート] 手順 3](assets/cda-vrs-step-three.png)

>[!TIP]
>
>CDA 対応のベース [!UICONTROL レポートスイート] の上に、必要な数の CDA [!UICONTROL 仮想レポートスイート] を作成できます。

### 履歴の再記述

ユーザーがログインし、[!DNL Device Graph] がユーザーを識別してデバイスをマッピングするのに時間がかかる場合があります。CDA では 30 日間のルックバックウィンドウを利用して、以前は識別されていなかった訪問者を、最大過去 30 日までユーザーとして再表示できるようにします。

これはどのように役立つでしょうか。上記のディスカッションから Isabelle のユーザージャーニーを思い出してください。

![[!DNL Cross-Device Analytics] ジャーニー](assets/cda-isabelle-journey-cross-device-analytics.png)

Isabelle が購入の直前までログインしなかった可能性があり、[!DNL Device Graph] が購入後のある時点まで Isabelle のデバイスを一緒にマッピングしなかった可能性があります。しかし、CDA では 30 日間のルックバックによって Isabelle の過去の行動を個人レベルで再表示でき、必要な Isabelle のジャーニーのクロスデバイス表示を提供します。

>[!NOTE]
>
>履歴を再表示できるため、CDA 対応の [!UICONTROL 仮想レポートスイート] でデータが時間の経過とともに変化する可能性があります。CDA ベースの分析からのインサイトを伝えるときは、このことを念頭に置いてください。

## [!UICONTROL クロスデバイス分析] の前提条件

CDA は [[!DNL Analytics Ultimate]](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-analytics.html) に含まれています。2019年9月以降、以下の前提条件を満たしている [!DNL Analytics Ultimate] のお客様は CDA を使用する資格があります。CDA の前提条件を次に示します。

* 会社は [!DNL Adobe Experience Platform Identity Service Device Graph] を使用する必要があります。
* [Experience Cloud ID（ECID）](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ja)やグラフとの ID 同期など、[!DNL Device Graph] に必要なすべてを実装する必要があります。
* 現在、単一の [!DNL Device Graph] で 2 つの IMS 組織を使用することはできないので、単一の IMS 組織で標準化する必要があります。
* [!DNL Device Graph]、および CDA の特定のコンポーネントは、[!DNL Microsoft Azure] でホストされます。つまり、[!DNL Analytics] データがアドビのデータ処理センターとアドビの [!DNL Microsoft Azure] でのプレゼンスの間で相互にコピーされます。一部の [!DNL Analytics] データは [!DNL Azure] に保存されます。会社はこの取り決めに同意する必要があります。
* CDA には、「クロスデバイス」 [!UICONTROL レポートスイート] が必要です。つまり、CDA に使用する [!UICONTROL レポートスイート] には、複数の異なるデバイスタイプまたは「サーフェス」（デスクトップ web、モバイル web、モバイルアプリなど）からのデータが含まれている必要があります。2019年9月の時点で、この [!UICONTROL レポートスイート] のサーバーコールのボリュームは 1 日あたり 1 億サーバーコール以下である必要があります（サーバーコールボリュームの制限は、今後数か月で増加します）。 

## クロスデバイスデータの解釈

### 訪問者ではない人物

CDA [!UICONTROL 仮想レポートスイート] 内には、いくつかの変更があります。例えば、 [!UICONTROL ユニーク訪問者] 指標は、 [!UICONTROL 人物] と [!UICONTROL 一意のデバイス] の 2 つの新しい指標に置き換えられます。これらの新しい指標を使用すれば、オーディエンスのサイズに関するより良いインサイトが得られます。

*人物と一意のデバイス*
![CDA [!UICONTROL 人物指標]](assets/cda-people-metric.png)

[[!UICONTROL セグメントビルダー]](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-build.html?lang=ja)では、 [!UICONTROL 訪問者] セグメントコンテナが [!UICONTROL ユーザー] セグメントコンテナに置き換えられました。CDA VRS を使用すると、次のようなクロスデバイスセグメントを作成できます。

* 複数のデバイスを使用する人物
* モバイルデバイスでジャーニーを始め、後でデスクトップデバイスで購入する人物
* 人物が複数のデバイスを使用してタスクを遂行する訪問

*ユーザーレベルのセグメント*
![[!DNL Segment Builder] [!UICONTROL ユーザー]コンテナ](assets/cda-segment-builder-person-container.png)

### ディメンションの永続性

CDA VRS 内で、[!DNL eVars] などのディメンションがデバイス間で自動的に保持されるようになりました。例えば、[!DNL eVar] は次のように設定されています。

* 配分：最新（最後）
* 有効期限：購入

これで、購入イベントが発生するまで、あるデバイスから別のデバイスに自動的に保持されるようになりました。

## Analysis Workspace でのクロスデバイスデータの分析

### ユーザーベースのオーディエンス分析

自社ブランドとやり取りをしているユーザーの数を知りたいと思ったことはありませんか。それらのユーザーが使用しているデバイスの数と種類を把握したいと思ったことははありませんか。ユーザーの使用状況はどのように重なっていますか。CDA VRS を使用すると、デバイス間の [ベン図](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/venn.html?lang=ja) とユーザーあたりのデバイスの [ヒストグラム](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/histogram.html?lang=ja) を作成できます。

*ユーザーベースのオーディエンス分析*
![ベン図とヒストグラム](assets/cda-venn-and-histogram.png)

### クロスデバイス [!DNL Flow]

CDA と Analysis Workspace を使用すると、ユーザーが時間とともに、あるデバイスから別のデバイスにどのように移動しているかを [[!DNL Flow visualization]](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/flow/flow.html?lang=ja) で視覚化できます。ユーザーがジャーニーのどこで離脱し、どこで継続するかを確認することができます。

CDA を使用した *[!DNL Flow]*
![[!DNL Flow Visualization]](assets/cda-flow-viz.png)

### クロスデバイス [!DNL Fallout]

いくつかの [[!DNL Fallout visualizations]](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/fallout/fallout-flow.html?lang=ja) を使用して、成功を収める前に、ユーザーが特定の一連の手順をどの程度うまく実行しているかを分析する可能性があります。従来のデバイスベースの分析を使用すると、これらの [!DNL Fallout visualizations] の表示が制限されることをご存知ですか？「フォールスルー」を正常に行うには、次の手順を前の手順と同じブラウザーまたはアプリで実行する必要があります。デバイスベースの分析では、別のデバイスで次の手順を正常に完了したユーザーが誰かはわかりません。

ご安心ください。CDA がこれを可能にします。CDA は、[!DNL Fallout visualizations] をはるかに便利にするクロスデバイス表示を作成します。結局のところ、本当に重要なのは、そのユーザーが最終的にどこかで自分のタスクに成功したかどうかです。

CDA を使用した *[!DNL Fallout]*
![[!DNL Fallout Visualization]](assets/cda-fallout-viz.png)

### [!DNL Cross-Device Attribution IQ]

CDA は Analysis Workspace の下にクロスデバイスデータのレイヤーを作成するため、すべての分析にはクロスデバイスの観点が追加されます。強力な例の 1 つに、[[!DNL Attribution IQ]](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution/attribution.html?lang=ja) を通じたものがあります。Analysis Workspace の [!DNL Attribution IQ] を使用すると、複数のアトリビューションモデルを並べて比較できます。この機能を CDA で使用すると、様々なデバイスが成功にどのように貢献しているかを比較できます。

例えば、最終的に成功につながるやり取りで使用された最初のデバイスが携帯電話であった頻度を把握したいとします。これは、携帯電話の「獲得率」を表します。CDA と [!DNL Attribution IQ] を使用すると、次の分析を行うことができます。

CDA を使用した *[!DNL Attribution IQ]*
![[!DNL Attribution IQ]](assets/cda-attribution-iq.png)

詳しくは、[[!DNL Cross-Device Analytics] ヘルプドキュメント](https://experienceleague.adobe.com/docs/analytics/components/cda/cda-home.html?lang=ja) を参照してください。

---
title: ジャーニーIQの理解と使用 — デバイス間分析
description: ユーザーはブランドとやり取りする際、様々な方法や複数のデバイスでやり取りします。 デバイス間の分析は、Adobe Experience PlatformIDサービスと統合され、デバイスと人との対応付け方法を識別します。 その後、このインテリジェンス機能を活用して、デバイス間でのユーザー行動の表示を作成します。 その結果、デバイスではなく人に対して分析を行うことができます。
feature: CDA
topics: null
activity: use
doc-type: article
team: Technical Marketing
kt: 4138
role: Business Practitioner
level: Intermediate
translation-type: tm+mt
source-git-commit: f3b3fa7d91b0cb21005b57768ca23ed6700fcc03
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 6%

---


# [!DNL Journey IQ]の理解と使用 — デバイス間の分析

ユーザーはブランドとやり取りする際、様々な方法や複数のデバイスでやり取りします。 デバイス間の分析は、[!DNL Adobe Experience Platform Identity Service]と統合して、デバイスと人との対応付け方法を特定します。 その後、このインテリジェンス機能を活用して、デバイス間でのユーザー行動の表示を作成します。 その結果、デバイスではなく人に対して分析を行うことができます。

## デバイス間分析の概要

### 自分は自分の装置ではない

ユーザーがブランドとやり取りする際には、様々な方法で、また複数の「サーフェス」や「デバイス」で行います。 PCやモバイルデバイスでWebブラウザーを使用する場合や、モバイルアプリを使用する場合があります。 cookieに基づくデータ収集で育った従来のデジタル解析では、これらの各サーフェスは一意の「訪問者」として表されます。 つまり、各人間ユーザーは、複数の個別訪問者として表されます。

次に例を示します。 Isabelleが次のようにブランドとやり取りしたとします。

*イザベルは3人の*
![訪問者です。従来のAnalyticsジャーニー](assets/cda-isabelle-journey-traditional-analytics.png)

従来の解析を使用して、イザベルのジャーニーは3つに分割されます。 彼女は3人のユニークな訪問者として表され、それぞれ異なるタスクを使用して隔離されたデバイスを実行しています。 必要なのは、イザベルのやり取りの統合されたデバイス間表示です。 [!DNL Journey IQ: Cross-Device Analytics] にこの表示を示します。

*Isabelleは、1人の*
![personCross-Device Analyticsジャーニーです](assets/cda-isabelle-journey-cross-device-analytics.png)

### デバイス間の表示による解析の改善

人間中心のクロスデバイス表示のIsabelleの行動は、分析に大きな影響を与えます。 例えば、従来の訪問者ベースのアプローチでは、マーケティングチャネルの効果について完全な実態を示すわけではありません。 イザベルのジャーニーを見てみましょう。チャネルが商品表示と購入のクレジットを受け取ることに焦点を当てています。 簡単にするために[!UICONTROL ラストタッチ]アトリビューションを使用しますが、同じ問題が発生するのは、Isabelleの動作を別々の訪問者に分割する場合です。 従来の訪問者ベースの表示を使用した世界は、大きく異なる、誤解を招く結果をもたらします。

*従来のAnalyticsとデバイス間の*
![分析チャネルアトリビューション](assets/channel-attribution.png)

デバイス間の表示を使用すると、電子メールチャネルは製品の表示と購入の両方のクレジットを受け取ります。これは、Isabelleの実際の経験をより正確に表します。

読み続けて学習：

* [!DNL Cross-Device Analytics]の仕組み
* [!DNL Cross-Device Analytics]の前提条件
* デバイス間データの解釈
* Analysis Workspaceでのデバイス間データの分析

## [!DNL Cross-Device Analytics]の仕組み

[!DNL Journey IQ: Cross-Device Analytics (CDA)] またはを使用して、デバイス [!DNL Adobe Experience Platform Identity Service]と人とのマッピング方法を識別するた [[!DNL Co-op Graph]](https://docs.adobe.com/content/help/ja-JP/device-co-op/using/home.html) め [!DNL Private Graph] に、と統合されます。その後、このインテリジェンス機能を活用して、デバイス間でのユーザー行動の表示を作成します。 CDAには、マルチデバイスの使用状況や、ブランドとのインタラクションに関する顧客体験を企業が把握できるように、他に類を見ない機能やツールが含まれています。 これは、[!UICONTROL フォールアウト]、[!DNL Flow]、[!DNL Cohort]、[!DNL Segment IQ]、[!DNL Attribution IQ]などの強力なツールを使用して、個人ベースのオーディエンス分析とデバイス間のアトリビューション、分類、ジャーニー分析を深く洞察するために、Analysis Workspaceの下の層に配置されています。

###   [!DNL Cross-Device Virtual Report Suite]

CDAは、特別な種類のクロスデバイス[[!UICONTROL 仮想レポートスイート]](https://docs.adobe.com/content/help/ja-JP/analytics/components/virtual-report-suites/vrs-about.html)を通じて提供されます。 これにより、デバイス間の分析を導入する際に、元のデバイスベースのレポートスイートを引き続き使用できます。 CDA VRSの設定は簡単です。

VRSビルダーの1つ目の手順で、AdobeがCDA対応として設定した[!UICONTROL レポートスイート]を選択します。

*CDA対応のベース（ソース） [!UICONTROL レポートスイートの選択仮想レポート]*
![[!UICONTROL スイート] ステップ1](assets/cda-vrs-step-one.png)

次に、[!UICONTROL レポート時間処理]をオンにし、[!UICONTROL デバイス間のステッチ]を有効にします。

*レ [!UICONTROL ポート時間の] 処理と [!UICONTROL デバイス間の]*
![[!UICONTROL 切り替えを有効にする仮想レポートスイート] ステップ2](assets/cda-vrs-step-two.png)

VRSの設定を終了し、保存します。 CDA VRSは、次に示すように、Analysis Workspaceに特別なアイコンと共に表示されます。

*分析WorkspaceVirtual Report*
![[!UICONTROL SuiteのCDA VRSを選択します。] 手順3](assets/cda-vrs-step-three.png)

>[!TIP]
>
>CDA [!UICONTROL 仮想レポートスイート]は、CDA対応のベース[!UICONTROL レポートスイート]の上に、必要な数だけ作成できます。

### 履歴の再利用

ユーザーがログインし、[!DNL Co-op Graph]や[!DNL Private Graph]がユーザーを識別してデバイスをマッピングするのに時間がかかる場合があります。 CDAは30日間のルックバックウィンドウを利用して、以前は不明だった訪問者を、過去30日間までの人物として再認証できます。

これはどう役に立ちますか？ 上のディスカッションからIsabelleのユーザジャーニーを思い出してください。

![[!DNL Cross-Device Analytics] ジャーニー](assets/cda-isabelle-journey-cross-device-analytics.png)

Isabelleは購入直前までログインせず、[!DNL Co-op Graph]や[!DNL Private Graph]は購入後しばらくの間、イザベルのデバイスをマッピングしなかった可能性があります。 しかしCDAの30日間の振り返りにより、CDAは個人レベルでイザベルの過去の行動を再び伝えることができ、必要なジャーニーのクロスデバイス表示を提供できます。

>[!NOTE]
>
>履歴は再記述できるので、CDA対応の[!UICONTROL 仮想レポートスイート]では、データが時間の経過と共に変更される可能性があります。 CDAベースの分析からインサイトを伝える際は、この点に注意してください。

## [!UICONTROL デバイス間分析]の前提条件

CDAは[[!DNL Analytics Ultimate]](https://helpx.adobe.com/legal/product-descriptions/adobe-analytics.html)に含まれています。 2019年9月以降、以下に示す前提条件を満たす[!DNL Analytics Ultimate]のお客様は、CDAを使用する資格があります。 CDAの前提条件は次のとおりです。

* 会社は、[!DNL Adobe Experience Platform Identity Service] [[!DNL Co-op Graph]](https://docs.adobe.com/content/help/en/device-co-op/using/home.html)のメンバであるか、または[!DNL Adobe Experience Platform Identity Service Private Graph]を使用する必要があります。
* [Experience CloudID (ECID)](https://docs.adobe.com/content/help/ja-JP/id-service/using/home.html)とグラフとの同期IDを含む、[!DNL Co-op Graph]または[!DNL Private Graph]に必要なすべてを実装する必要があります。 技術的な要件に加えて、[!DNL Co-op Graph]には他の法的要件や契約上の要件があることに注意してください。
* 現在、1つの[!DNL Private Graph]で2つのIMSタグを使用することはできないので、1つのIMS組織で標準化する必要があります。 複数のIMS組織を持つ顧客がCDAと組み合わせて[!DNL Co-op Graph]を使用できる場合があります。
* [!DNL Co-op graph]と[!DNL Private Graph]、およびCDAの特定のコンポーネントは、[!DNL Microsoft Azure]でホストされます。 つまり、[!DNL Analytics]データは、Adobeのデータ処理センターと[!DNL Microsoft Azure]のAdobeの存在との間で前後にコピーされます。 一部の[!DNL Analytics]データは[!DNL Azure]に保存されます。 あなたの会社はこの取り決めに同意しなければならない。
* CDAには、「クロスデバイス」[!UICONTROL レポートスイート]が必要です。 つまり、CDAに使用する[!UICONTROL レポートスイート]には、デスクトップWeb、モバイルWeb、モバイルアプリなど、複数の異なるデバイスタイプまたは「サーフェス」からのデータを含める必要があります。 2019年9月時点で、この[!UICONTROL レポートスイート]のサーバーコールの量は、100MMサーバーコール/日以下にする必要があります。 （今後数か月間、サーバーコールのボリューム制限が増えます）。
* 2019年9月現在、[!DNL Co-op Graph]と[!DNL Private Graph]は北米でのみご利用いただけます。 EMEAおよびAPACでのグラフプレゼンスのスケジュールは、今後発表される予定です。 これらの地域にいる場合は、グラフが利用可能になった時点で準備が整うよう、開始にこれらの前提条件を確認することをお勧めします。

## デバイス間データの解釈

### 訪問者以外の人

CDA [!UICONTROL 仮想レポートスイート]内で、いくつかの変更点が表示されます。 例えば、[!UICONTROL 実訪問者数]指標は、2つの新しい指標に置き換えられます。[!UICONTROL 人]と[!UICONTROL 個別デバイス]。 これらの新しい指標により、オーディエンスのサイズに関する洞察が大幅に向上します。

*人と個別*
![デバイスCDA [!UICONTROL 人指標]](assets/cda-people-metric.png)

[[!UICONTROL セグメントビルダー]](https://docs.adobe.com/content/help/ja-JP/analytics/components/segmentation/segmentation-workflow/seg-build.html)では、[!UICONTROL 訪問者]セグメントコンテナは、[!UICONTROL 個人]セグメントコンテナに置き換えられました。 CDA VRSを使用して、次のようなデバイス間のセグメントを作成できます。

* 複数のデバイスを使用しているユーザー
* モバイルデバイスでジャーニーを開始し、その後デスクトップデバイスで購入するユーザー
* 複数のデバイスを使用してタスクを達成する訪問

*Personレベルの*
![[!DNL Segment Builder]  segmentsPersonContainer](assets/cda-segment-builder-person-container.png)

### Dimension持続性

CDA VRS内では、[!DNL eVars]などのディメンションが自動的に複数のデバイス間で保持されるようになりました。 例えば、[!DNL eVar]は次のように設定されます。

* 配分：最新（最後）
* 有効期限：購入

は、購入イベントが起動されるまで、デバイス間で自動的に保持されるようになりました。

## Analysis Workspaceでのデバイス間データの分析

### 個人ベースのオーディエンス分析

ブランドと関わり合う人が何人いるのか不思議に思ったことはありますか？ 使用するデバイスの数と種類を理解したいとお考えですか。 使用状況が重複するのはどのようか。 CDA VRSを使用して、クロスデバイス[ベン図](https://docs.adobe.com/content/help/ja-JP/analytics/analyze/analysis-workspace/visualizations/venn.html)とデバイスパーパーパーパーパーソン[ヒストグラム](https://docs.adobe.com/content/help/ja-JP/analytics/analyze/analysis-workspace/visualizations/histogram.html)を作成できます。

*人物ベースのオーディエンス*
![分析ベンとヒストグラム](assets/cda-venn-and-histogram.png)

### クロスデバイス [!DNL Flow]

CDAとAnalysis Workspaceを使用すると、[[!DNL Flow visualization]](https://docs.adobe.com/content/help/ja-JP/analytics/analyze/analysis-workspace/visualizations/flow/flow.html)で、人々がデバイス間を時間の経過と共にどのように移動しているかを視覚化できます。 ジャーニーのどこで落ちて行くかが分かります

*[!DNL Flow](CDA)*
![[!DNL Flow Visualization]](assets/cda-flow-viz.png)

### クロスデバイス [!DNL Fallout]

成功を収める前に、一連の手順を通してユーザーがどの程度上手く行っているかを分析するために、[[!DNL Fallout visualizations]](https://docs.adobe.com/content/help/ja-JP/analytics/analyze/analysis-workspace/visualizations/fallout/fallout-flow.html)をいくつか使うと思います。 従来のデバイスベースの解析を使用する場合、[!DNL Fallout visualizations]の表示が制限されていることをご存じですか。 「フォールスルー」を正常に行うには、次の手順が前の手順と同じブラウザーまたはアプリで行われる必要があります。 デバイスベースの分析では、別のデバイスの次の手順を正常に完了したユーザーは見えなくなります。

心配するな、CDAがお話しした。 CDAは、[!DNL Fallout visualizations]をもっと役に立たせるクロスデバイス表示を作り出します。 結局のところ、人が最終的にどこかでタスクに成功したかどうかが重要なのです。

*[!DNL Fallout](CDA)*
![[!DNL Fallout Visualization]](assets/cda-fallout-viz.png)

### [!DNL Cross-Device Attribution IQ]

CDAはAnalysis Workspaceの下にクロスデバイスデータの層を作成するので、すべての分析にクロスデバイスの観点でフレーバーが付けられます。 強力な例として、[[!DNL Attribution IQ]](https://docs.adobe.com/content/help/ja-JP/analytics/analyze/analysis-workspace/attribution/models.html)を使用します。 [!DNL Attribution IQ] Analysis Workspaceでは、複数のアトリビューションモデルを並べて比較できます。この機能をCDAと組み合わせて使用すると、異なるデバイスがどのように成功に貢献しているかを比較できます。

例えば、インタラクションで最初に使用されるデバイスが携帯電話でどれだけ頻繁に使用され、最終的に成功をもたらすかを把握したい場合、 これは、携帯電話の「獲得率」を表します。 CDA + [!DNL Attribution IQ]では、次の分析が可能です。

*[!DNL Attribution IQ](CDA)*
![[!DNL Attribution IQ]](assets/cda-attribution-iq.png)

詳しくは、[[!DNL Cross-Device Analytics] ヘルプドキュメント](https://docs.adobe.com/content/help/ja-JP/analytics/components/cda/cda-home.html)を参照してください。

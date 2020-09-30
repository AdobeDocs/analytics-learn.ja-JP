---
title: ジャーニーIQの理解と使用 — デバイス間分析
description: ユーザーはブランドとやり取りする際、様々な方法や複数のデバイスでやり取りします。 デバイス間の分析は、Adobe Experience PlatformIDサービスと統合され、デバイスと人との対応付け方法を識別します。 その後、このインテリジェンス機能を活用して、デバイス間でのユーザー行動の表示を作成します。 その結果、デバイスではなく人に対して分析を行うことができます。
feature: cda
topics: null
audience: all
activity: use
doc-type: article
team: Technical Marketing
kt: 4138
translation-type: tm+mt
source-git-commit: 24ad92b0ccdf1112e3ed4a0968cd47db757598c3
workflow-type: tm+mt
source-wordcount: '1681'
ht-degree: 6%

---


# 理解と使用 [!DNL Journey IQ] — デバイス間分析

ユーザーはブランドとやり取りする際、様々な方法や複数のデバイスでやり取りします。 デバイス間の分析は、と統合さ [!DNL Adobe Experience Platform Identity Service] れて、デバイスと人とのマッピング方法を識別します。 その後、このインテリジェンス機能を活用して、デバイス間でのユーザー行動の表示を作成します。 その結果、デバイスではなく人に対して分析を行うことができます。

## デバイス間分析の概要

### 自分は自分の装置ではない

ユーザーがブランドとやり取りする際には、様々な方法で、また複数の「サーフェス」や「デバイス」で行います。 PCやモバイルデバイスでWebブラウザーを使用する場合や、モバイルアプリを使用する場合があります。 cookieに基づくデータ収集で育った従来のデジタル解析では、これらの各サーフェスは一意の「訪問者」として表されます。 つまり、各人間ユーザーは、複数の個別訪問者として表されます。

次に例を示します。 Isabelleが次のようにブランドとやり取りしたとします。

*イザベルは*![従来の解析の遍歴を持つ3つの訪問者です](assets/cda-isabelle-journey-traditional-analytics.png)

従来の解析を使用して、イザベルの遍歴は3つに分割されます。 彼女は3人のユニークな訪問者として表され、それぞれ異なるタスクを使用して隔離されたデバイスを実行しています。 必要なのは、イザベルのやり取りの統合されたデバイス間表示です。 [!DNL Journey IQ: Cross-Device Analytics] にこの表示を示します。

*Isabelleは1人のユーザー*![がデバイス間分析の遍歴](assets/cda-isabelle-journey-cross-device-analytics.png)

### デバイス間の表示による解析の改善

人間中心のクロスデバイス表示のIsabelleの行動は、分析に大きな影響を与えます。 例えば、従来の訪問者ベースのアプローチでは、マーケティングチャネルの効果について完全な実態を示すわけではありません。 イザベルの旅を振り返ってみましょう。チャネルが商品表示と購入のクレジットを受け取ることに焦点を当てています。 簡単にするために [!UICONTROL ラストタッチアトリビューションを使用しますが] 、同じ問題は、イザベルの動作を別々の訪問者に分割する場合に、任意のアトリビューションモデルを使用して発生します。 従来の訪問者ベースの表示を使用した世界は、大きく異なる、誤解を招く結果をもたらします。

*従来のAnalyticsとデバイス間のAnalytics*![チャネルアトリビューションの比較](assets/channel-attribution.png)

デバイス間の表示を使用すると、電子メールチャネルは製品の表示と購入の両方のクレジットを受け取ります。これは、Isabelleの実際の経験をより正確に表します。

読み続けて学習：

* How [!DNL Cross-Device Analytics] Works
* 前提条件 [!DNL Cross-Device Analytics]
* デバイス間データの解釈
* Analysis Workspaceでのデバイス間データの分析

## How [!DNL Cross-Device Analytics] Works

[!DNL Journey IQ: Cross-Device Analytics (CDA)] を統合 [!DNL Adobe Experience Platform Identity Service]し、 [[!DNL Co-op Graph]を使用する](https://docs.adobe.com/content/help/ja-JP/device-co-op/using/home.html) か、デバイスと人との対応付け [!DNL Private Graph] を識別します。 その後、このインテリジェンス機能を活用して、デバイス間でのユーザー行動の表示を作成します。 CDAには、マルチデバイスの使用状況や、ブランドとのインタラクションに関する顧客体験を企業が把握できるように、他に類を見ない機能やツールが含まれています。 これはAnalysis Workspaceの下のレイヤーとして配置され、 [!UICONTROL フォールアウト]、 [!DNL Flow]、 [!DNL Cohort]、などの強力なツールを使用して、個人ベースのオーディエンス分析とデバイス間のアトリビューション、セグメント化、遍歴の分析について深い洞察を提供 [!DNL Segment IQ][!DNL Attribution IQ]します。

###   [!DNL Cross-Device Virtual Report Suite]

CDAは、特別な種類のデバイス間 [[!UICONTROL 仮想レポートスイートを通じて提供されます]](https://docs.adobe.com/content/help/ja-JP/analytics/components/virtual-report-suites/vrs-about.html)。 これにより、デバイス間の分析を導入する際に、元のデバイスベースのレポートスイートを引き続き使用できます。 CDA VRSの設定は簡単です。

VRSビルダーの1つの手順で、AdobeがCDA対応として設定した [!UICONTROL レポートスイート] を選択します。

*CDA対応のベース（ソース）[!UICONTROL レポートスイート]*![[!UICONTROL 仮想レポートスイート] Step Oneを選択します。](assets/cda-vrs-step-one.png)

次に、「 [!UICONTROL レポートの時間処理] 」をオンにして、デバイス [!UICONTROL 間のステッチを有効にします]。

*レ[!UICONTROL ポート時処理]/デバイス[!UICONTROL 間の切り替えを有効にする]*![ 仮想レポートスイートのステップ2](assets/cda-vrs-step-two.png)

VRSの設定を終了し、保存します。 CDA VRSは、次に示すように、Analysis Workspaceに特別なアイコンと共に表示されます。

*Analysis Workspace*![[!UICONTROL 仮想レポートスイートのCDA VRSを選択します] 。手順3](assets/cda-vrs-step-three.png)

>[!TIP]
>
>CDAが有効なベースレポートスイートの上に [!UICONTROL 、CDA] 仮想レポートスイートを必要な数だけ作成でき ます。

### 履歴の再利用

ユーザーがログインし、ログインした後、またはユーザーを識別してデバイスをマッピングするのに時間がかかる場合 [!DNL Co-op Graph] があ [!DNL Private Graph] ります。 CDAは30日間のルックバックウィンドウを利用して、以前は不明だった訪問者を、過去30日間までの人物として再認証できます。

これはどう役に立ちますか？ 上のディスカッションからイザベルのユーザの遍歴を思い出してください。

![[!DNL Cross-Device Analytics] 旅](assets/cda-isabelle-journey-cross-device-analytics.png)

Isabelleは、購入直前までログインせず、購入後しばらくの間、Isabelleのデバイスをマッピングし [!DNL Co-op Graph] なかっ [!DNL Private Graph] た可能性があります。 CDAの30日間の振り返りにより、CDAはイザベルの過去の行動を人間レベルで言い換え、必要なデバイス間の表示を提供します。

>[!NOTE]
>
>履歴は再記述できるので、CDA対応の [!UICONTROL 仮想レポートスイートでは、時間の経過と共にデータが変化する可能性があります]。 CDAベースの分析からインサイトを伝える際は、この点に注意してください。

## デバイス [!UICONTROL 間分析の前提条件]

CDAは、 [[!DNL Analytics Ultimate]に含まれています](https://helpx.adobe.com/legal/product-descriptions/adobe-analytics.html)。 2019年9月以降、以下に示す前提条件を満たす [!DNL Analytics Ultimate] お客様は、CDAを使用する資格があります。 CDAの前提条件は次のとおりです。

* 会社は、 [!DNL Adobe Experience Platform Identity Service] [!DNL Co-op Graph]のメンバである必要があります [。または、](https://docs.adobe.com/content/help/ja-JP/device-co-op/using/home.html)[!DNL Adobe Experience Platform Identity Service Private Graph][!DNL Co-op Graph]を使用してください。
* グラフとの [!DNL Co-op Graph] Experience CloudID(ECID) [!DNL Private Graph] とIDの同期に必要なすべてのものを実装する [](https://docs.adobe.com/content/help/ja-JP/id-service/using/home.html) か、またはグラフとの同期に必要なものすべてを実装する必要があります。 技術的な要件に加えて、には法的要件や契約上の他の要件 [!DNL Co-op Graph] があることに注意してください。
* 現在、1つのIMS組織で2つのIMS組織を使用することはできないので、1つのIMS組織で標準化する必要があり [!DNL Private Graph]ます。 複数のIMS組織を持つ顧客がCDAと組み合わせてIMSを使用できる場合 [!DNL Co-op Graph] があります。
* CDAの [!DNL Co-op graph] および [!DNL Private Graph]特定のコンポーネントは、でホストされ [!DNL Microsoft Azure]ます。 つまり、 [!DNL Analytics] Adobeのデータ処理センターとAdobeの在席との間でデータが前後にコピーされ [!DNL Microsoft Azure]ます。 一部の [!DNL Analytics] データはに保存され [!DNL Azure]ます。 あなたの会社はこの取り決めに同意しなければならない。
* CDAでは、「デバイス間」の [!UICONTROL レポートスイートが必要]です。 つまり、CDAに使用する [!UICONTROL レポートスイート] には、デスクトップWeb、モバイルWeb、モバイルアプリなど、複数の異なるデバイスタイプまたは「サーフェス」からのデータを含める必要があります。 2019年9月時点で、この [!UICONTROL レポートスイートのサーバーコールの量は] 、1日100MMサーバーコール数以下にする必要があります。 （今後数か月間、サーバーコールのボリューム制限が増えます）。
* 2019年9月現在、 [!DNL Co-op Graph] およびは北米でのみ利用 [!DNL Private Graph] 可能です。 EMEAおよびAPACでのグラフプレゼンスのスケジュールは、今後発表される予定です。 これらの地域にいる場合は、グラフが利用可能になった時点で準備が整うよう、開始にこれらの前提条件を確認することをお勧めします。

## デバイス間データの解釈

### 訪問者以外の人

CDA [!UICONTROL Virtual Report Suiteには]、いくつかの変更点があります。 例えば、 [!UICONTROL 実訪問者数指標は2つの新しい指標に置き換えられます] 。 [!UICONTROL ユーザー] と [!UICONTROL 個別デバイス]。 これらの新しい指標により、オーディエンスのサイズに関する洞察が大幅に向上します。

*ユーザーと個別デバイス*![CDA [!UICONTROL 人物指標]](assets/cda-people-metric.png)

セグメ [[!UICONTROL ントビルダー]](https://docs.adobe.com/content/help/ja-JP/analytics/components/segmentation/segmentation-workflow/seg-build.html)では [!UICONTROL 、] 訪問者セグメントコンテナが [!UICONTROL 個人] セグメントコンテナに置き換えられました。 CDA VRSを使用して、次のようなデバイス間のセグメントを作成できます。

* 複数のデバイスを使用しているユーザー
* モバイルデバイスでの旅を開始し、後でデスクトップデバイスで購入する人
* 複数のデバイスを使用してタスクを達成する訪問

*個人レベルのセグメント*![[!DNL Segment Builder] Person  コンテナ](assets/cda-segment-builder-person-container.png)

### Dimension持続性

CDA VRS内で、などのディメンションがデバイス間で自動的に保持さ [!DNL eVars] れるようになりました。 例えば、次のよう [!DNL eVar] に設定された場合、

* 配分：最新（最後）
* 有効期限：購入

は、購入イベントが起動されるまで、デバイス間で自動的に保持されるようになりました。

## Analysis Workspaceでのデバイス間データの分析

### 個人ベースのオーディエンス分析

ブランドと関わり合う人が何人いるのか不思議に思ったことはありますか？ 使用するデバイスの数と種類を理解したいとお考えですか。 使用状況が重複するのはどのようか。 CDA VRSを使用して、デバイス間の [ベン図](https://docs.adobe.com/content/help/ja-JP/analytics/analyze/analysis-workspace/visualizations/venn.html) 、および個人別の [ヒストグラムを作成できます](https://docs.adobe.com/content/help/ja-JP/analytics/analyze/analysis-workspace/visualizations/histogram.html)。

*人ベースのオーディエンス分析*![ベンとヒストグラム](assets/cda-venn-and-histogram.png)

### クロスデバイス [!DNL Flow]

CDAとAnalysis Workspaceを使用すると、 [[!DNL Flow visualization]で、時間の経過とともに人々がデバイス間をどのように移動しているかを視覚化できます](https://docs.adobe.com/content/help/ja-JP/analytics/analyze/analysis-workspace/visualizations/flow/flow.html)。 彼らが旅の途中でどこに落ちて行くかを見ることができます

*[!DNL Flow](CDA)*
![[!DNL Flow Visualization]](assets/cda-flow-viz.png)

### クロスデバイス [!DNL Fallout]

成功を実現する前に、 [[!DNLフォールアウトビジュアライゼーション]](https://docs.adobe.com/content/help/ja-JP/analytics/analyze/analysis-workspace/visualizations/fallout/fallout-flow.html) [#DNLフォールアウトビジュアライゼーション]を使用して、特定の一連の手順を行うユーザーの成果を分析することがよくあります。 従来のデバイスベースの解析を使用する場合、それらの表示 [!DNL Fallout visualizations] が制限されることをご存じでしたか。 「フォールスルー」を正常に行うには、次の手順が前の手順と同じブラウザーまたはアプリで行われる必要があります。 デバイスベースの分析では、別のデバイスの次の手順を正常に完了したユーザーは見えなくなります。

心配するな、CDAがお話しした。 CDAはデバイス間の表示を作成し、 [!DNL Fallout visualizations] 非常に役立ちます。 結局のところ、人が最終的にどこかでタスクに成功したかどうかが重要なのです。

*[!DNL Fallout](CDA)*
![[!DNL Fallout Visualization]](assets/cda-fallout-viz.png)

### [!DNL Cross-Device Attribution IQ]

CDAはAnalysis Workspaceの下にクロスデバイスデータの層を作成するので、すべての分析にクロスデバイスの観点でフレーバーが付けられます。 強力な例として、 [[!DNLAttribution IQ]を使用し](https://docs.adobe.com/content/help/ja-JP/analytics/analyze/analysis-workspace/attribution/models.html)ます。 [!DNL Attribution IQ] analysis workspaceでは、複数のアトリビューションモデルを並べて比較できます。 この機能をCDAと組み合わせて使用すると、異なるデバイスがどのように成功に貢献しているかを比較できます。

例えば、インタラクションで最初に使用されるデバイスが携帯電話でどれだけ頻繁に使用され、最終的に成功をもたらすかを把握したい場合、 これは、携帯電話の「獲得率」を表します。 CDA + [!DNL Attribution IQ] では、次の分析が可能です。

*[!DNL Attribution IQ](CDA)*
![[!DNL Attribution IQ]](assets/cda-attribution-iq.png)

For more information, see the [[!DNL Cross-Device Analytics] help documentation](https://docs.adobe.com/content/help/ja-JP/analytics/components/cda/cda-home.html).

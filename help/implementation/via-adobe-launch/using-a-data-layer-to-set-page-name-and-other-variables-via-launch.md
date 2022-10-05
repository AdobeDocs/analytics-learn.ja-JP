---
title: データレイヤーを使用し、タグを介して Analytics 変数を設定します
description: Analytics データやその他のデータソリューションを調達するためのデータレイヤーのExperience Cloudについて説明します。
feature: Launch Implementation
role: Developer, Data Engineer
level: Beginner
kt: 1852
thumbnail: 25899.jpg
exl-id: 408ceb47-df05-4456-85bb-0ef2798a05a5
source-git-commit: d78c3351d2a98704396ceb8f84d123dd463befe5
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 9%

---

# データレイヤーを使用し、を介して Analytics 変数を設定します。 [!DNL Tags] {#use-a-data-layer-to-set-analytics-variables-in-adobe-analytics-via-tags}

のデータレイヤーの使用 [!DNL Analytics] その他のExperience Cloudソリューションは、ベストプラクティスです。 このビデオでは、データレイヤーから値を取り出し、で使用する方法を説明します。 [!DNL Experience Platform Tags] Adobe Analyticsで変数を設定する

## データレイヤー {#data-layers}

A _データレイヤー_ は、開発者がデジタル Web ページに追加する JavaScript オブジェクトのフレームワークです。 Analytics ソリューションは、最終的にデータレイヤーを使用してレポートに入力します。 タグ管理システム ( [!DNL Experience Platform Tags]) は、データレイヤーを読み取り、値を変数にマッピングし、そのデータをデジタルエクスペリエンスソリューションに送信する仲介者です。

内のデータレイヤーに関する追加情報の確認 [Experience Cloud文書](https://experienceleague.adobe.com/docs/analytics/implementation/prepare/data-layer.html?lang=ja) そしてブログ [データレイヤー：バズワードからベストプラクティスまで](https://blog.adobe.com/en/2014/03/13/data-layers-buzzword-best-practice).

## データレイヤー、 [!DNL Experience Platform Tags]、およびAdobe Analytics{#data-layers-launch-and-adobe-analytics}

1. サイトで使用するデータレイヤー規格を定義または識別します。

   1. データレイヤーを、ページの head セクション内、および [!DNL Experience Platform Tags]. これにより、 [!DNL Tags] Adobe Targetのように、ページ上で高く設定する必要があるAdobeソリューションによって実行されます。

1. データレイヤーにデータを入力します。
1. In [!DNL Experience Platform Tags], create &quot;[!UICONTROL データ要素]」と呼ばれ、データレイヤー内のデータポイントをマッピングします。 これらのデータ要素は、 [!DNL Experience Platform Tags] in [!UICONTROL ルール] および [!UICONTROL 拡張機能].
1. 次の [!DNL Analytics] 拡張機能のグローバル変数セクション、または [!DNL Tags rule]を設定し、 [!UICONTROL データ要素] から [!UICONTROL prop], [!UICONTROL eVar], [!UICONTROL pageName]、その他 [!DNL Analytics] 変数。
1. データを [!DNL Analytics] に送信するビーコンをトリガーします。

次のビデオでは、プロセスを順を追って説明します。

>[!VIDEO](https://video.tv.adobe.com/v/25899/?quality=12)

>[!NOTE]
>
>このビデオで使用される特定のデータレイヤーは、組織にとって「ベストプラクティス」とは見なされない場合があります。 データレイヤーを使用して重要なデータをデジタルマーケティングソリューションに表示する概念は、ベストプラクティスです。
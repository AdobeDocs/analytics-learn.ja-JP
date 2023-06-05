---
title: データレイヤーを使用し、タグを介して Analytics 変数を設定する
description: Analytics データやその他の Experience Cloud ソリューションを調達するためのデータレイヤーの使用について説明します。
feature: Launch Implementation
role: Developer, Data Engineer
level: Beginner
kt: 1852
thumbnail: 25899.jpg
exl-id: 408ceb47-df05-4456-85bb-0ef2798a05a5
source-git-commit: 7224af1bd798d447f1b14c61e836f8e5c8af7ea4
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# データレイヤーを使用し、[!DNL Tags] を介して Analytics 変数を設定する {#use-a-data-layer-to-set-analytics-variables-in-adobe-analytics-via-tags}

[!DNL Analytics] やその他の Experience Cloud ソリューションにデータレイヤーを使用することは、ベストプラクティスです。このビデオでは、データレイヤーから値を取り込み、[!DNL Experience Platform Tags] でその値を使用して Adobe Analytics に変数を設定する方法を説明します。

## データレイヤー {#data-layers}

_データレイヤー_&#x200B;とは、開発者がページに挿入する JavaScript オブジェクトのフレームワークのことを指します。Analytics ソリューションでは最終的に、データレイヤーを使用してレポートに入力します。タグ管理システム（[!DNL Experience Platform Tags]）は、データレイヤーを読み取り、値を変数にマッピングし、そのデータをデジタルエクスペリエンスソリューションに送信する仲介者です。

内のデータレイヤーに関する追加情報の確認 [Experience Cloud文書](https://experienceleague.adobe.com/docs/analytics/implementation/prepare/data-layer.html?lang=ja).

## データレイヤー、[!DNL Experience Platform Tags]、および Adobe Analytics{#data-layers-launch-and-adobe-analytics}

1. サイトで使用するデータレイヤー標準を定義または特定します。

   1. データレイヤーを、できる限り、ページの head セクション内、および [!DNL Experience Platform Tags] への呼び出しの前に配置します。こうすることにより、[!DNL Tags] や Adobe ソリューション（Adobe Target のように、ページ上部に設定する必要があるもの）で、すぐに値にアクセスできるようにします。

1. データレイヤーにデータを入力します。
1. [!DNL Experience Platform Tags] では、データレイヤー内のデータポイントをマッピングする「[!UICONTROL データ要素]」を作成します。これらのデータ要素は、[!DNL Experience Platform Tags] 全体で、[!UICONTROL ルール]や[!UICONTROL 拡張機能]で使用されます。
1. [!DNL Analytics] 拡張機能のグローバル変数セクション、または [!DNL Tags rule] で、[!UICONTROL データ要素]の値を、[!UICONTROL prop]、[!UICONTROL eVar]、[!UICONTROL pageName]、およびその他の [!DNL Analytics] 変数に割り当てます。
1. データを [!DNL Analytics] に送信するビーコンをトリガーします。

次のビデオでは、プロセスを順を追って説明します。

>[!VIDEO](https://video.tv.adobe.com/v/25899/?quality=12&learn=on)

>[!NOTE]
>
>このビデオで使用される特定のデータレイヤーは、組織にとって「ベストプラクティス」とは見なされない場合があります。データレイヤーを使用して重要なデータをデジタルマーケティングソリューションに表示するという概念は、ベストプラクティスです。
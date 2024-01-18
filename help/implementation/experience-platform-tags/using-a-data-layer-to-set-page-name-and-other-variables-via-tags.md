---
title: データレイヤーを使用して Analytics 変数をExperience Platform [!DNL tags]
description: データレイヤーを使用して Analytics データやその他のExperience Cloudソリューションを調達する方法を説明します。
feature: Tags
topics: Development
role: Developer, Data Engineer
level: Beginner
kt: 1852
thumbnail: 25899.jpg
exl-id: 408ceb47-df05-4456-85bb-0ef2798a05a5
source-git-commit: a45667a8d7ccb46b9e33bd11a78fac9714a61df5
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 50%

---

# データレイヤーを使用して Analytics 変数をExperience Platform [!DNL tags]

[!DNL Analytics] やその他の Experience Cloud ソリューションにデータレイヤーを使用することは、ベストプラクティスです。このビデオでは、データレイヤーから値を取り出し、Experience Platformで使用する方法を説明します [!DNL tags] を使用してAdobe Analyticsに変数を設定します。

## データレイヤー

_データレイヤー_&#x200B;とは、開発者がページに挿入する JavaScript オブジェクトのフレームワークのことを指します。Analytics ソリューションでは最終的に、データレイヤーを使用してレポートに入力します。タグ管理システム (Experience Platformを含む ) [!DNL tags]) は、データレイヤーを読み取り、値を変数にマッピングし、そのデータをデジタルエクスペリエンスソリューションに送信する仲介者です。

内のデータレイヤーに関する追加情報の確認 [Experience Cloud文書](https://experienceleague.adobe.com/docs/analytics/implementation/prepare/data-layer.html?lang=ja).

## データレイヤー、Experience Platform [!DNL tags]、およびAdobe Analytics

1. サイトで使用するデータレイヤー標準を定義または特定します。

   1. データレイヤーを、ページの head セクション内で、コールトゥExperience Platformの前にできるだけ高く配置します。 [!DNL tags]. こうすることにより、[!DNL tags] や Adobe ソリューション（Adobe Target のように、ページ上部に設定する必要があるもの）で、すぐに値にアクセスできるようにします。

1. データレイヤーにデータを入力します。
1. Experience Platform [!DNL tags], create &quot;[!UICONTROL データ要素]」と呼ばれ、データレイヤー内のデータポイントをマッピングします。 これらのデータ要素は、Experience Platform全体で使用されます [!DNL tags] in [!UICONTROL ルール] および [!UICONTROL 拡張機能].
1. [!DNL Analytics] 拡張機能のグローバル変数セクション、または [!DNL Tags rule] で、[!UICONTROL データ要素]の値を、[!UICONTROL prop]、[!UICONTROL eVar]、[!UICONTROL pageName]、およびその他の [!DNL Analytics] 変数に割り当てます。
1. データを [!DNL Analytics] に送信するビーコンをトリガーします。

次のビデオでは、プロセスを順を追って説明します。

>[!NOTE]
>
> Launch は現在 **[!DNL tags]**

>[!VIDEO](https://video.tv.adobe.com/v/25899/?quality=12&learn=on)

>[!NOTE]
>
>このビデオで使用される特定のデータレイヤーは、組織にとって「ベストプラクティス」とは見なされない場合があります。データレイヤーを使用して重要なデータをデジタルマーケティングソリューションに表示するという概念は、ベストプラクティスです。

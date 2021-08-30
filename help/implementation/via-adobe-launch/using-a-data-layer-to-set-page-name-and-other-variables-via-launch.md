---
title: Launchを介したAdobe Analyticsでのデータレイヤーの使用によるページ名とその他の変数の設定
description: Analyticsやその他のデータソリューションに対してデータレイヤーを使用するExperience Cloudは、ベストプラクティスと見なされます。 このビデオでは、データレイヤーから値を取り出し、Launchで値を使用してAdobe Analyticsで変数を設定する方法を説明します。
feature: Launch Implementation
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1852
role: Developer, Data Engineer
level: Beginner
exl-id: 408ceb47-df05-4456-85bb-0ef2798a05a5
source-git-commit: fe861dfd541c1b9cb3b233fa3f56d55054305fd9
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 7%

---

# データレイヤーを使用した 経由のページ名およびその他の変数の設定[!DNL Experience Platform Launch] {#using-a-data-layer-to-set-page-name-and-other-variables-in-adobe-analytics-via-launch}

[!DNL Analytics]やその他のExperience Cloudソリューションに対してデータレイヤーを使用することがベストプラクティスと見なされます。 このビデオでは、データレイヤーから値を取り出し、[!DNL Experience Platform Launch]で値を使用してAdobe Analyticsで変数を設定する方法を説明します。

## データレイヤー {#data-layers}

サイトやAdobe Experience Cloudソリューション(特にAdobe Analyticsを使用)でデータを操作する場合は、データレイヤーを使用することをお勧めします。 「_データ層_」とは、開発者がページに挿入する JavaScript オブジェクトのフレームワークのことを指します。データ層は、トラッキングツール（[!DNL Experience Platform Launch]のようなタグ管理システムを含む）でレポートに入力するために使用できます。 [Experience Cloudのドキュメント](https://experienceleague.adobe.com/docs/analytics/implementation/prepare/data-layer.html?lang=en)または[W3Cサイト](https://www.w3.org/)で、データレイヤーに関する追加情報を参照してください。

さらに、ブログ「[データレイヤー：バズワードからベストプラクティスまで、](https://theblog.adobe.com/data-layers-buzzword-best-practice/)は、データ層に関する優れた情報と例を提供します。

## データレイヤー、[!DNL Experience Platform Launch]、Adobe Analytics（おお？）{#data-layers-launch-and-adobe-analytics-oh-my}

1. サイトで使用するデータレイヤー標準を作成します。この標準は[!DNL Experience Platform Launch]によって参照できます。

   1. このデータレイヤーは、ページの先頭の、 [!DNL Experience Platform Launch]への呼び出しの前にできるだけ高くし、 [!DNL Launch]や、Adobe Targetのようにページ上で高くする必要があるAdobeソリューションで値をすぐに使用できるようにします。

1. データレイヤーにデータを入力します。
1. [!DNL Experience Platform Launch]で、データレイヤー内のデータポイントを参照し、[!UICONTROL rules]、[!UICONTROL extensions]などの[!DNL Experience Platform Launch]全体で使用できる「[!UICONTROL データ要素]」を作成します。
1. [!UICONTROL データ要素]を[!DNL Analytics]拡張グローバル変数またはルールで使用し、[!UICONTROL prop]、[!UICONTROL eVars]、[!UICONTROL pageName]または他の[!DNL Analytics]変数に値を割り当てます。
1. トリガー:[!DNL Analytics]にデータを送信するビーコン。

次のビデオでは、このプロセスの手順を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/25899/?quality=12)

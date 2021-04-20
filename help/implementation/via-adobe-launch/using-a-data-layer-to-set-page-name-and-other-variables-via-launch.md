---
title: データレイヤーを使用したページ名と他の変数のAdobe Analyticsでの設定（起動を参照）
description: Analyticsおよび他のExperience Cloudソリューション用のデータレイヤーの使用は、ベストプラクティスと見なされます。 このビデオでは、データレイヤーから値を取り出し、「起動」で値を使用してAdobe Analyticsの変数を設定する方法を説明します。
feature: Launch Implementation
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1852
role: "Developer, Data Engineer"
level: Beginner
translation-type: tm+mt
source-git-commit: f3b3fa7d91b0cb21005b57768ca23ed6700fcc03
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 4%

---


# データレイヤーを使用した[!DNL Experience Platform Launch] {#using-a-data-layer-to-set-page-name-and-other-variables-in-adobe-analytics-via-launch}経由のページ名と他の変数の設定

[!DNL Analytics]や他のExperience Cloudソリューションに対してデータレイヤーを使用することは、ベストプラクティスと見なされます。 このビデオでは、データレイヤーから値を取り出し、[!DNL Experience Platform Launch]で値を使用してAdobe Analyticsの変数を設定する方法を説明します。

## データレイヤー{#data-layers}

サイト上のデータ、特にAdobe AnalyticsでAdobe Experience Cloudのソリューションを扱う場合は、データレイヤーを使用することをお勧めします。 「_データ層_」とは、開発者がページに挿入する JavaScript オブジェクトのフレームワークのことを指します。データレイヤーは、（[!DNL Experience Platform Launch]のようなタグ管理システムを含む）トラッキングツールで使用して、レポートに入力できます。 データレイヤーに関する追加情報については、[Experience Cloudドキュメント](https://marketing.adobe.com/resources/help/en_US/sc/implement/ref-data-layer.html)または[W3Cサイト](https://www.w3.org/)を参照してください。

また、[Data Layers:BuzzwordからBest Practice（ベストプラクティス）](https://theblog.adobe.com/data-layers-buzzword-best-practice/)まで、データ層に関する優れた情報と例をいくつか示しています。

## データレイヤー、[!DNL Experience Platform Launch]、Adobe Analytics（ああ？）{#data-layers-launch-and-adobe-analytics-oh-my}

1. サイトで使用するデータレイヤー標準を作成し、[!DNL Experience Platform Launch]から参照できるようにします。

   1. [!DNL Experience Platform Launch]を呼び出す前に、ページの先頭にこのデータレイヤーをできるだけ高く置いておくと、[!DNL Launch]や、Adobe Targetのようにページ上の値を高くする必要のあるAdobeソリューションで値をすぐに使用できます。

1. データレイヤーにデータを入力します。
1. [!DNL Experience Platform Launch]に、データレイヤー内のデータポイントを参照し、[!UICONTROL ルール]、[!UICONTROL 拡張子]などの[!DNL Experience Platform Launch]全体で使用できる「[!UICONTROL データ要素]」を作成します。
1. [!UICONTROL 拡張グローバル変数[!DNL Analytics]またはルールで、データ要素]を使用して、[!UICONTROL props]、[!UICONTROL eVars]、[!UICONTROL pageName]、その他の[!DNL Analytics]変数に値を割り当てます。
1. データを[!DNL Analytics]に送信するビーコンをトリガーします。

次のビデオでは、このプロセスの概要を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/25899/?quality=12)

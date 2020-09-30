---
title: データレイヤーを使用したページ名と他の変数のAdobe Analyticsでの設定（起動を参照）
description: Analyticsおよび他のExperience Cloudソリューション用のデータレイヤーの使用は、ベストプラクティスと見なされます。 このビデオでは、データレイヤーから値を取り出し、「起動」で値を使用してAdobe Analyticsの変数を設定する方法を説明します。
feature: launch implementation
topics: null
audience: implementer
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1852
translation-type: tm+mt
source-git-commit: ee6c03cff5b051d9293d75965e9fd98f151d7fce
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# データレイヤーを使用したページ名および他の変数の設定( [!DNL Experience Platform Launch] {#using-a-data-layer-to-set-page-name-and-other-variables-in-adobe-analytics-via-launch}

ベストプラクティスとして、他のExperience Cloudソリューション用のデータレイヤー [!DNL Analytics] を使用することをお勧めします。 このビデオでは、データレイヤーから値を取り出し、それらをで使用してAdobe Analyticsの変数を設定する方法 [!DNL Experience Platform Launch] を説明します。

## データレイヤー {#data-layers}

サイト上のデータ、特にAdobe AnalyticsでAdobe Experience Cloudのソリューションを扱う場合は、データレイヤーを使用することをお勧めします。 「_データ層_」とは、開発者がページに挿入する JavaScript オブジェクトのフレームワークのことを指します。The data layers can be used by tracking tools (including tag management systems like [!DNL Experience Platform Launch]) to populate reports. データレイヤーに関する追加情報は、 [Experience Cloudドキュメント](https://marketing.adobe.com/resources/help/en_US/sc/implement/ref-data-layer.html) または [W3Cサイトで確認できます](https://www.w3.org/)。

さらに、ブログの [データレイヤーを参照してください。BuzzwordからBest Practice](https://theblog.adobe.com/data-layers-buzzword-best-practice/)（ベストプラクティス）まで、データ層に関する優れた情報と例をいくつか示しています。

## データレイヤー、 [!DNL Experience Platform Launch]およびAdobe Analytics（ああ？）{#data-layers-launch-and-adobe-analytics-oh-my}

1. サイトで使用するデータレイヤ標準を作成し、を参照できるようにし [!DNL Experience Platform Launch]ます。

   1. このデータレイヤーは、ページの先頭、への呼び出しの前にできる限り高くし、値をすぐに使用できるよう [!DNL Experience Platform Launch][!DNL Launch]にします。そのため、値は、Adobe Targetのようにページ上で高くする必要があるAdobeソリューションで使用できます。

1. データレイヤーにデータを入力します。
1. で [!DNL Experience Platform Launch]は、データレイヤー内のデータポイントを参照し、ルー[!UICONTROL ル、]extensions、 [!DNL Experience Platform Launch] extensions、などですべて使用できる「 [!UICONTROL data elements]」を作成し ます。
1. 拡張グローバル変数またはルールで [!UICONTROL データ要素] を使用し [!DNL Analytics] 、値をprop、 [!UICONTROL eVars]、pageVars [!DNL Analytics] 、otheVarsに割り当てます。
1. データを送信するビーコンをトリガし [!DNL Analytics]ます。

次のビデオでは、このプロセスの概要を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/25899/?quality=12)

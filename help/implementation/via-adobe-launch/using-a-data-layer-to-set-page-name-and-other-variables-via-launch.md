---
title: データレイヤーを使用した Launch 経由の Adobe Analytics でのページ名およびその他の変数の設定
description: Analytics やその他の Experience Cloud ソリューションにデータレイヤーを使用することは、ベストプラクティスと見なされます。このビデオでは、データレイヤーから値を取り込み、Launch でその値を使用して Adobe Analytics に変数を設定する方法を説明します。
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
ht-degree: 100%

---

# データレイヤーを使用した [!DNL Experience Platform Launch] 経由のページ名およびその他の変数の設定 {#using-a-data-layer-to-set-page-name-and-other-variables-in-adobe-analytics-via-launch}

[!DNL Analytics] やその他の Experience Cloud ソリューションにデータレイヤーを使用することは、ベストプラクティスと見なされます。このビデオでは、データレイヤーから値を取り込み、[!DNL Experience Platform Launch] でその値を使用して Adobe Analytics に変数を設定する方法を説明します。

## データレイヤー {#data-layers}

サイトや Adobe Experience Cloud ソリューション、特に Adobe Analytics でデータを操作する際には、データレイヤーを使用することをお勧めします。_データレイヤー_ とは、開発者がページに挿入する JavaScript オブジェクトのフレームワークのことを指します。データレイヤーは、トラッキングツール（[!DNL Experience Platform Launch] のようなタグ管理システムなど）でレポートへの情報入力に使用できます。データレイヤーに関する追加情報は、 [Experience Cloud ドキュメント](https://experienceleague.adobe.com/docs/analytics/implementation/prepare/data-layer.html?lang=ja) または [W3C サイト](https://www.w3.org/) で検索してください。

また、 [データレイヤー：バズワードからベストプラクティスまで](https://theblog.adobe.com/data-layers-buzzword-best-practice/) のブログを参照してください。このブログでは、データレイヤーに関する優れた情報と、いくつかの例を紹介しています。

## データレイヤー、[!DNL Experience Platform Launch]、Adobe Analytics{#data-layers-launch-and-adobe-analytics-oh-my}

1. サイトで使用するデータレイヤー標準を作成します。これは、[!DNL Experience Platform Launch] で参照できます。

   1. [!DNL Experience Platform Launch] への呼び出しの前に、このデータレイヤーをページの先頭のできるだけ上部に配置して、[!DNL Launch] や、Adobe Target のようにページの上部に表示される必要のあるアドビのソリューションで、すぐに値を使用できるようにします。

1. データレイヤーにデータを入力します。
1. [!DNL Experience Platform Launch] で、データレイヤーのデータポイントを参照する「[!UICONTROL データ要素]」を作成します。これは、 [!DNL Experience Platform Launch] 全体で [!UICONTROL ルール] や [!UICONTROL 拡張機能] などで使用できます。
1. [!DNL Analytics] 拡張グローバル変数またはルールのいずれかで [!UICONTROL データ要素] を使用し、値を [!UICONTROL props]、 [!UICONTROL eVars]、 [!UICONTROL pageName]、 またはその他の [!DNL Analytics] 変数に割り当てます。
1. データを [!DNL Analytics] に送信するビーコンをトリガーします。

次のビデオでは、プロセスを順を追って説明します。

>[!VIDEO](https://video.tv.adobe.com/v/25899/?quality=12)

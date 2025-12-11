---
title: Analytics トラッキングサーバーとレポートスイート ID の識別方法
description: Adobe Analytics を設定する際や、他の Experience Cloud ソリューションで参照する際は、多くの場合、使用している Analytics 「トラッキングサーバー」や、データの送信先となる「レポートスイート」を知っておくと便利です。また、それを知っておくことが必要な場合さえあります。このビデオでは、Adobe Analytics が実装済みかどうかに関係なく両方の値を見つける方法を説明します。
feature: Implementation Basics
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 2358
role: Developer
level: Beginner
exl-id: 3925026f-69f1-4425-b3a9-6fef26375fed
source-git-commit: 474e68e2937c82efa459b6ed8048a4abd2753285
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 100%

---

# Analytics [!DNL tracking server] と[!UICONTROL レポートスイート ID] の識別方法 {#how-to-identify-your-analytics-tracking-server-and-report-suites}

Adobe Analytics を設定する際や、他の Experience Cloud ソリューションで参照する際は、多くの場合、使用している Analytics 「トラッキングサーバー」や、データの送信先となる「[!UICONTROL レポートスイート]」を知っておくと便利です。また、知っておくことが必要な場合さえあります。このビデオでは、Adobe Analytics が実装済みかどうかに関係なく両方の値を見つける方法を説明します。

>[!IMPORTANT]
>
>この記事とビデオは、Web SDK を使用した実装ではなく、Adobe Analytics の「AppMeasurement」実装に適用されます。

## 実装後 {#after-implementation}

サイトに Analytics を実装したら、トラッキングビーコンで [!DNL tracking server] と [!DNL report suite ID] を見つけることができます。[!DNL tracking server] はビーコンではホスト名になるので、見つけるのは容易です。[!UICONTROL レポートスイート] IDは、ビーコンのパス名の「/b/ss/」の直後にあるコンマ区切りのリストです。

ビーコンや、Analytics などの Experience Cloud ソリューションに入力されるすべての情報を確認するには、[「Experience Cloud Debugger」Chrome 拡張機能](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj?hl=ja)をインストールします。

## 実装前 {#before-implementation}

**[!DNL Tracking server]** - Adobe Analytics の実装をまだ開始していない場合は、「.sc.omtrdc.net」[!DNL tracking server] のサブドメインを選択します。例えば、「Jim’s Brims」という名前のオンラインの帽子店があるとします。この場合は、[!DNL tracking server] を次のように設定するだけです。

「jimsbrims.sc.omtrdc.net」

**[!UICONTROL レポートスイート]** - 作成した[!UICONTROL レポートスイート]のリストを検索するには、[!DNL Analytics] にログインして、トップメニューの[!UICONTROL 管理者]／[!UICONTROL レポートスイート]に移動して、[!UICONTROL レポートスイート]のリスト（ID およびタイトルを含む）を参照します。

詳しくは、以下のビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/26061/?quality=12&learn=on)

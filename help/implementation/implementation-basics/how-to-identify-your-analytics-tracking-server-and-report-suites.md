---
title: Adobe Analytics のトラッキングサーバーとレポートスイート ID を特定する方法
description: Adobe Analytics を設定する際や、他の Experience Cloud ソリューションで参照する際は、多くの場合、使用している Analytics の「トラッキングサーバー」や、データの送信先となる「レポートスイート」を知っておくと便利です。また、それを知っておくことが必要になる場合もあります。 このビデオでは、Adobe Analytics が実装済みかどうかに関係なく両方の値を見つける方法を説明します。
feature: Implementation Basics
topics:
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 2358
role: Developer
level: Beginner
exl-id: 3925026f-69f1-4425-b3a9-6fef26375fed
TQID: 'https://experienceleague.adobe.com/DRy-lxNuEQR9Tb-nIoev0Mu1OzSiCcLcqve1eDf7p6Q'
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
    internal-label: Reports
  - id: a421fb65-2c82-457a-921c-28c46b697a39
    internal-label: Analytics basics
subfeature_v2:
  - id: c24fe15a-643a-47bd-8278-5e027df49785
    internal-label: Implementation basics
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
    internal-label: Measurement
source-git-commit: 3e00cf9416ba2c6886e5a7efb952cac8ce370930
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 100%
---
# Analytics [!DNL tracking server] と[!UICONTROL レポートスイート ID] の識別方法 {#how-to-identify-your-analytics-tracking-server-and-report-suites}

Adobe Analytics を設定する際や、他の Experience Cloud ソリューションで参照する際は、多くの場合、使用している Analytics 「トラッキングサーバー」や、データの送信先となる「[!UICONTROL レポートスイート]」を知っておくと便利です。また、知っておくことが必要な場合さえあります。 このビデオでは、Adobe Analytics が実装済みかどうかに関係なく両方の値を見つける方法を説明します。

>[!IMPORTANT]
>
>この記事とビデオは、Web SDK を使用した実装ではなく、Adobe Analytics の「AppMeasurement」実装に適用されます。

## 実装後 {#after-implementation}

サイトに Analytics を実装したら、トラッキングビーコンで [!DNL tracking server] と [!DNL report suite ID] を見つけることができます。 [!DNL tracking server] はビーコンではホスト名になるので、見つけるのは容易です。 [!UICONTROL レポートスイート] IDは、ビーコンのパス名の「/b/ss/」の直後にあるコンマ区切りのリストです。

ビーコンや、Analytics などの Experience Cloud ソリューションに入力されるすべての情報を確認するには、[「Experience Cloud Debugger」Chrome 拡張機能](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj?hl=ja)をインストールします。

## 実装前 {#before-implementation}

**[!DNL Tracking server]** - Adobe Analytics の実装をまだ開始していない場合は、「.sc.omtrdc.net」[!DNL tracking server] のサブドメインを選択します。 例えば、「Jim’s Brims」という名前のオンラインの帽子店があるとします。 この場合は、[!DNL tracking server] を次のように設定するだけです。

「jimsbrims.sc.omtrdc.net」

**[!UICONTROL レポートスイート]** - 作成した[!UICONTROL レポートスイート]のリストを検索するには、[!DNL Analytics] にログインして、トップメニューの[!UICONTROL 管理者]／[!UICONTROL レポートスイート]に移動して、[!UICONTROL レポートスイート]のリスト（ID およびタイトルを含む）を参照します。

詳しくは、以下のビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/40896/?captions=jpn&quality=12&learn=on)

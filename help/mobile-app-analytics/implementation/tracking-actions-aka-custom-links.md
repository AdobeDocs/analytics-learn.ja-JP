---
title: Experience Platform SDK を使用したモバイルアプリでのアクション（カスタムリンク名）のトラッキング
description: アクションは、モバイルアプリで発生するイベントです。 このビデオでは、trackAction API を使用してアクションをトラッキングし、測定する方法を紹介します。
feature: Mobile SDK
topics:
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 2563
topic: Mobile
role: Developer
level: Experienced
exl-id: 541c51b8-638e-43b4-90ac-0ce94290a141
TQID: 'https://experienceleague.adobe.com/msvft7mQiNGjLqGEezPIbwruvSbsunPGUIFF1q7vlT0'
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
    internal-label: API
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
    internal-label: Implementations
subfeature_v2:
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
    internal-label: Events
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
    internal-label: Mobile SDK
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
    internal-label: Experienced
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 3e00cf9416ba2c6886e5a7efb952cac8ce370930
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 73%
---
# Experience Platform SDK を使用したモバイルアプリでのアクション（カスタムリンク）のトラッキング {#tracking-actions-aka-custom-links-in-a-mobile-app-with-the-experience-platform-sdk}

アクションは、モバイルアプリで発生するイベントです。 このビデオでは、trackAction API を使用してアクションを追跡し測定する方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/328307/?captions=jpn&quality=12&learn=on)

これは、サイト上の画面読み込み以外のすべてのアクションをトラッキングするために使用することを推奨する API です。 画面が表示される場合は、trackState を使用します。これは、ページビューヒットをトリガーします。 それ以外の場合は、trackAction を使用して、実行中のアクションに関連付けられた変数を送信します。

このデータは`contextData`として取り込まれます。つまり、[!UICONTROL 処理ルール &#x200B;]を使用して、これらの`contextData`変数からモバイルデータを取得し、Adobe Analyticsの[!DNL eVars]、[!DNL Props]、イベントなどにマッピングする必要があります。

trackAction の詳細情報については、 [ドキュメント](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/#track-user-actions-for-adobe-analytics) を参照してください。

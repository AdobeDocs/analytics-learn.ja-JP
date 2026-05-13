---
title: Experience Platform SDK を使用したモバイルアプリでのアクション（カスタムリンク）のトラッキング
description: アクションは、モバイルアプリで発生するイベントです。 このビデオでは、trackAction API を使用してアクションを追跡し測定する方法を説明します。
feature: Mobile SDK
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 2563
topic: Mobile
role: Developer
level: Experienced
exl-id: 541c51b8-638e-43b4-90ac-0ce94290a141
TQID: https://experienceleague.adobe.com/msvft7mQiNGjLqGEezPIbwruvSbsunPGUIFF1q7vlT0
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 677e5a22dab92be7ff021c8410525b9091975aef
workflow-type: tm+mt
source-wordcount: 184
ht-degree: 73%

---

# Experience Platform SDK を使用したモバイルアプリでのアクション（カスタムリンク）のトラッキング {#tracking-actions-aka-custom-links-in-a-mobile-app-with-the-experience-platform-sdk}

アクションは、モバイルアプリで発生するイベントです。 このビデオでは、trackAction API を使用してアクションを追跡し測定する方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/328307/?captions=jpn&quality=12&learn=on)

これは、サイト上の画面読み込み以外のすべてのアクションを追跡するために使用する必要がある APIです。 画面が表示される場合は、trackState を使用します。これは、ページビューヒットをトリガーします。 それ以外の場合は、trackAction を使用して、実行中のアクションに関連付けられた変数を送信します。

このデータは`contextData`として取り込まれます。つまり、[!UICONTROL 処理ルール &#x200B;]を使用して、これらの`contextData`変数からモバイルデータを取得し、Adobe Analyticsの[!DNL eVars]、[!DNL Props]、イベントなどにマッピングする必要があります。

trackAction の詳細情報については、 [ドキュメント](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/#track-user-actions-for-adobe-analytics) を参照してください。

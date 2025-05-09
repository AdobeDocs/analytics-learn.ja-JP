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
role: Developer, Data Engineer
level: Experienced
exl-id: 541c51b8-638e-43b4-90ac-0ce94290a141
source-git-commit: 4d467928756950074620388645523021b21fb0d5
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 99%

---

# Experience Platform SDK を使用したモバイルアプリでのアクション（カスタムリンク）のトラッキング {#tracking-actions-aka-custom-links-in-a-mobile-app-with-the-experience-platform-sdk}

アクションは、モバイルアプリで発生するイベントです。 このビデオでは、trackAction API を使用してアクションを追跡し測定する方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/328307/?quality=12&learn=on&captions=jpn)

これは、サイト上の画面読み込み以外のすべてのアクションを追跡するために使用する必要がある APIです。 画面が表示される場合は、trackState を使用します。これは、ページビューヒットをトリガーします。それ以外の場合は、trackAction を使用して、実行中のアクションに関連付けられた変数を送信します。

このデータは `contextData` として取り込まれます。つまり、[!UICONTROL 処理ルール]を使用して、これらの `contextData` 変数からモバイルデータを取り込み、[!DNL eVars]、[!DNL Props]、イベントなどにマッピングする必要があります。 （Adobe Analytics）

trackAction の詳細情報については、 [ドキュメント](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/#track-user-actions-for-adobe-analytics) を参照してください。

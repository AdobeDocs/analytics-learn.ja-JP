---
title: Experience PlatformSDKを使用したモバイルアプリでのアクションの追跡（カスタムリンク）
description: 'アクションは、モバイルアプリで発生するイベントです。 このビデオでは、trackAction APIを使用してアクションを追跡し測定する方法を説明します。 '
feature: モバイル SDK
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 2563
topic: モバイル
role: 「開発者、データ・エンジニア」
level: 経験豊富な
translation-type: tm+mt
source-git-commit: f3b3fa7d91b0cb21005b57768ca23ed6700fcc03
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 1%

---


# Experience PlatformSDK {#tracking-actions-aka-custom-links-in-a-mobile-app-with-the-experience-platform-sdk}を使用したモバイルアプリでのアクションの追跡（AKAカスタムリンク）

アクションは、モバイルアプリで発生するイベントです。 このビデオでは、trackAction APIを使用してアクションを追跡し測定する方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/26268/?quality=12)

これは、サイト上のすべての画面読み込み以外のアクションを追跡するために使用する必要があるAPIです。 画面が現れる場合は、trackStateを使用します。この状態は、ページ表示がヒットしたトリガーです。 それ以外の場合は、trackActionを使用して、実行中のアクションに関連付けられた変数を送信します。

このデータは`contextData`として取り込まれます。つまり、[!UICONTROL 処理ルール]を使用して、これらの`contextData`変数からモバイルデータを取り込み、[!DNL eVars]、[!DNL Props]、イベントなどにマッピングする必要があります。 Adobe Analyticsで

trackActionの詳細については、[ドキュメント](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/configuration-reference/mobile-core-api-reference)を参照してください。

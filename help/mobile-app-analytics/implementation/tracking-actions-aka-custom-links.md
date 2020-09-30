---
title: Experience PlatformSDKを使用したモバイルアプリでのアクションの追跡（カスタムリンク）
description: 'アクションは、モバイルアプリで発生するイベントです。 このビデオでは、trackAction APIを使用してアクションを追跡し測定する方法を説明します。 '
feature: mobile sdk
topics: null
audience: implementer
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 2563
translation-type: tm+mt
source-git-commit: a42658cfd4bae7b077ddd48b4cf5c7db54e35c98
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---


# Experience PlatformSDKを使用したモバイルアプリでのアクションの追跡（カスタムリンク） {#tracking-actions-aka-custom-links-in-a-mobile-app-with-the-experience-platform-sdk}

アクションは、モバイルアプリで発生するイベントです。 このビデオでは、trackAction APIを使用してアクションを追跡し測定する方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/26268/?quality=12)

これは、サイト上のすべての画面読み込み以外のアクションを追跡するために使用する必要があるAPIです。 画面が現れる場合は、trackStateを使用して、ページ表示のヒットをトリガーします。 それ以外の場合は、trackActionを使用して、実行中のアクションに関連付けられた変数を送信します。

このデータは次のよう `contextData`に取り込まれます。つまり、 [!UICONTROL 処理ルールを使用して、これらの] 変数からモバイルデータを取得し、それを `contextData` 、 [!DNL eVars]、 [!DNL Props]、イベントにマッピングする必要があります。 adobe analyticsで

trackActionの詳細については、ドキュメントを参照してくだ [さい](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/configuration-reference/mobile-core-api-reference)。

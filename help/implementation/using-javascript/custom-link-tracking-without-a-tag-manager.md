---
title: タグマネージャーを使用しないカスタムリンクトラッキング
description: ページ上の多くのアクションでは、追跡をページの表示のように扱わないでください。 このビデオでは、(Experience Platform Launchなどの)タグマネージャーを使用していない場合に、Analyticsにリンクトラッキングビーコンをコーディングする方法を学びます。 コードを参照し、重要なヒントを学びます。
feature: appmeasurement implementation
topics: null
audience: implementer
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1845
translation-type: tm+mt
source-git-commit: 8276828e9e759a1964ca5ea89bb1395e5e78b500
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# タグマネージャーを使用しないカスタムリンクトラッキング {#custom-link-tracking-without-a-tag-manager}

ページ上の多くのアクションでは、追跡をページの表示のように扱わないでください。 このビデオでは、(Adobeなどの)タグマネージャーを使用していない場合に、Analyticsにリンクトラッキングビーコンをコーディングする方法を学びま [!DNL Experience Platform Launch]す。 コードを参照し、重要なヒントを学びます。

## s.tl()ビーコンの送信 {#sending-an-s-tl-beacon}

データをAdobe Analyticsに送信する関数は2つあります。

1. s.t() - 「track」ビーコン。ページ表示のヒットで、特定のページ名のページ表示を増分し、他の変数を設定します
1. s.tl() - 「リンクを追跡」ビーコン。「カスタムリンク」ヒット/ビーコンと呼ばれることが多く、ページ表示を増分せず、pageName変数を無視します。 これは、通常、ページ上で新しいページや画面を読み込まない小さなアクションや、新しいページを読み込まないその他のアクションを追跡するために使用します。

>[!NOTE]
>
>このビデオでは、Adobeのようなタグマネージャーを使用していない場合に、カスタムリンクのヒットをコード化する方法を示 [!DNL Experience Platform Launch]します。 導入には、アドビのベストプラクティス [!DNL Experience Platform Launch]となる推奨事項を使用することをお勧めします。 ただし、内のコードを作成する必要がある場合は、次 `s.tl()`の方法を使用します。

>[!VIDEO](https://video.tv.adobe.com/v/25832/?quality=12)

## サンプルコード {#sample-code}

ビデオ内のカスタムリンクで使用されているサンプルコードを次に示します。

```JavaScript
<a href="#" onclick="
    s.linkTrackVars='events,eVar2,prop2';
    s.linkTrackEvents=s.events='event2';
    s.eVar2='facebook share';
    s.prop2='facebook share';
    s.tl(this,'o','Social Share');
    s.manageVars('clearVars',s.linkTrackVars,1);">
    Click here to share on FaceBook
</a>
```

カスタムリンクについて詳しくは、 [ドキュメントを参照してください](https://marketing.adobe.com/resources/help/ja_JP/sc/implement/function_tl.html)。
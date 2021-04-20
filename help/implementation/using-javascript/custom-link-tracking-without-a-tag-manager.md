---
title: タグマネージャーを使用しないカスタムリンクトラッキング
description: ページ上の多くのアクションでは、追跡をページの表示のように扱わないでください。 このビデオでは、(Experience Platform Launchなどの)タグマネージャーを使用していない場合に、Analyticsにリンクトラッキングビーコンをコーディングする方法を学びます。 コードを参照し、重要なヒントを学びます。
feature: Appmeasurement Implementation
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1845
role: "Developer, Data Engineer"
level: Intermediate
translation-type: tm+mt
source-git-commit: f3b3fa7d91b0cb21005b57768ca23ed6700fcc03
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 4%

---


# タグマネージャーを使用しないカスタムリンクトラッキング{#custom-link-tracking-without-a-tag-manager}

ページ上の多くのアクションでは、追跡をページの表示のように扱わないでください。 このビデオでは、Adobe[!DNL Experience Platform Launch]のようなタグマネージャーを使用していない場合、Analyticsにリンクトラッキングビーコンをコーディングする方法を学びます。 コードを参照し、重要なヒントを学びます。

## s.tl()ビーコンの送信{#sending-an-s-tl-beacon}

データをAdobe Analyticsに送信する関数は2つあります。

1. s.t() - 「track」ビーコン。ページ表示のヒットで、特定のページ名のページ表示を増分し、他の変数を設定します
1. s.tl() - 「リンクを追跡」ビーコン。「カスタムリンク」ヒット/ビーコンと呼ばれることが多く、ページ表示を増分せず、pageName変数を無視します。 これは、通常、ページ上で新しいページや画面を読み込まない小さなアクションや、新しいページを読み込まないその他のアクションを追跡するために使用します。

>[!NOTE]
>
>このビデオでは、Adobe[!DNL Experience Platform Launch]のようなタグマネージャーを使用していない場合に、カスタムリンクヒットをコード化する方法を示します。 導入のベストプラクティスとして、[!DNL Experience Platform Launch]を使用することをお勧めします。 ただし、`s.tl()`内のコードを記述する必要がある場合は、次の方法を使用します。

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

カスタムリンクの詳細については、[ドキュメント](https://marketing.adobe.com/resources/help/ja_JP/sc/implement/function_tl.html)を参照してください。
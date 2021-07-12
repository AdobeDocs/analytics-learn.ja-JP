---
title: タグマネージャーを使用しないカスタムリンクトラッキング
description: ページ上の多くのアクションでは、トラッキングをページビューのように扱わないでください。 このビデオでは、タグマネージャー(Experience Platform Launchなど)を使用していない場合に、Analyticsにリンクトラッキングビーコンをコーディングする方法を学びます。 コードを参照し、重要なヒントを確認してください。
feature: Appmeasurementの実装
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1845
role: Developer, Data Engineer
level: Intermediate
exl-id: e4567b1c-414e-44ad-982f-52b0150e7eda
source-git-commit: 32424f3f2b05952fe4df9ea91dcbe51684cee905
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 8%

---

# タグマネージャーを使用しないカスタムリンクトラッキング {#custom-link-tracking-without-a-tag-manager}

ページ上の多くのアクションでは、トラッキングをページビューのように扱わないでください。 このビデオでは、タグマネージャー(Adobe[!DNL Experience Platform Launch]など)を使用していない場合に、Analyticsにリンクトラッキングビーコンをコーディングする方法を学びます。 コードを参照し、重要なヒントを確認してください。

## s.tl()ビーコンの送信 {#sending-an-s-tl-beacon}

Adobe Analyticsにデータを送信する関数は2つあります。

1. s.t() - 「track」ビーコン。ページビューヒットで、特定のページ名のページビュー数を増分し、他の変数を設定します。
1. s.tl() - 「リンクを追跡」ビーコン。「カスタムリンク」ヒット/ビーコンと呼ばれ、ページビューを増分せず、pageName変数を無視します。 これは、一般に、新しいページや画面を読み込まないページ上の小さなアクションや、新しいページ読み込みにつながらないその他のアクションを追跡するために使用されます。

>[!NOTE]
>
>このビデオでは、Adobe[!DNL Experience Platform Launch]のようなタグマネージャーを使用していない場合に、カスタムリンクヒットをコード化する方法を示します。 実装のベストプラクティスとして、[!DNL Experience Platform Launch]を使用することをお勧めします。 ただし、`s.tl()`にコードを記述する必要がある場合は、次の方法を使用します。

>[!VIDEO](https://video.tv.adobe.com/v/25832/?quality=12)

## サンプルコード {#sample-code}

次に、ビデオのカスタムリンクで使用されるサンプルコードを示します。

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

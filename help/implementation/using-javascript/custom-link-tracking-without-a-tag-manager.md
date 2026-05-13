---
title: タグマネージャーを使用しないカスタムリンクトラッキング
description: ページ上の多くのアクションでは、トラッキングをページビューのように扱わないでください。 このビデオでは、タグマネージャー（Experience Platform Launch など）を使用していない場合に、Analytics へのリンクトラッキングビーコンをコード化する方法を説明します。 コードを参照し、重要なヒントを確認してください。
feature: Appmeasurement Implementation
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1845
role: Developer
level: Intermediate
exl-id: e4567b1c-414e-44ad-982f-52b0150e7eda
TQID: https://experienceleague.adobe.com/BU98KM1JAq3v6Gd7SRU0FNT3qW-4a9UvP0M-ffFqJIA
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 677e5a22dab92be7ff021c8410525b9091975aef
workflow-type: tm+mt
source-wordcount: 272
ht-degree: 100%

---

# タグマネージャーを使用しないカスタムリンクトラッキング {#custom-link-tracking-without-a-tag-manager}

ページ上の多くのアクションでは、トラッキングをページビューのように扱わないでください。 このビデオでは、タグマネージャー（Adobe [!DNL Experience Platform Launch] など）を使用していない場合に、Analytics へのリンクトラッキングビーコンをコード化する方法を説明します。 コードを参照し、重要なヒントを確認してください。

## s.tl() ビーコンの送信 {#sending-an-s-tl-beacon}

Adobe Analytics にデータを送信する関数は 2 つあります。

1. s.t() - 「トラック」ビーコン。特定のページ名のページビューを増分し、その他の変数を設定するページビューヒットです。
1. s.tl() - 「トラックリンク」ビーコン。「カスタムリンク」ヒット／ビーコンとも呼ばれ、ページビューを増分せず、pageName 変数を無視します。 これは、新しいページや画面を読み込まないページ上の小さなアクションや、新しいページ読み込みにつながらない他のアクションをトラッキングするために一般的に使用されます。

>[!NOTE]
>
>このビデオでは、Adobe [!DNL Experience Platform Launch] などのタグマネージャーを使用していない場合に、カスタムリンクヒットをコード化する方法を説明します。 実装に関するベストプラクティスのレコメンデーションである [!DNL Experience Platform Launch] を使用することをお勧めします。 ただし、`s.tl()` でコード化する必要がある場合は、次の方法でコード化できます。

>[!VIDEO](https://video.tv.adobe.com/v/25832/?quality=12&learn=on)

## サンプルコード {#sample-code}

ビデオ内のカスタムリンクで使用されるサンプルコードを次に示します。

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

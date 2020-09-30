---
title: 'Adobe Analyticsでの単一ページアプリ(SPA)の追跡時のベストプラクティスの使用 '
description: このドキュメントでは、単一ページアプリ(SPA)を追跡するためにAdobe Analyticsを使用している場合、従い、注意が必要なベストプラクティスをいくつか説明します。 このドキュメントでは、Experience Platform Launchの使用に重点を置いています。これは、推奨される実装方法です。
feature: implementation basics
topics: spa
audience: implementer
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1389
translation-type: tm+mt
source-git-commit: 548ac75589383dfd4da4ae02412de91a0a3b28d6
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Adobe Analyticsでの単一ページアプリ(SPA)の追跡時のベストプラクティスの使用 {#using-best-practices-when-tracking-spa-in-adobe-analytics}

このドキュメントでは、単一ページアプリ(SPA)を追跡するためにAdobe Analyticsを使用している場合、従い、注意が必要なベストプラクティスをいくつか説明します。 このドキュメントでは、Adobeの使用に重点を置いてい [!DNL Experience Platform Launch]ます。これは、推奨される実装方法です。

初期メモ：

* 以下の項目は、を使用してサイトに実装していることを前提 [!DNL Experience Platform Launch] としています。 を使用しない場合も考慮事項が存在しますが、実装方法に合わせ [!DNL Experience Platform Launch]る必要があります。
* すべてのSPAは異なるので、次の項目を調整してニーズに合わせる必要がある場合がありますが、ベストプラクティスをお客様と共有したいと思います。SPAページにAdobe Analyticsを導入する際に考慮する必要があること。

## でのSPAの操作に関する簡単な図 [!DNL Experience Platform Launch] {#simple-diagram-of-working-with-spas-in-launch}

![起動時のanalyticsのspa](assets/spa_for_analyticsinlaunch.png)

**注意：** これは、を使用したAdobe Analytics導入でのSPAページの処理方法を簡単に示した図 [!DNL Experience Platform Launch]です。 このページの以降のセクションでは、慎重に検討または対処する必要がある手順と問題について説明します。

## データレイヤーの設定 {#setting-the-data-layer}

新しいコンテンツがSPAページに読み込まれる場合、またはSPAページでアクションが発生した場合、最初に行う必要があるのは、データレイヤーを更新することです。 これは、カスタムイベントが実行され、でルールがトリガーされる前に発生する必要があります。これ [!DNL Experience Platform Launch][!DNL Experience Platform Launch] により、データレイヤーから新しい値を取得し、それらの値をAdobe Analyticsにプッシュできるようになります。

以下はサンプルのデータレイヤーです。このレイヤーの要素は、表示の変更時やSPAでの操作時に変更できます。 例えば、全画面または大部分の画面を変更する場合、「[!DNL pageName]」要素を変更して、新しい要素を取り込んでAdobe Analyticsに送信することが一般的で [!DNL Experience Platform Launch] す。

```JavaScript
<script>
    digitalData = {
        pageInstanceID: "Launch Demo Site",
        page:{
            pageInfo:{
                pageID: '2745374',
                pageName: 'acs demo - product listing page'
            },
            attributes:{
                project: "Experience Platform Launch Project"
            }
        },
        user : [ {
          "profile" : [ {
            "attributes" : {
              "gender" : "male",
              "age" : "35"
            }
          } ]
        }],
        libraries : {
          adobe : {
            launch : {
              state : 0, // 0 = not loaded , 1 = loaded
              domain : "assets.adobedtm.com"
            }
          }
        }

     };
    </script>
```

## カスタムイベントとリスニングの設定( [!DNL Experience Platform Launch] {#setting-custom-events-and-listening-in-launch}

新しいコンテンツがページに読み込まれたり、サイトでアクションが発生した場合に、ルールを実行してデータを送信でき [!DNL Experience Platform Launch] るように、通知が必要になり [!DNL Analytics]ます。 これを行う方法はいくつかあります。 [!UICONTROL ダイレクト型ルー] ル  またはカスタムイベント。

* [!UICONTROL ダイレクト型ル] ール :で [!DNL Experience Platform Launch]は、 [!UICONTROL 直接呼び出しをページから直接呼び出すと実行される] ダイレクト型ルー  ルを設定できます。 ページの読み込みやサイトでの操作が非常に簡単な場合、またはそれが一意で、（Xに設定され、毎回トリガーされる）特定の命令セットを毎回実行できる場合は、 [!DNL eVar4] 直接呼び出し [!DNL event2][!UICONTROL ルールを使用できます]。 ダイレク [!DNL Experience Platform Launch] ト型ルールの作成に関する [!UICONTROL ドキュメントを参照してくだ] さい 。
* カスタムイベント:機能を強化したり、異なる値のペイロードを動的に付加する機能のために、でカスタムJavaScriptイベントを設定し、それらをリッスンする必要があります。ペイロードを使用して変数を設定し、データをAdobe Analyticsに送信できます。 [!DNL Experience Platform Launch]この機能が必要になる可能性が高いので、このオプションがベストプラクティスと見なされます。 ただし、サイトの各機能によって、どの方法が最も適切かが判断されます。 このカスタムイベント方式を使用する必要があると仮定して、このドキュメントを進めます。

**例：** この [ヘルプドキュメントには](https://helpx.adobe.com/experience-manager/kt/integration/using/launch-reference-architecture-SPA-tutorial-implement.html) 、実装済みのサンプルSPAサイト [!DNL Analytics] (および他のExperience Cloudソリューション)へのリンク、および実装済みの内容を説明するドキュメントへのリンクがあります。 このSPAの例では、次のカスタムイベントが使用されています。

* [!DNL event-view-start]:このイベントは、読み込み中の表示/状態の表示開始で起動します。
* [!DNL event-view-end]:このイベントは、表示/状態の変更が発生し、ページ上のすべてのSPAコンポーネントの読み込みが完了した場合でも起動する必要があります。 これは、通常、Adobe Analyticsへの呼び出しをトリガーするイベントです。
* [!DNL event-action-trigger]:このイベントは、表示/状態の読み込みを除く、ページでイベントが発生した場合に起動します。 これは、クリックイベントである場合や、表示を変更せずに小さなコンテンツが変更される場合があります。

発行方法と発行日時について詳しくは、上記の参照ページ/ドキュメントを参照してください。 これらの同じイベント名を使用する必要はありませんが、ここに示す機能は推奨されるベストプラクティスです。 次のビデオでは、サンプルサイトと、カスタムイベントをリッスンす [!DNL Experience Platform Launch] る場所を示します。

>[!VIDEO](https://video.tv.adobe.com/v/23024/?quality=12)

## ルー [!DNL Experience Platform Launch][!UICONTROL ルでのs.t()またはs.tl()の実行] {#running-s-t-or-s-tl-in-the-launch-rule}

SPAを使用する際に最も重要な点の1つ [!DNL Analytics] は、との違い `s.t()` で `s.tl()`す。 においてこれらのメソッドの1つをトリガして、にデータを送信 [!DNL Experience Platform Launch] します。ただし、それぞれを送信するタイミングを知る必要があり [!DNL Analytics]ます。

* **s.t()** - 「t」は「track」を表し、通常のページ表示です。 URLが変更されない場合でも、表示は十分に変更されるので、新しい「ページ *」と* 見なすことができますか。 その場合は、s.[!DNL pageName] 変数に値を取り込み、呼び出し `s.t()` を [!DNL Analytics]

* **s.tl()** - 「tl」は「リンクを追跡」を表し、通常はページ上のクリック数や小さなコンテンツの変更を追跡するために使用されます。フルスクリーンの変更とは逆です。 ページの変更が小さく、完全な新しい「ページ」と見なさないようにする場合は、s.pageName変数の設定につ `s.tl()` いてはを使用し、心配する必要はありません。この変数は無視 [!DNL Analytics] されます。

**ヒント：** 一部のユーザーは、画面が50%以上変更された場合はページ表示と見なして使用すべきという一般的なガイドラインを使用し `s.t()`ます。 画面に対する変化が50%未満の場合は、を使用し `s.tl()`ます。 ただし、これは、お客様次第で、新しい「ページ」と見なすものと、Adobe Analyticsでのサイトの追跡方法が決まります。

次のビデオでは、トリガーする場所、方法、 `s.t()` またはLaunch by Adobe `s.tl()` 内を示します。

>[!VIDEO](https://video.tv.adobe.com/v/23048/?quality=12)

## 変数のクリア {#clearing-variables}

Adobe Analyticsでサイトをトラッキングする場合、当然、適切なデータを適切なタイミングでに送信す [!DNL Analytics] る必要があります。 SPA環境では、変数内で追跡される値が保持され、 [!DNL Analytics] 変数に再送信される可能性があります。この値は、必要なくなった場合に [!DNL Analytics]も送信されます。 このため、 [!DNL Analytics] 拡張子に変数をクリアする関数があるので、次のイメージリクエストを実行してにデータを送信する際に新しいスレートが作成され [!DNL Launch][!DNL Analytics]ます。

上の図では、ヒットを送信した *後に変数をクリアし、プロセスの最後にリストしています* 。 実際には、ヒットが送信される前にORした後に実行できますが、ルール内で一貫性を持たせてください。したがって、変数を設定して送信する前と後のどちらかを必ずクリアしてください。 [!DNL Experience Platform Launch] 実行 *前に変数をクリアする場合は* 、まず変数をクリアし、次に新しい変数を設定し、最後に新しいデータをに送信する必要があり `s.t()`[!DNL Analytics]ます。

**注意：** 実行時には必ずしも変数のクリアが必要とは限りません。これは、どの変数が設定される `s.tl()`かを知るために、 `s.tl()` 変数をその変数と共に使用する必要があるからです(内の内部で自動的に追加される [!DNL linkTrackVars][!DNL Analytics][!DNL Experience Platform Launch])。 つまり、を使用する場合、通常はエラーのある変数は入ってきません `s.tl()`が、SPA環境でを使用する場合 `s.t()` は非常にお勧めします。 ただし、品質の高いデータ収集を確実に行うためだけに、Clear Variables関数をSPA環境 `s.t()``s.tl()` とSPAの両方で使用することをベストプラクティスとしてお勧めします。

次のビデオでは、の変数をクリアする場所/方法を示し [!DNL Launch]ます。

>[!VIDEO](https://video.tv.adobe.com/v/23049/?quality=12)

## その他の考慮事項 {#additional-considerations}

### カスタムコードウィンドウ( [!DNL Experience Platform Launch] {#custom-code-windows-in-launch}

この [!DNL Launch][!DNL Analytics] 拡張子には、カスタムコードを挿入できる場所が2つあります。「 [!UICONTROL ライブラリ管理] 」セクションと「カスタムコードを使用してトラッカーを[!UICONTROL 設定]」セクションの追加。

![Analyticsカスタムコードウィンドウの起動](assets/launch_analyticscustomcodewindows.png)

重要なのは、SPAページで最初のページ読み込みが発生した場合に、これらの場所のいずれかが実際にコードを1回だけ実行することです。 表示の変更やサイト上のアクションに対してコードを実行する必要がある場合は、適切な **[!UICONTROL ルール]** (「ページ読み込み：」 [!UICONTROL イベント表示エンドのルール])と同じになり、ルールが [!UICONTROL 実行されるたびにコードが実行されます] 。 ルール内でそのアクションを作成する場合 [!UICONTROL は]、 *拡張子=コア* 、 *アクションタイプ=カスタムコードを設定します*。

### 「ハイブリッド」 SPA/標準サイト {#hybrid-spa-regular-sites}

一部のサイトは、「標準」ページとSPAページを組み合わせたものです。 この場合、両方のページタイプで機能する戦略を使用する必要があります。 サイトでカスタムイベントを設定し、でルールをトリガーする場合 [!DNL Experience Platform Launch]は、ハッシュの変更などに基づいて、ページ [!DNL Analytics] から重複ヒットが発生しないように注意してください。 (これがルールのトリガーを選択した場合の例で [!DNL Experience Platform Launch] す)。 この場合、Adobe Analyticsで誤ったデータが提供されないように、ページ表示の1つを抑制する必要があります。

より詳細な制御が可能なように機能を個別の [!UICONTROL ルールに分割する場合は] 、この操作を覚えておき [!UICONTROL 、] 他のルールに対する変更も可能にし、 [!UICONTROL データの整合性を保護する][!DNL Analytics] ようにします。

### A4T [!DNL Target] を使用した統合 {#integration-with-target-via-a4t}

ちょっとした引き出し線です A4Tの [!DNL Target] 使用と統合する場合は、同じ表示変更に対する [!DNL Target] リクエストとリク [!DNL Analytics] エストが同じSDIDを持っていることを確認してください。 これにより、ソリューションでデータが正しく同期されます。

ヒットを確認するには、デバッガーまたはパケットスニファープログラムを使用します。 また、Experience Cloud Debugger( [ここからダウンロードできるChromeの拡張機能](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj))も使用できます。 [!DNL Target] は、ページで最初に実行される必要があるので、JavaScriptコンソールまたはデバッガーでも確認できます。

## その他のリソース {#additional-resources}

* [AdobeフォーラムでのSPAの議論](https://forums.adobe.com/thread/2451022)
* [Experience Platform LaunchでのSPAの実装方法を示すリファレンス・アーキテクチャ・サイト](https://helpx.adobe.com/experience-manager/kt/integration/using/launch-reference-architecture-SPA-tutorial-implement.html)
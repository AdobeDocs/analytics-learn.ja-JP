---
title: 'Adobe Analyticsでの単一ページアプリ(SPA)の追跡時のベストプラクティスの使用 '
description: このドキュメントでは、シングルページアプリ(SPA)を追跡するためにAdobe Analyticsを使用している場合に、従って注意する必要のあるベストプラクティスをいくつか説明します。 このドキュメントでは、Experience Platform Launchの使用に重点を置いています。これは、推奨される実装方法です。
feature: 導入の基本
topics: spa
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1389
topic: SPA
role: 「開発者、データ・エンジニア」
level: 中間
translation-type: tm+mt
source-git-commit: f3b3fa7d91b0cb21005b57768ca23ed6700fcc03
workflow-type: tm+mt
source-wordcount: '1676'
ht-degree: 0%

---


# Adobe Analytics{#using-best-practices-when-tracking-spa-in-adobe-analytics}での単一ページアプリ(SPA)の追跡時のベストプラクティスの使用

このドキュメントでは、シングルページアプリ(SPA)を追跡するためにAdobe Analyticsを使用している場合に、従って注意する必要のあるベストプラクティスをいくつか説明します。 このドキュメントでは、Adobe[!DNL Experience Platform Launch]の使用に重点を置いています。これは推奨される実装方法です。

初期メモ：

* 以下の項目は、[!DNL Experience Platform Launch]を使用してサイトに実装していることを前提としています。 [!DNL Experience Platform Launch]を使用しない場合も、考慮事項は存在しますが、実装方法に合わせる必要があります。
* すべてのSPAは異なるので、お客様のニーズに最も合うように次の項目を調整する必要がある場合がありますが、ベストプラクティスをお客様と共有したいと思います。SPAページにAdobe Analyticsを導入する際に考える必要のあること。

## [!DNL Experience Platform Launch] {#simple-diagram-of-working-with-spas-in-launch}でSPAを使用した簡単な図

![起動時のanalyticsのspa](assets/spa_for_analyticsinlaunch.png)

**注意：** これは、Adobe Analyticsの導入でのSPAページの処理方法を簡単に示した図で [!DNL Experience Platform Launch]す。このページの以降のセクションでは、慎重に検討または対処する必要がある手順と問題について説明します。

## データレイヤーの設定{#setting-the-data-layer}

SPAページに新しいコンテンツが読み込まれる場合、またはSPAページでアクションが発生した場合、最初に行う必要があるのは、データレイヤーを更新することです。 これは、[!DNL Experience Platform Launch]がデータレイヤーから新しい値を取り出してAdobe Analyticsにプッシュできるように、カスタムイベントが起動し、トリガールールが[!DNL Experience Platform Launch]で発生する前に発生する必要があります。

以下はサンプルのデータレイヤーです。このレイヤーの要素は、SPAでの表示の変更や操作時に変更できます。 例えば、全画面/大部分の画面を変更した場合、[!DNL Experience Platform Launch]で新しい要素を取り込んでAdobe Analyticsに送信できるように、「[!DNL pageName]」要素を変更するのが一般的です。

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

## [!DNL Experience Platform Launch] {#setting-custom-events-and-listening-in-launch}でのカスタムイベントとリスニングの設定

新しいコンテンツがページに読み込まれたり、サイトでアクションが発生した場合に、[!DNL Experience Platform Launch]に通知し、ルールを実行して[!DNL Analytics]にデータを送信できるようにします。 これを行う方法はいくつかあります。[!UICONTROL 直接呼び出し] [!UICONTROL ルール]またはカスタムイベント。

* [!UICONTROL 直接] [!UICONTROL 呼び出しルール]:で [!DNL Experience Platform Launch]は、 [!UICONTROL 直接呼び出しをページから直接呼び出すと実行される]  直接呼び出しルールを設定できます。ページの読み込みやサイトでの操作が非常に簡単な場合、またはそれが一意で、毎回特定の命令セットを実行できる場合([!DNL eVar4]をXに、トリガー[!DNL event2]を毎回実行する)は、[!UICONTROL 直接呼び出し][!UICONTROL ルール]を使用できます。 [!UICONTROL 直接呼び出し] [!UICONTROL ルール]の作成に関する[!DNL Experience Platform Launch]ドキュメントを参照してください。
* カスタムイベント:機能を強化し、異なる値のペイロードを動的に付加する機能を実現するには、カスタムJavaScriptイベントを設定し、[!DNL Experience Platform Launch]でリッスンする必要があります。ペイロードを使用して変数を設定し、データをAdobe Analyticsに送信できます。 この機能が必要になる可能性が高いので、このオプションがベストプラクティスと見なされます。 ただし、サイトの各機能によって、どの方法が最も適切かが判断されます。 このカスタムイベント方式を使用する必要があると仮定して、このドキュメントを進めます。

**例：** この [](https://helpx.adobe.com/experience-manager/kt/integration/using/launch-reference-architecture-SPA-tutorial-implement.html) ヘルプドキュメントには、実装済みのSPAサイトのサンプル [!DNL Analytics] (および他のExperience Cloudソリューション)へのリンク、および実装済みの内容を説明するドキュメントがあります。このSPAの例では、次のカスタムイベントが使用されています。

* [!DNL event-view-start]:このイベントは、読み込み中の表示/状態の表示開始で起動します。
* [!DNL event-view-end]:このイベントは、表示/状態の変更が発生し、ページ上のすべてのSPAコンポーネントの読み込みが完了した場合でも起動する必要があります。これは、Adobe Analyticsへの呼び出しをトリガーするイベントです。
* [!DNL event-action-trigger]:このイベントは、表示/状態の読み込みを除く、ページでイベントが発生した場合に起動します。これは、クリックイベントである場合や、表示を変更せずに小さなコンテンツを変更する場合があります。

発行方法と発行日時について詳しくは、上記の参照ページ/ドキュメントを参照してください。 これらの同じイベント名を使用する必要はありませんが、ここに示す機能は推奨されるベストプラクティスです。 次のビデオでは、サンプルサイトと、[!DNL Experience Platform Launch]のカスタムイベントをリッスンする場所を示します。

>[!VIDEO](https://video.tv.adobe.com/v/23024/?quality=12)

## [!DNL Experience Platform Launch] [!UICONTROL ルール] {#running-s-t-or-s-tl-in-the-launch-rule}でs.t()またはs.tl()を実行

SPAで作業する際に[!DNL Analytics]にとって最も重要なことの1つは、`s.t()`と`s.tl()`の違いです。 [!DNL Experience Platform Launch]でこれらのメソッドの1つをトリガして[!DNL Analytics]にデータを送信しますが、それぞれのメソッドをいつ送信するかを知る必要があります。

* **s.t()** - 「t」は「track」を表し、通常のページ表示です。URLが変更されない場合でも、表示は十分に変更されるので、**&#x200B;新しい「ページ」と見なす必要がありますか。 その場合は、s.[!DNL pageName]変数を設定し、`s.t()`を使用して[!DNL Analytics]に呼び出しを送信します

* **s.tl()** - 「tl」は「リンクを追跡」を表し、通常はページ上のクリック数や小さなコンテンツの変更を追跡するために使用されます。フルスクリーンの変更とは逆です。ページの変更が小さく、完全な新しい「ページ」と見なさない場合は、`s.tl()`を使用し、s.pageName変数の設定は気にしないでください。[!DNL Analytics]では無視されます。

**ヒント：** 一部のユーザーは、画面が50%以上変更された場合はページ表示と見なして使用すべきだという一般的なガイドラインを使用し `s.t()`ます。画面に対する変更が50%未満の場合は、`s.tl()`を使用します。 ただし、これは、お客様次第で、新しい「ページ」と見なすものと、Adobe Analyticsでのサイトの追跡方法が決まります。

次のビデオでは、Launch by Adobe内の`s.t()`または`s.tl()`のトリガーの場所/方法を示します。

>[!VIDEO](https://video.tv.adobe.com/v/23048/?quality=12)

## 変数{#clearing-variables}をクリア中

Adobe Analyticsでサイトを追跡する場合、当然ながら適切なデータを適切なタイミングで[!DNL Analytics]に送信するだけです。 SPA環境では、[!DNL Analytics]変数で追跡される値は永続的に保持され、必要なくなった場合に[!DNL Analytics]に再送信できます。 このため、[!DNL Analytics] [!DNL Launch]拡張子に変数をクリアする関数があるので、次のイメージリクエストを実行して[!DNL Analytics]にデータを送信する際に新しいスレートが必要です。

上の図では、ヒットを送信した&#x200B;*の後で*&#x200B;変数をクリアし、プロセスの最後にリストしています。 実際には、ヒットが送信される前にORした後に実行できますが、[!DNL Experience Platform Launch]ルールでは一貫性を保つ必要があるので、変数を設定して送信する前と後のどちらかを必ずクリアします。 `s.t()`を実行する&#x200B;*前に*&#x200B;変数をクリアする場合は、まず変数をクリアし、次に新しい変数を設定し、最後に新しいデータを[!DNL Analytics]に送ります。

**注意：** 変数のクリアは、実行時に必ずしも必要とは限りま `s.tl()`せん。 `s.tl()` 変数を同時に使用して、どの変数が設定され [!DNL linkTrackVars] るかを知らせる必要があるからです(内の内部で自動的に追加され [!DNL Analytics]  [!DNL Experience Platform Launch]ます)。つまり、`s.tl()`を使用する場合は誤った変数は通常入ってこないのですが、SPA環境で`s.t()`を使用する場合は非常にお勧めします。 上述のとおり、SPA環境の`s.t()`と`s.tl()`の両方でClear Variables関数を使用し、品質の高いデータ収集を確実に行うことをベストプラクティスとしてお勧めします。

次のビデオでは、[!DNL Launch]内の変数をクリアする場所/方法を示します。

>[!VIDEO](https://video.tv.adobe.com/v/23049/?quality=12)

## その他の考慮事項 {#additional-considerations}

### [!DNL Experience Platform Launch] {#custom-code-windows-in-launch}のカスタムコードウィンドウ

[!DNL Launch] [!DNL Analytics]拡張子には、カスタムコードを挿入できる場所が2つあります。[!UICONTROL ライブラリ管理]セクションと追加の「[!UICONTROL カスタムコードを使用してトラッカーを設定]」セクション

![Analyticsカスタムコードウィンドウの起動](assets/launch_analyticscustomcodewindows.png)

SPAページで初回のページ読み込みが発生した場合、これらの場所のいずれかが実際にコードを1回だけ実行することを知っておくことが重要です。 表示の変更やサイト上のアクションに対してコードを実行する必要がある場合は、適切な&#x200B;**[!UICONTROL ルール]**&#x200B;に追加のアクションを追加する必要があります(例： &quot;page load:イベント表示エンド&quot; [!UICONTROL ルール])を設定し、[!UICONTROL ルール]が実行されるたびにコードが実行されるようにします。 [!UICONTROL ルール]でそのアクションを作成する場合、*拡張子=コア*&#x200B;および&#x200B;*アクションタイプ=カスタムコード*&#x200B;を設定します。

### &quot;ハイブリッド&quot; SPA/標準サイト{#hybrid-spa-regular-sites}

「通常の」ページとSPAページを組み合わせたサイトもあります。 この場合、両方のページタイプで機能する戦略を使用する必要があります。 サイトでカスタムイベントを設定し、[!DNL Experience Platform Launch]のルールをトリガーする場合は、ハッシュの変更などに基づいて、ページから[!DNL Analytics]に重複ヒットが送られないように注意してください。 (これが[!DNL Experience Platform Launch]ルールのトリガーを選んだ場合)。 この場合、Adobe Analyticsで誤ったデータが提供されないように、ページ表示の1つを抑制する必要があります。

より詳細な制御を行うために、機能を[!UICONTROL ルール]に分割する場合は、[!UICONTROL ルール]に対する変更を他の[!UICONTROL ルール]に対しても行えるように、ドキュメントを覚えておいてください。[!DNL Analytics]

### A4T {#integration-with-target-via-a4t}を介した[!DNL Target]との統合

ちょっとした引き出し線です A4Tを使用して[!DNL Target]と統合する場合は、同じ表示の変更に対する[!DNL Target]リクエストと[!DNL Analytics]リクエストが同じSDIDを持っていることを確認してください。 これにより、ソリューションでデータが正しく同期されます。

ヒットを確認するには、デバッガーまたはパケットスニファープログラムを使用します。 また、Experience Cloud Debugger（Chromeの拡張機能）を使用することもできます。拡張機能は[HERE](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj)からダウンロードできます。 [!DNL Target] は、ページで最初に実行される必要があるので、JavaScriptコンソールまたはデバッガーでも確認できます。

## その他のリソース {#additional-resources}

* [AdobeフォーラムでのSPAの議論](https://forums.adobe.com/thread/2451022)
* [Experience Platform LaunchでのSPAの実装方法を示すリファレンスアーキテクチャサイト](https://helpx.adobe.com/experience-manager/kt/integration/using/launch-reference-architecture-SPA-tutorial-implement.html)
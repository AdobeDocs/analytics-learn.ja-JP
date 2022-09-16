---
title: Adobe Analytics で単一ページアプリケーション（SPA）をトラッキングする際のベストプラクティスの使用
description: このドキュメントでは、Adobe Analytics を使用して単一ページアプリケーション（SPA）をトラッキングする際に、従う必要があり、注意する必要のあるいくつかのベストプラクティスについて説明します。このドキュメントでは、推奨される実装方法である Experience Platform Launch の使用に焦点を当てます。
feature: Implementation Basics
topics: spa
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1389
topic: SPA
role: Developer, Data Engineer
level: Intermediate
exl-id: 8fe63dd1-9629-437f-ae07-fe1c5a05fa42
source-git-commit: 32424f3f2b05952fe4df9ea91dcbe51684cee905
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 100%

---

# Adobe Analytics で単一ページアプリケーション（SPA）をトラッキングする際のベストプラクティスの使用 {#using-best-practices-when-tracking-spa-in-adobe-analytics}

このドキュメントでは、Adobe Analytics を使用して単一ページアプリケーション（SPA）をトラッキングする際に、従う必要があり、注意する必要のあるいくつかのベストプラクティスについて説明します。このドキュメントでは、推奨される実装方法である Adobe [!DNL Experience Platform Launch] の使用に焦点を当てます。

最初のメモ：

* 以下の項目は、[!DNL Experience Platform Launch] を使用してサイトに実装していることを前提としています。[!DNL Experience Platform Launch] を使用していない場合でも考慮事項は存在しますが、実装方法に合わせて調整する必要があります。
* SPA はそれぞれ異なるため、必要に応じて次の項目を微調整する必要が生じる場合がありますが、SPA ページに Adobe Analytics を実装する際に考える必要がある、いくつかのベストプラクティスを紹介します。

## [!DNL Experience Platform Launch] でのSPAの操作に関する簡単な図 {#simple-diagram-of-working-with-spas-in-launch}

![ローンチでの分析用 SPA](assets/spa_for_analyticsinlaunch.png)

**メモ：** 前述のように、これは [!DNL Experience Platform Launch] を使用した Adobe Analytics 実装において、SPA ページがどのように処理されるかを簡略化した図です。このページの以降の節では、慎重に検討または行動すべき手順と問題について説明します。

## データレイヤーの設定 {#setting-the-data-layer}

新しいコンテンツが SPA ページに読み込まれるとき、またはアクションが SPA ページで実行されるとき、最初におこなうべきことの 1 つは、データレイヤーを更新することです。これは、[!DNL Experience Platform Launch] はデータレイヤーから新しい値を取得して、Adobe Analytics にプッシュできるよう、カスタムイベントが発生して [!DNL Experience Platform Launch] でルールがトリガーされる前に実行する必要があります。

以下はデータレイヤーのサンプルで、ビューの変更または SPA でのアクションによってその要素が変更される可能性があります。例えば、全画面または大画面の変更では、「[!DNL pageName]」要素を変更して、新しい要素を [!DNL Experience Platform Launch] でキャプチャして Adobe Analytics に送信できるようにするのが一般的です。

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

## [!DNL Experience Platform Launch] でのカスタムイベントとリスニングの設定  {#setting-custom-events-and-listening-in-launch}

新しいコンテンツがページに読み込まれたとき、またはサイトでアクションが発生したとき、ルールを実行してデータを [!DNL Analytics] に送信できるように、[!DNL Experience Platform Launch] に通知する必要があります。これを行うには、[!UICONTROL 直接呼出し] [!UICONTROL ルール] とカスタムイベントの 2 つの方法があります。

* [!UICONTROL 直接呼出し] [!UICONTROL ルール]：[!DNL Experience Platform Launch] では、ページから直接呼び出されたときに実行される [!UICONTROL 直接呼出し] [!UICONTROL ルール] を設定できます。ページの読み込みやサイトでのアクションが非常に単純な場合、またはそれが一意であり、毎回特定の命令セットを実行できる場合（[!DNL eVar4] を X に設定し、毎回 [!DNL event2] をトリガーする）、[!UICONTROL 直接呼び出し] [!UICONTROL ルール] を使用できます。[!UICONTROL 直接呼出し] [!UICONTROL ルール] の作成については、[!DNL Experience Platform Launch] ドキュメントを参照してください。
* カスタムイベント：より多くの機能および異なる値でペイロードを動的に添付する機能のために、カスタム JavaScript イベントを設定し、[!DNL Experience Platform Launch] でリッスンする必要があります。そこでは、ペイロードを使用して変数を設定し、データを Adobe Analytics に送信できます。 この機能が必要になる可能性が高いので、このオプションはベストプラクティスと見なされます。 ただし、サイトの各機能によって、どの方法が最も適切かを判断できます。このカスタムイベントメソッドを使用する必要があると仮定して、このドキュメントを進めます。

**例：** [この](https://helpx.adobe.com/experience-manager/kt/integration/using/launch-reference-architecture-SPA-tutorial-implement.html?lang=ja)ヘルプ ドキュメントには、[!DNL Analytics]（およびその他の Experience Cloud ソリューション）を実装した SPA サイトのサンプルへのリンクと、実装内容を説明するドキュメントがあります。これらの SPA の例では、次のカスタムイベントが使用されています。

* [!DNL event-view-start]：このイベントは、読み込み中のビュー／状態のビュー開始時に発生します。
* [!DNL event-view-end]：このイベントは、ビュー／状態の変更が発生し、ページ上のすべての SPA コンポーネントの読み込みが完了した場合でも実行する必要があります。これは、通常、Adobe Analytics への呼び出しをトリガーにするイベントです。
* [!DNL event-action-trigger]：このイベントは、ビュー／状態の読み込みを除く、ページでイベントが発生したときに発生します。これは、クリックイベントか、ビューの変更を伴わない小さなコンテンツの変更である可能性があります。

実行方法とタイミングについて詳しくは、上記の参照ページ／ドキュメントを参照してください。 これらの同じイベント名を使用する必要はありませんが、ここに記載されている機能は推奨されるベストプラクティスです。次のビデオでは、サンプルサイトと、[!DNL Experience Platform Launch] でカスタムイベントをリッスンするための場所を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/23024/?quality=12)

## [!DNL Experience Platform Launch] [!UICONTROL ルール] の s.t() または s.tl() を実行 {#running-s-t-or-s-tl-in-the-launch-rule}

SPA で作業する際に [!DNL Analytics] について理解しておくべき最も重要なことの 1 つは、`s.t()` と `s.tl()` の違いです。[!DNL Experience Platform Launch] でこれらのメソッドのいずれかをトリガーして [!DNL Analytics] にデータを送ることになりますが、それぞれのメソッドをいつ送信するかを知っておく必要があります。

* **s.t()** - 「t」は「track」を表します。通常のページビューです。URL が変更されない場合でも、ビューは新しい「ページ」と *見なされる* ほどに変更されますか？その場合は、s.[!DNL pageName] 変数を設定し、`s.t()` を使用して呼び出しを [!DNL Analytics] に送信します。

* **s.tl()** - 「tl」は「リンクをトラック」を表し、通常は全画面の変更とは異なり、ページ上のクリックまたは小さなコンテンツ変更のトラッキングに使用されます。ページ上の変更が小さく、完全に新しい「ページ」と見なされない場合は、`s.tl()` を使用します。[!DNL Analytics] は無視されるので、s.pageName 変数の設定について心配する必要はありません。

**ヒント：** 画面が 50% 以上変化する場合は、これをページビューと見なして `s.t()` を使用するという一般的なガイドラインを使用するユーザーもいます。画面の変化が 50% 未満の場合は、`s.tl()` を使用します。ただし、これは、完全にユーザー次第であり、新しい「ページ」と見なす内容と、Adobe Analytics でのサイトの追跡方法によって異なります。

次のビデオでは、Experience Platform Launch で `s.t()` または `s.tl()` をトリガーする場所／方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/23048/?quality=12)

## 変数のクリア {#clearing-variables}

当然、Adobe Analytics を使用してサイトを追跡する場合は、適切なデータを適切なタイミングで [!DNL Analytics] に送信するだけです。SPA 環境では、[!DNL Analytics] 変数で追跡された値が保持され、不要になった場合には [!DNL Analytics] に再送信される可能性があります。このため、[!DNL Analytics] [!DNL Launch] 拡張機能には変数をクリアする機能があり、次のイメージリクエストを実行してデータを [!DNL Analytics] に送信すると、新しい状態になります。 

上の図では、プロセスの最後にリストされており、ヒットを送信した *後* に変数をクリアしています。実際には、ヒットが送信される前または後に実行できますが、[!DNL Experience Platform Launch] ルールで一貫性を維持する必要があるため、変数を設定して送信する前または後に常にクリアする必要があります。`s.t()` を実行する *前* に変数をクリアする場合は、必ず最初に変数をクリアし、次に新しい変数を設定して、最後に新しいデータを [!DNL Analytics] に送信してください。 

**メモ：** `s.tl()` では、どの変数が設定されるか（[!DNL Experience Platform Launch] のバックグラウンドで自動的に追加される）を [!DNL Analytics] に通知するために、毎回 [!DNL linkTrackVars] 変数を一緒に使用する必要があるため、`s.tl()` を実行するときに変数をクリアする必要はありません。つまり、`s.tl()` を使用する場合、通常は誤った変数は含まれませんが、SPA 環境で `s.t()` を使用する場合は非常に推奨されます。そうは言っても、質の高いデータ収集を確実に行うために、SPA 環境で `s.t()` と `s.tl()` の両方に変数のクリア関数を使用することをベストプラクティスとしてお勧めします。

次のビデオでは、[!DNL Launch] で変数をクリアする場所／方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/23049/?quality=12)

## その他の考慮事項 {#additional-considerations}

### [!DNL Experience Platform Launch] のカスタムコードウィンドウ {#custom-code-windows-in-launch}

[!DNL Launch] [!DNL Analytics] 拡張機能では、カスタムコードを挿入できる場所が 2 つあります。[!UICONTROL ライブラリ管理] セクションと追加の「[!UICONTROL カスタムコードを使用したトラッカーの設定]」セクションです。

![Analytics カスタムコードウィンドウの起動](assets/launch_analyticscustomcodewindows.png)

SPA ページで最初のページの読み込みが行われる際に、これらの場所のいずれかが実際にコードを実行するのは 1 回だけであることを知っておくことが重要です。ビューの変更またはサイトのアクションでコードを実行する必要がある場合は、適切な **[!UICONTROL ルール]** にアクションを（例：「ページの読み込み：イベント／表示／終了」 [!UICONTROL ルール]）を追加し、その [!UICONTROL ルール] が実行されるたびにコードが実行されるようにする必要があります。[!UICONTROL ルール] でそのアクションを作成するときは、 *拡張機能 = Core* および *アクションタイプ = カスタムコード* を設定します。

### 「ハイブリッド」SPA／通常のサイト {#hybrid-spa-regular-sites}

一部のサイトは、「通常の」ページと SPA ページを組み合わせています。この場合、両方のページタイプで機能する方法を使用する必要があります。サイトでカスタムイベントを設定し、[!DNL Experience Platform Launch] でルールをトリガーするときは、ハッシュの変更などに基づいて、ページから [!DNL Analytics] に重複ヒットが発生しないように注意してください（それが [!DNL Experience Platform Launch] ルールのトリガーを選択した方法である場合）。この場合、Adobe Analytics で誤ったデータが返されないように、ページビューの 1 つを抑制する必要があります。

機能を個別の [!UICONTROL ルール] に分割して、より詳細に制御できるようにする場合は、これを行ったことを忘れずに文書化してください。これにより、一方の [!UICONTROL ルール] に変更を加えて、もう一方の [!UICONTROL ルール] にも変更を加えると、 [!DNL Analytics] データの整合性を保護できます。

### A4T 経由での [!DNL Target] との統合 {#integration-with-target-via-a4t}

ここでは、簡単に説明します。A4T を使用して [!DNL Target] と統合する場合は、同じ表示変更での [!DNL Target] リクエストと [!DNL Analytics] リクエストの SDID が同じであることを確認してください。これにより、データがソリューション上で適切に同期されるようになります。

ヒットを確認するには、デバッガーまたはパケットスニファープログラムを使用します。[こちら](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) からダウンロード可能な Chrome 拡張機能である Experience Cloud Debugger を使用することもできます。[!DNL Target] はページの最初に起動する必要があるため、JavaScript コンソールまたはデバッガーでも確認できます。

## その他のリソース {#additional-resources}

* [アドビフォーラムでの SPA ディスカッション](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/best-practices-for-single-page-apps/m-p/267940?profile.language=ja)
* [Experience Platform Launch での SPA の実装方法を示すリファレンスアーキテクチャのサイト](https://helpx.adobe.com/experience-manager/kt/integration/using/launch-reference-architecture-SPA-tutorial-implement.html)

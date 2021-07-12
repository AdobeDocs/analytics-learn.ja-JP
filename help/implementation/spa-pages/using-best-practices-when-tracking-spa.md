---
title: 'Adobe Analyticsでシングルページアプリケーション(SPA)を追跡する際のベストプラクティスの使用 '
description: このドキュメントでは、Adobe Analyticsを使用してシングルページアプリケーション(SPA)を追跡する際に従って注意する必要がある、いくつかのベストプラクティスについて説明します。 このドキュメントでは、推奨される実装方法であるExperience Platform Launchの使用に焦点を当てます。
feature: 実装の基本
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
source-wordcount: '1672'
ht-degree: 0%

---

# Adobe Analyticsでシングルページアプリケーション(SPA)を追跡する際のベストプラクティスの使用 {#using-best-practices-when-tracking-spa-in-adobe-analytics}

このドキュメントでは、Adobe Analyticsを使用してシングルページアプリケーション(SPA)を追跡する際に従って注意する必要がある、いくつかのベストプラクティスについて説明します。 このドキュメントでは、推奨される実装方法であるAdobe[!DNL Experience Platform Launch]の使用に焦点を当てます。

初期メモ：

* 以下の項目は、サイトに[!DNL Experience Platform Launch]を実装することを前提としています。 [!DNL Experience Platform Launch]を使用しない場合でも、考慮事項は存在しますが、実装方法に合わせて調整する必要があります。
* すべてのSPAは異なるので、ニーズに合わせて以下の項目を調整する必要が生じる場合がありますが、ベストプラクティスをいくつかお客様と共有したいと考えています。SPAページにAdobe Analyticsを実装する際に考慮する必要がある事項について説明します。

## [!DNL Experience Platform Launch]でのSPAの操作の簡単な図 {#simple-diagram-of-working-with-spas-in-launch}

![launchでのanalytics用spa](assets/spa_for_analyticsinlaunch.png)

**注意：** この図は、Adobe Analytics実装でのSPAページの使用方法を簡略化したもので [!DNL Experience Platform Launch]す。このページの以降の節では、慎重に検討または対処する必要がある手順と問題について説明します。

## データレイヤーの設定 {#setting-the-data-layer}

新しいコンテンツがSPAページに読み込まれる場合、またはSPAページでアクションが実行される場合、最初におこなうべきことの1つは、データレイヤーを更新することです。 これは、 [!DNL Experience Platform Launch]でカスタムイベントが発生し、トリガールールが発生する前に発生する必要があります。そのため、 [!DNL Experience Platform Launch]がデータレイヤーから新しい値を取得し、Adobe Analyticsにプッシュできます。

以下に、データレイヤーの例を示します。このレイヤーの要素は、SPAでの表示の変更や操作時に変更できます。 例えば、全画面/大部分の画面を変更する場合、[!DNL Experience Platform Launch]で新しい要素を取り込んでAdobe Analyticsに送信できるように、「[!DNL pageName]」要素を変更するのが一般的です。

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

## [!DNL Experience Platform Launch]でのカスタムイベントとリスンの設定 {#setting-custom-events-and-listening-in-launch}

ページに新しいコンテンツが読み込まれる場合や、サイトでアクションが発生した場合は、ルールを実行して[!DNL Analytics]にデータを送信できるように、[!DNL Experience Platform Launch]に通知する必要があります。 これをおこなう方法はいくつかあります。[!UICONTROL 直接呼び出し] [!UICONTROL ルール]またはカスタムイベント。

* [!UICONTROL 直接呼] [!UICONTROL び出しルール]:では、ペ [!DNL Experience Platform Launch]ージから直接呼び出さ [!UICONTROL れ]  たときに実行する直接呼び出しルールを設定できます。ページの読み込みやサイトでの操作が非常に簡単な場合、または一意で、毎回特定の命令セットを実行できる場合([!DNL eVar4]をXに設定し、トリガー[!DNL event2]を毎回)、[!UICONTROL 直接呼び出し] [!UICONTROL ルール]を使用できます。 [!UICONTROL 直接呼び出し] [!UICONTROL ルール]の作成に関する[!DNL Experience Platform Launch]ドキュメントを参照してください。
* カスタムイベント：機能の強化と、異なる値を持つペイロードを動的にアタッチする機能のために、[!DNL Experience Platform Launch]でカスタムJavaScriptイベントを設定し、それらをリッスンする必要があります。ここでは、ペイロードを使用して変数を設定し、データをAdobe Analyticsに送信します。 この機能が必要になる可能性が高いので、このオプションがベストプラクティスと見なされます。 ただし、サイトの各機能によって、どの方法が最適かが判断されます。 このカスタムイベントメソッドを使用する必要があると仮定して、このドキュメントを進めます。

**例：** THIShelpドキュメ [](https://helpx.adobe.com/experience-manager/kt/integration/using/launch-reference-architecture-SPA-tutorial-implement.html) ントには、(およびその他のExperience Cloudソリューション)を実装したSPAサイトのサンプルへのリンク、および実装内容を説明するドキュメントが含まれていま [!DNL Analytics] す。これらのSPAの例では、次のカスタムイベントが使用されています。

* [!DNL event-view-start]:このイベントは、読み込み中のビュー/状態のビュー開始時に発生します。
* [!DNL event-view-end]:このイベントは、ビュー/状態の変更が発生し、ページ上のすべてのSPAコンポーネントの読み込みが終了した場合でも実行する必要があります。これは、通常、Adobe Analyticsへの呼び出しをトリガーするイベントです。
* [!DNL event-action-trigger]:このイベントは、表示/状態の読み込みを除く、ページ上でイベントが発生した場合に発生します。これは、クリックイベントや、ビューの変更なしでの小さなコンテンツの変更である可能性があります。

呼び出し方法とタイミングについて詳しくは、上記の参照ページ/ドキュメントを参照してください。 同じイベント名を使用する必要はありませんが、ここに示す機能は推奨ベストプラクティスです。 次のビデオでは、サンプルサイトと、 [!DNL Experience Platform Launch]内でカスタムイベントをリッスンする場所を示します。

>[!VIDEO](https://video.tv.adobe.com/v/23024/?quality=12)

## [!DNL Experience Platform Launch] [!UICONTROL ルール]でs.t()またはs.tl()を実行する {#running-s-t-or-s-tl-in-the-launch-rule}

SPAを使用する際に[!DNL Analytics]にとって最も重要な点の1つは、`s.t()`と`s.tl()`の違いです。 [!DNL Experience Platform Launch]でこれらのメソッドの1つを呼び出して[!DNL Analytics]にデータを送信しますが、それぞれを送信するタイミングを知る必要があります。

* **s.t()**  - 「t」は「track」を表し、通常のページビューです。URLが変更されない場合でも、**&#x200B;を新しい「ページ」と見なすほど、ビューが十分に変更されますか。 その場合は、 s.[!DNL pageName]変数を設定し、 `s.t()`を使用して呼び出しを[!DNL Analytics]に送信します。

* **s.tl()**  - 「tl」は「リンクを追跡」を表し、通常は、全画面表示の変更とは対照的に、ページ上のクリック数や小さなコンテンツの変更を追跡するために使用されます。ページ上の変更が小さく、完全な新しい「ページ」と見なさないようにする場合は、`s.tl()`を使用し、s.pageName変数の設定について心配しないでください。[!DNL Analytics]では無視されます。

**ヒント：** 一部のユーザーは、画面が50%を超える場合、ページビューと見なしてを使用する必要があるという一般的なガイドラインを使用し `s.t()`ます。画面への変更が50%未満の場合は、`s.tl()`を使用します。 ただし、これは完全にユーザー次第で、新しい「ページ」と見なすものと、Adobe Analyticsでのサイトの追跡方法が決まります。

次のビデオでは、Launch by Adobe内の`s.t()`または`s.tl()`のトリガーの場所と方法を示します。

>[!VIDEO](https://video.tv.adobe.com/v/23048/?quality=12)

## 変数のクリア {#clearing-variables}

Adobe Analyticsでサイトを追跡する場合、当然ながら適切なタイミングで[!DNL Analytics]に適切なデータを送信するだけで済みます。 SPA環境では、 [!DNL Analytics]変数で追跡された値が保持され、 [!DNL Analytics]に再送される可能性があります（これが不要になった場合もあります）。 このため、[!DNL Analytics] [!DNL Launch]拡張機能に変数をクリアする関数があるので、次のイメージリクエストを実行して[!DNL Analytics]にデータを送信する際に新しいスレートが生成されます。

上の図では、ヒットを送信した&#x200B;*後ろの変数*&#x200B;をクリアし、プロセスの最後にリストされています。 実際には、ヒットが送信される前または後におこなうことができますが、[!DNL Experience Platform Launch]ルールでは一貫性があるので、常に変数を設定して送信する前または後にクリアします。 `s.t()`を実行する前に&#x200B;*変数をクリアする場合は、まず変数をクリアし、次に新しい変数を設定してから、最後に[!DNL Analytics]に新しいデータを送信します。*

**注意：** 実行時には必ずしも変数のクリアが必要とは限りませ `s.tl()`ん。これは、 `s.tl()` 設定される変数を指定するた [!DNL linkTrackVars] め、毎回変数を使用する必要があるからです(のバックグラウンドで自動的に追加されま [!DNL Analytics]  [!DNL Experience Platform Launch]す)。つまり、`s.tl()`を使用する際には必要な変数が入ってこないのが普通ですが、SPA環境で`s.t()`を使用する場合は非常にお勧めします。 ただし、SPA環境では、品質の高いデータ収集を確実におこなうために、`s.t()`と`s.tl()`の両方でClear Variables関数を使用することをお勧めします。

次のビデオでは、[!DNL Launch]内の変数をクリアする場所と方法を示します。

>[!VIDEO](https://video.tv.adobe.com/v/23049/?quality=12)

## その他の考慮事項 {#additional-considerations}

### [!DNL Experience Platform Launch]のカスタムコードウィンドウ {#custom-code-windows-in-launch}

[!DNL Launch] [!DNL Analytics]拡張機能には、カスタムコードを挿入できる場所が2つあります。[!UICONTROL ライブラリ管理]セクションと、追加の「[!UICONTROL カスタムコードを使用したトラッカーの設定]」セクション。

![Analyticsカスタムコードウィンドウの起動](assets/launch_analyticscustomcodewindows.png)

SPAページで最初のページ読み込みが発生した場合、これらの場所のいずれかが実際には1回だけコードを実行することを把握しておくことが重要です。 ビューの変更時またはサイト上のアクションでコードを実行する必要がある場合、適切な&#x200B;**[!UICONTROL ルール]**&#x200B;に追加のアクションを追加する必要があります(例：「ページ読み込み：event-view-end&quot; [!UICONTROL rule])と呼ばれ、[!UICONTROL rule]が実行されるたびにコードが実行されます。 [!UICONTROL ルール]でそのアクションを作成する場合、*拡張機能=コア*&#x200B;および&#x200B;*アクションタイプ=カスタムコード*&#x200B;を設定します。

### 「ハイブリッド」SPA/通常のサイト {#hybrid-spa-regular-sites}

一部のサイトは、「通常」のページとSPAのページを組み合わせたものです。 この場合、両方のページタイプで機能する方法を使用する必要があります。 サイトでカスタムイベントを設定し、[!DNL Experience Platform Launch]でルールをトリガーする場合は、ハッシュの変更などに基づいて、ページから[!DNL Analytics]に二重のヒットが入らないように注意してください。 (その場合、[!DNL Experience Platform Launch]ルールのトリガーを選択します)。 この場合、Adobe Analyticsで誤ったデータが返されないように、ページビューの1つを抑制する必要があります。

より詳細な制御が可能なように、機能を個別の[!UICONTROL ルール]に分割する場合は、[!UICONTROL ルール]を他の[!UICONTROL ルール]に変更し、[!DNL Analytics]データの整合性を保護できるように、記憶と文書を作成します。

### A4Tによる[!DNL Target]との統合 {#integration-with-target-via-a4t}

ちょっとした引き出し線です A4Tを使用して[!DNL Target]と統合する場合は、同じビュー上の[!DNL Target]リクエストと[!DNL Analytics]リクエストのSDIDが同じに変更されていることを確認してください。 これにより、データがソリューション上で正しく同期されます。

ヒットを確認するには、デバッガーまたはパケットスニファープログラムを使用します。 また、[HERE](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj)をダウンロードできるChrome拡張機能であるExperience Cloud Debuggerを使用することもできます。 [!DNL Target] は最初にページで実行される必要があるので、JavaScriptコンソールまたはデバッガーでもを確認できます。

## その他のリソース {#additional-resources}

* [SPAフォーラムでのAdobe](https://forums.adobe.com/thread/2451022)
* [Experience Platform LaunchでのSPAの実装方法を示すリファレンスアーキテクチャのサイト](https://helpx.adobe.com/experience-manager/kt/integration/using/launch-reference-architecture-SPA-tutorial-implement.html)

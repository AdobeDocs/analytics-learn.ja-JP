---
title: シングルページアプリケーション (SPA) の実装のベストプラクティス
description: シングルページアプリケーション (SPA) にAdobe Analyticsを実装するためのベストプラクティスをいくつか説明します。 これには、Experience Platformタグの使用が含まれます。この方法は、推奨される実装方法です。
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
source-git-commit: d78c3351d2a98704396ceb8f84d123dd463befe5
workflow-type: tm+mt
source-wordcount: '1313'
ht-degree: 3%

---

# シングルページアプリケーション (SPA) の実装のベストプラクティス {#implementation-best-practices-for-single-page-appliations}

実装のベストプラクティスをいくつか学ぶ [!DNL Adobe Analytics] ( シングルページアプリケーション (SPA) 上 ) これには、 [!DNL Experience Platform Tags]：推奨される実装方法。

最初のメモ：

* 以下のコンテンツは、 [!DNL Experience Platform Tags] を使用してAdobe Analyticsを実装します。 次の点を考慮する必要があります。 [!DNL Experience Platform Tags] を使用しないので、実装方法に適応させる必要があります。
* SPAには違いがあるので、ニーズに最も合うようにアプローチを調整する必要があります。

## [!DNL Experience Platform Tags] でのSPAの操作に関する簡単な図 {#simple-diagram-of-working-with-spas-in-tags}

![タグでの analytics 用SPA](assets/spa_for_analyticsinlaunch.png)

**注意：** 次の図は、Adobe Analytics実装でSPAページが [!DNL Experience Platform Tags]. 次の節では、考慮すべき手順と問題を説明します。

## データレイヤーの設定 {#set-the-data-layer}

新しいコンテンツが読み込まれたとき、またはSPAページでアクションが発生したとき、 *最初にデータレイヤーを更新*. これは必ず起こる **前** でルールを実行するトリガーを設定するカスタムイベント [!DNL Experience Platform Tags]. これにより、データレイヤーの正しい値がタグとAdobe Analyticsにプッシュされます。

次に、サンプルデータレイヤーを示します。 これらの要素は、SPAページで実行されたアクションに応じて、最初のビューまたはその後のビューの変更に基づいて変化する場合があります。 たとえば、フルビューまたは大部分のビューの変更時には、一意の「[!DNL pageName]」の値を使用して、Adobe Analyticsレポートのビューを区別します。

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

## でカスタムイベントを設定し、これらのイベントをリッスンします。 [!DNL Experience Platform Tags] {#setting-custom-events-and-listening-in-tags}

新しいコンテンツが読み込まれたとき、またはSPAページでアクションが発生したときに、にデータを送信するルールを実行するようExperience Platformタグに通知する必要があります。 [!DNL Analytics]. これには、次の 2 つの方法があります。 [!UICONTROL ダイレクト型ルール] またはカスタムイベントを使用します。

* [!UICONTROL ダイレクト型ルール]:の設定 [!UICONTROL ダイレクト型ルール] ページから直接呼び出されると実行されます。 ページの読み込みまたはアクションが単純で、一意で、毎回特定の命令のセットを実行できる場合 ( 例えば、set [!DNL eVar4] X とトリガー [!DNL event2] 毎回 ) の場合、この方法が適切です。 参照： [!DNL Experience Platform Tags] 作成の詳細に関するドキュメント [!UICONTROL ダイレクト型ルール].
* カスタムイベント：SPAページで発生するイベントに一意の値を持つペイロードを動的にアタッチする必要がある場合は、カスタム JavaScript イベントを使用し、でリッスンします。 [!DNL Experience Platform Tags]. ペイロードを使用して、タグでデータ要素と Analytics 変数を設定します。 SPAでは通常、この方法が必要となるので、この方法がベストプラクティスと見なされます。 次の例では、カスタムイベントメソッドを使用しています。

**例：** [この](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html) ヘルプドキュメントには、を実装するサンプルSPAサイトへのリンクがあります。 [!DNL Analytics] およびその他のExperience Cloudソリューション この例では、次のカスタムイベントが使用されています。

* **[!DNL Event-view-start]**:読み込むビュー/状態のビュー開始時に実行します。
* **[!DNL Event-view-end]**:ビュー/状態の変更が発生し、ページ上のすべてのSPAコンポーネントの読み込みが完了したときに実行します。 これは、通常、Adobe Analyticsにデータを送信するイベントです。
* **[!DNL Event-action-trigger]**:表示/状態の読み込みを除く、ページでイベントが発生した場合に実行します。 この例としては、クリックイベントや、ビューを変更しない小さなコンテンツの変更などがあります。

これらのイベントが発生する方法とタイミングについて詳しくは、上記のページとドキュメントを参照してください。 実装で同じイベント名を使用する必要はありません。 使用する方法の機能上の使用例は、それぞれの推奨ベストプラクティスとして理解するのに不可欠です。 次のビデオでは、のサンプルSPAページとサンプルコードを示します。 [!DNL Experience Platform Tags] カスタムイベントをリッスンします。

>[!VIDEO](https://video.tv.adobe.com/v/23024/?quality=12)

## s.t() または s.tl() を [!DNL Experience Platform Tags] {#running-s-t-or-s-tl-in-the-launch-rule}

理解すべき重要な概念 [!DNL Analytics] SPAを使用する場合、 `s.t()` および `s.tl()`. コードは、でこれらのトリガーのいずれか 1 つをします。 [!DNL Experience Platform Tags] にデータを送信する [!DNL Analytics].

* **s.t()** - 「t」は「track」を表し、これはページビューを表します。 表示が十分に変更された場合  *検討する* 新しい「ページ」に対して、この呼び出しを使用します。 一意の値を [!DNL s.pageName] 変数と使用 `s.t()` データをに送信する [!DNL Analytics].

* **s.tl()** - 「tl」は「リンクを追跡」を表し、これはリンククリックまたは小さなコンテンツ変更を表します。 ビューの変更が最小限の場合は、 `s.tl()` インタラクションに関する一意の値をに渡す [!DNL Analytics]. 渡されたこの変数は次の値ではありません： [!DNL s.pageName](Analytics では `s.tl()` の呼び出しを受け取る。

**ヒント：** 一般的なガイドラインとして、画面が 50%以上変わった場合は、 `s.t()` ページビュー呼び出し。 それ以外の場合は、 `s.tl()`. ただし、新しい「ページ」を構成するアクションと、Adobe Analyticsレポートでのその表示方法を検討する際には、判断を活用してください。

次のビデオでは、トリガーの場所と方法を示します `s.t()` または `s.tl()` タグ内。

>[!VIDEO](https://video.tv.adobe.com/v/23048/?quality=12)

## 変数をクリア {#clear-variables}

適切なデータをに送信 [!DNL Analytics] 適切なタイミングで SPA環境で、 [!DNL Analytics] 変数が持続し、次に戻る [!DNL Analytics]に含める必要はありません。 関数が [!DNL Analytics] [!DNL Tags] 拡張機能を使用して、次の呼び出しでにデータが誤って送信されないように変数をクリアします。 [!DNL Analytics].

上の図は、クリアされた変数を示しています *後* データを送信します。 実際には、呼び出しの前または後に発生する可能性がありますが、 [!DNL Experience Platform Tags] より簡潔な実装のルール。 変数をクリアする場合 *前* 実行する `s.t()`、呼び出しの直後に新しい変数を設定し、次に新しいデータの送信に進みます。 [!DNL Analytics].

**注意：** 実行時に変数をクリアする必要はありません `s.tl()`. この呼び出しでは、 [!DNL linkTrackVars] 指示する変数 [!DNL Analytics] 設定する変数 これは自動的に発生します [!DNL Experience Platform Tags] 設定を通じて。 これにより、 `s.t()` SPA環境でを呼び出します。 最も清潔で最も信頼性の高い実装を確保するために、SPA環境では、両方の呼び出しに clear 変数関数を使用するほうが簡単な場合があります。

次のビデオでは、で変数をクリアする場所と方法を示します [!DNL Tags].

>[!VIDEO](https://video.tv.adobe.com/v/23049/?quality=12)

## その他の留意事項 {#additional-considerations}

### のカスタムコードウィンドウ [!DNL Experience Platform Tags] {#custom-code-windows-in-tags}

内 [!DNL Tags] [!DNL Analytics] 拡張機能の場合、カスタムコードを挿入する場所は 2 つあります。「[!UICONTROL ライブラリ管理]&quot;および&quot;[!UICONTROL カスタムコードを使用したトラッカーの設定]」セクション。

![タグ分析カスタムコードウィンドウ](assets/launch_analyticscustomcodewindows.png)

これらの場所のいずれかで、SPAページの最初のページ読み込みに対して、1 回だけ、そこに含まれるコードが実行されます。 ビューまたはアクションの変更時にコードを実行する場合は、そのコードを適切な **[!UICONTROL ルール]** ( 例：「ページ読み込み」:event-view-end」ルール ) を使用して、 [!UICONTROL ルール] 実行 アクションを [!UICONTROL ルール]，設定 *拡張機能=コア* および *アクションタイプ=カスタムコード*.

### 「ハイブリッド」SPAと従来のサイト {#hybrid-spa-and-traditional-sites}

一部のサイトは、従来のページとSPAページの組み合わせで構成されています。 この場合は、両方のページタイプで機能する方法を使用します。 サイト上でカスタムイベントを設定し、 [!DNL Experience Platform Tags]を使用する場合、2 回のヒットが [!DNL Analytics] ハッシュの変更などに基づいて この場合、Adobe Analyticsに渡される重複データを防ぐために、ページビューの 1 つを抑制します。

機能を一意のに分割する場合 [!UICONTROL ルール] より詳細な制御を行うには、この操作を行ったことを忘れないでください。 変更する場合 [!UICONTROL ルール]、他の [!UICONTROL ルール].

### との統合 [!DNL Target] A4T の使用 {#integration-with-target-using-a4t}

との統合時 [!DNL Target] A4T を使用して、 [!DNL Target] および [!DNL Analytics] 同じビューまたはアクションで送信されたリクエストには、同じ SDID パラメーター値が渡されます。 これにより、データがバックエンドで正しく同期されます。

これらのヒットを表示するには、デバッガーまたはパケット監視ツールを使用します。 Adobeには、この目的のExperience Platformデバッガーが用意されています。 これは、次のことが可能な Chrome 拡張機能です。 [ここにダウンロード](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=ja). [!DNL Target] は、ページで最初に実行されます。 これは、デバッガーでも確認できます。

## その他のリソース {#additional-resources}

* [アドビフォーラムでの SPA ディスカッション](https://experienceleaguecommunities.adobe.com:443/t5/adobe-experience-platform-launch/best-practices-for-single-page-apps/m-p/267940)
* [Experience Platform Launch での SPA の実装方法を示すリファレンスアーキテクチャのサイト](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html)

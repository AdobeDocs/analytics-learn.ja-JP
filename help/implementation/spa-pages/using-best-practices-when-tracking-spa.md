---
title: 単一ページアプリケーション（SPA）の実装のベストプラクティス
description: 単一ページアプリケーション（SPA）に Adobe Analytics を実装するためのベストプラクティスについて説明します。これには、推奨される実装方法である Experience Platform タグの使用が含まれます。
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
source-git-commit: 8fc641743bc9e07b838a22ca64ccc15344d52764
workflow-type: tm+mt
source-wordcount: '1313'
ht-degree: 100%

---

# 単一ページアプリケーション（SPA）の実装のベストプラクティス {#implementation-best-practices-for-single-page-appliations}

単一ページアプリケーション（SPA）での [!DNL Adobe Analytics] 実装のベストプラクティスについて説明します。これには推奨される実装方法である [!DNL Experience Platform Tags] の使用が含まれます。

最初のメモ：

* 以下のコンテンツは、サイトに Adobe Analytics を実装するための [!DNL Experience Platform Tags] の使用について説明します。これらの考慮事項は、[!DNL Experience Platform Tags] を使用しない場合にも適用されるので、実装方法に合わせて調整する必要があります。
* SPA には違いがあるので、ニーズに最も合うようにアプローチを調整する必要があります。

## [!DNL Experience Platform Tags] での SPA の操作に関する簡単な図 {#simple-diagram-of-working-with-spas-in-tags}

![タグでの分析用 SPA](assets/spa_for_analyticsinlaunch.png)

**メモ：**&#x200B;これは [!DNL Experience Platform Tags] を使用した Adobe Analytics 実装において、SPA ページがどのように処理されるかを簡単に示した図です。次の節では、考慮すべき手順と問題を説明します。

## データレイヤーの設定 {#set-the-data-layer}

新しいコンテンツの読み込み時、または SPA ページでのアクション発生時は、*最初にデータレイヤーを更新*&#x200B;します。これは [!DNL Experience Platform Tags] でルールをトリガーするカスタムイベントが実行される&#x200B;**前に**&#x200B;行う必要があります。これにより、正しい値がデータレイヤーからタグに、その後 Adobe Analytics にプッシュされます。

次に、サンプルデータレイヤーを示します。これらの要素は、最初のビューや、SPA ページで実行されたアクションによるその後のビューの変更に基づいて変更する場合があります。例えば、フルビューまたは大部分のビューの変更時には、Adobe Analytics のレポートにおいてビューを区別するために一意の「[!DNL pageName]」値を渡すことが一般的な要件となっています。

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

## [!DNL Experience Platform Tags] でカスタムイベントを設定し、これらのイベントをリッスンします。 {#setting-custom-events-and-listening-in-tags}

新しいコンテンツの読み込み時、または SPA ページでのアクション発生時は、[!DNL Analytics] にデータを送信するルールを実行するよう Experience Platform タグに通知する必要があります。これには、[!UICONTROL 直接呼出しルール]またはカスタムイベントの 2 つの方法があります。

* [!UICONTROL 直接呼出しルール]：ページから直接呼び出される際に実行される[!UICONTROL 直接呼出しルール]を設定します。ページの読み込みまたはアクションが単純または一意で、毎回特定の命令のセットを実行できる場合は（例えば、[!DNL eVar4] を X に設定し、毎回 [!DNL event2] をトリガーする） 、この方法が適しています。[!UICONTROL 直接呼出しルール]作成について詳しくは、[!DNL Experience Platform Tags]ドキュメント を参照してください。
* カスタムイベント：SPA ページで発生するイベントに一意の値を持つペイロードを動的に添付する必要がある場合は、カスタム JavaScript イベントを使用し、[!DNL Experience Platform Tags] でリッスンします。 ペイロードを使用して、タグでデータ要素と Analytics 変数を設定します。SPA ではこのニーズが一般的であるため、このメソッドがベストプラクティスと見なされます。次の例では、カスタムイベントメソッドを使用しています。

**例：** [この](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=ja)ヘルプドキュメントには、[!DNL Analytics] を実装するサンプル SPA サイトおよびその他の Experience Cloud ソリューションへのリンクがあります。これらの例では、次のカスタムイベントが使用されています。

* **[!DNL Event-view-start]**：読み込むビュー／状態のビュー開始時に実行します。
* **[!DNL Event-view-end]**：ビュー／状態の変更が発生し、ページ上のすべての SPA コンポーネントの読み込み完了時に実行します。これは、通常、Adobe Analytics にデータを送信するイベントです。
* **[!DNL Event-action-trigger]**：ビュー／状態の読み込みを除き、ページでのイベント発生時に実行します。この例は、クリックイベントか、ビューの変更を伴わない小さなコンテンツの変更を含みます。

これらのイベントの発生の仕方とタイミングについて詳しくは、上記のページとドキュメントを参照してください。実装で同じイベント名を使用する必要はありません。使用されるメソッドの機能的なユースケースは、それぞれの推奨ベストプラクティスとして理解するのに不可欠です。次のビデオでは、カスタムイベントをリッスンする [!DNL Experience Platform Tags]でのサンプル SPA ページとサンプルコードを説明します。

>[!VIDEO](https://video.tv.adobe.com/v/23024/?quality=12&learn=on)

## [!DNL Experience Platform Tags] で s.t() または s.tl() を実行する {#running-s-t-or-s-tl-in-the-launch-rule}

SPA の操作をする際に [!DNL Analytics] について理解しておくべき重要な概念は、`s.t()` および `s.tl()`の違いです。コードは、[!DNL Experience Platform Tags] でこれらのメソッドのうち 1 つまたはその他をトリガーし、[!DNL Analytics] にデータを送信します。

* **s.t()** - 「t」は「track」を指し、ページビューを表します。ビューが新しい「ページ」として&#x200B;*見なされる*&#x200B;程度に変更された場合は、この呼び出しを使用します。一意の値を [!DNL s.pageName] 変数に設定し、`s.t()` を使って [!DNL Analytics] にデータをに送信します。

* **s.tl()** - 「tl」は「トラックリンク」の意味で、リンククリックまたは小規模なコンテンツ変更を表します。ビューの変更が最小限の場合は、`s.tl()` を使用して、インタラクションに関する一意の値を [!DNL Analytics] に渡します。渡された変数は [!DNL s.pageName] ではないので、`s.tl()` の呼び出しを受信したときに Analytics で無視されます。

**ヒント：** 一般的なガイドラインとして、画面が 50%以上変わった場合は、`s.t()` ページビュー呼び出しを使用します。 それ以外の場合は、`s.tl()` を使用します。 ただし、新しい「ページ」を構成するアクションと、Adobe Analytics レポートでの表示方法を検討する際には、ご自身で判断するようにしてください。

次のビデオでは、タグで `s.t()` または `s.tl()` をトリガーする場所と方法を示します。

>[!VIDEO](https://video.tv.adobe.com/v/23048/?quality=12&learn=on)

## 変数のクリア {#clear-variables}

適切なデータを的確なタイミングで [!DNL Analytics] に送信します。SPA 環境では、[!DNL Analytics] 変数に格納された値が保持され、不要になった時点で [!DNL Analytics] に再送信される可能性があります。[!DNL Analytics] [!DNL Tags] 拡張機能には、次回の呼び出しで誤って [!DNL Analytics] にデータを送信しないように変数をクリアする関数があります。

上の図は、データを送信した&#x200B;*後*&#x200B;にクリアされた変数を示しています。実際には、呼び出しの前でも後でも構いませんが、[!DNL Experience Platform Tags] のルールの一貫性を保つことで、よりクリーンな実装が可能になります。`s.t()` を実行する&#x200B;*前*&#x200B;に変数をクリアする場合、呼び出しの直後に新しい変数を設定したあと、新しいデータを [!DNL Analytics] に送信します。

**注意：**`s.tl()`を実行するたびに変数のクリアが必要になるわけではありません。この呼び出しでは、[!DNL linkTrackVars] 変数を使用して、設定する変数を [!DNL Analytics] に指示する必要があります。これは、設定を通じて [!DNL Experience Platform Tags] で自動的に行われます。SPA 環境での `s.t()` 呼び出しの動作とは異なり、誤った変数が設定されるのを防ぐことができます。最もクリーンで最も信頼性の高い実装を確保するために、SPA 環境では、両方の呼び出しに変数クリア関数を使用する方が簡単な可能性があります。

次のビデオでは、[!DNL Tags] で変数をクリアする場所と方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/23049/?quality=12&learn=on)

## その他の留意事項 {#additional-considerations}

### [!DNL Experience Platform Tags] のカスタムコードウィンドウ {#custom-code-windows-in-tags}

[!DNL Tags] [!DNL Analytics] 拡張機能でカスタムコードを挿入できる場所としては、「[!UICONTROL ライブラリ管理]」セクションと「[!UICONTROL カスタムコードを使用したトラッカーの設定]」セクションの 2 つがあります。

![Tags Analytics のカスタムコードウィンドウ](assets/launch_analyticscustomcodewindows.png)

これらの場所のいずれかで、SPA ページの最初のページ読み込みに対して、そこに含まれるコードが 1 回だけ実行されます。 ビューまたはアクションの変更時にコードを実行する場合は、そのコードを適切な&#x200B;**[!UICONTROL ルール]**（例：「ページの読み込み：イベント／表示／終了」ルール ）に実装して、その[!UICONTROL ルール]が実行されるたびにコードが確実に実行されるようにします。[!UICONTROL ルール]でそのアクションを作成するときは、*拡張機能 = コア*&#x200B;と&#x200B;*アクションタイプ = カスタムコード*&#x200B;を設定します。

### 「ハイブリッド」SPAと従来のサイト {#hybrid-spa-and-traditional-sites}

一部に、従来のページと SPA ページの組み合わせで構成されているサイトがあります。このような場合は、両方のページタイプで機能する戦略を使用します。サイト上でカスタムイベントを設定し、[!DNL Experience Platform Tags] でルールをトリガーする場合は、ハッシュの変更などに基づいて重複ヒットが [!DNL Analytics] に送信されないようにしてください。この場合は、ページビューの 1 つを抑制して、Adobe Analytics に重複データが渡されないようにします。

より詳細な制御を行うために、機能を一意の[!UICONTROL ルール]に分ける場合は、それを行ったことをドキュメントに残しておくことを忘れないでください。一方の[!UICONTROL ルール]を変更する場合は、もう一方の[!UICONTROL ルール]にも同じ変更を行うようにします。

### A4T を使用した [!DNL Target] との統合 {#integration-with-target-using-a4t}

A4T を使用して [!DNL Target] と統合する場合は、同じビューまたはアクションで送信された [!DNL Target] および [!DNL Analytics] リクエストが同じ SDID パラメーター値を渡すことを確認します。これにより、データがバックエンドで正しく同期されます。

これらのヒットを表示するには、デバッガーまたはパケット監視ツールを使用します。 アドビでは、このための Experience Platform デバッガーを提供しています。これは Chrome 拡張機能で、[ここからダウンロード](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=ja)できます。 [!DNL Target] は、ページで最初に実行される必要があります。これは、デバッガーでも確認できます。

## その他のリソース {#additional-resources}

* [アドビフォーラムでの SPA ディスカッション](https://experienceleaguecommunities.adobe.com:443/t5/adobe-experience-platform-launch/best-practices-for-single-page-apps/m-p/267940)
* [Experience Platform Launch での SPA の実装方法を示すリファレンスアーキテクチャのサイト](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=ja)

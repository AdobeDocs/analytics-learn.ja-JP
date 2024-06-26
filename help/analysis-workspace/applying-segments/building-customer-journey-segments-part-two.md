---
title: カスタマージャーニーセグメントの作成 — 第 2 部
description: パート 2 では、購入およびリテンション訪問の目的セグメントを構築して、顧客の購入ジャーニーを把握し、コンテンツをパーソナライズする方法を説明します。 「Book Now」のクリックやログインなどのシグナルを使用して、効果的な分析とターゲットマーケティングのための購入と保持の意図を特定します。
feature: Segmentation
role: User
level: Experienced
last-substantial-update: 2023-07-21T00:00:00Z
jira: KT-13476
thumbnail: KT-13476.jpeg
source-git-commit: bc3bf5b22e3cf5a9d77e3fe8aa2d86c65a7eaefb
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 0%

---


# カスタマージャーニーセグメントの作成 — 第 2 部

パート 2 では、購入およびリテンション訪問の目的セグメントを構築して、顧客の購入ジャーニーを把握し、コンテンツをパーソナライズする方法を説明します。 「Book Now」のクリックやログインなどのシグナルを使用して、効果的な分析とターゲットマーケティングのための購入と保持の意図を特定します。

## 購入およびリテンション訪問の目的セグメントの作成

最後の投稿では、訪問意図セグメントの作成プロセスを説明し、最初の訪問意図セグメント「One Hit Wonders」を構築しました。 今日は、購入および定着セグメントを作成します。 訪問の約 23%をセグメント化し、残りの訪問目的セグメント用のプレースホルダーを作成しました。

![画像 1](assets/Image-1.png)

現在構築中の訪問意図セグメントは、訪問者ベースのカスタマージャーニーセグメントを構築する基盤となりました。 訪問インテントセグメントを作成したら、これらの訪問者ベースのジャーニーセグメントを作成します。

訪問意図セグメントの作成は削除のプロセスであることを思い出してください。 これらのセグメントを時系列で作成するのではありません 定義が簡単で難しい順に訪問インテントセグメントを作成しています。

1. 目的：0 - 1 ヒットの驚異
1. 目的：3 — 購入
1. 目的：4 — リテンション
1. 目的：2 — 検討
1. 目的：1 — 認識

最後の投稿では、旅行業界にいるので、「Purchase」セグメントを「Booking」と呼びました。 しかし、今後は、複数の業界に簡単に適用できるように、これを「購入」セグメントと呼びます。

シグナルが明確になるほど、セグメントの作成が容易になります。 最後の投稿では、バウンスしたトラフィックなので、最も簡単に定義できた「ワンヒットワンダーズ」セグメントを作成しました。 購入およびリテンションのインテントセグメントは、非常に明確なシグナルに基づいているので、非常に簡単に定義できます。

## 顧客ジャーニーは購入傾向とは異なる

購入意図セグメントの構築について見てみると、顧客のジャーニー内での位置を識別する傾向とは異なることを覚えておくことが重要です。 一部の購入傾向モデルでは、Web 訪問者をスコアリングして、購入の可能性を予測することができます。 これらのモデルは非常に便利ですが、現在構築する購入インテントセグメントとは異なります。

傾向モデルが訪問者が購入するかどうかを予測しようとしている間、訪問の目的セグメントは、人が購入ジャーニーのどこにいるかを把握しようとしています。 意図セグメントを使用してお客様の考え方を理解すると、コンテンツをパーソナライズし、マーケティングを調整して、販売パイプラインを促進する適切なトラフィックを促進できます。 したがって、購入インテントセグメントは、訪問者が購入を探していることを示す明示的な行動シグナルを探します。

## 購入訪問の目的セグメントの作成

購入訪問の目的セグメントは簡単に定義できます。 私の場合は「今すぐ予約」ボタンをクリックした人は誰でもクルーズ予約の意図を示しています これは、オンライン小売業者の「チェックアウト」をクリックすること、またはメディアコンテキストの「購読」リンクをクリックすることに似ています。

購入意図を推測するために使用するシグナルを決定する際には、いくつかの判断を行う必要があります。 購入意図セグメントにすべての購入を含めて欲しいのですが、コンバージョン率は 100%にはできません。 このセグメントでは、購入確認ページや「ありがとうございました」ページは使用しません。

同様に、購入の確認ページ（または購入確認の直前）も、分析やターゲティングに役立つように、ファネルが非常に下がりすぎる可能性が高くなります。

ファネルをさらに上に進むと、顧客が購入する意向を示すシグナルが役立つかどうかが明確になりません。 私の場合、「Book Now」は小売の「Checkout」リンクに似ており、これが私が使用したシグナルです。 しかし、小売のコンテキストでは、「チェックアウト」は、ファネルや「買い物かごを表示」または「買い物かごに追加」の方が長すぎる可能性があります。

これは食料品店のようなものだと考えられます 誰かが棚から商品を取り出して、それを買うつもりではない。 買い物かごに入れても、すぐに棚に戻すこともできます。 でも買い物かごに入れて歩き回ったら買い物をするチャンスは非常に高いです そして、彼らがその製品と一緒にチェックアウトラインに入ったら、彼らが買うのはかなり良い賭けです。

訪問したページや他の明示的な購入インテントシグナルを使用し、より直接的でない他のシグナルを避けて購入インテントを識別することをお勧めします。 例えば、セッションの数やセッションのページ数などは使用しません。 これらの間接シグナルは、購入インテントではなく、検討を示します。 このセグメントの目的は、訪問者の傾向ではなく、訪問に対する訪問者の意図を推測することです。

### Analytics Workspace を使用した購入インテントシグナルの識別

フォールアウトレポートは、購入意図を示す良好なシグナルを識別するのに非常に役立ちます。 論理的に意図を示す場所を探します。 そのステップへの注目すべきフォールアウトが表示されたら、そのステップが意図を示していることを確認できます。その後で、多くの場合、そのステップの小さいフォールアウトが表示されます。

![画像 2](assets/Image-2.png)

また、サイトの様々なページに関連するコンバージョン率を調べるのにも便利です。 これは、購入意図を示すが購入に必要でない可能性のあるページ（ファイナンスページ、購入設定ページなど）を識別する場合に特に役立ちます。

![画像 3](assets/Image-3.png)

最後に、購入開始から購入確認までのすべてのページをセグメントに含めることが重要です。 訪問者は、異なる時点で直帰し、購入フローに再度入ることができます。

### 他のセグメントの除外

最初の投稿から、訪問意図セグメントは、相互に排他的で完全に網羅的である必要があることを思い出してください。 これは、このシリーズで多くを聞くリフです。

購入意図セグメントに「1 回」と「完了」セグメントが含まれていないことを確認します。 購入インテントに使用するシグナルは非常に具体的なので、「1 回」および「完了」セグメントのみ除外する必要があります。

「1 回」セグメントと「完了」セグメントを除外すると、チェックアウトページでサイトに再度入った人が除外される場合があります。 これは問題ありません。「1 回」と「完了」の定義は 1 つのページビューです。つまり、訪問者がチェックアウトページに入ったり更新した場合でも、訪問は進行しなかったので、購入目的の式は存在しません。

### セグメントビルダーの購入インテントセグメント

購入インテントのセグメント定義は非常に簡単です。

訪問コンテナを使用して、購入する意図を明示的に示すページや他のアクションを含めます。 複数の include 条件がある場合、必ず「And」条件で結合されたコンテナに入れます。

「And」条件で結合されたセグメントに Exclude コンテナを追加します。 「 1 ヒットの驚異」セグメント定義（ページビュー数が 1 に等しい）を「除外」コンテナに追加します。

![画像 4](assets/Image-4.png)

ベストプラクティスとして、必ずコンテナにラベルを付けてください。 特に、セグメント定義がより複雑になるので、嬉しいことです。

購入インテントセグメントを構築したので、訪問インテントデータ品質ワークスペースを使用して、購入インテントセグメントが「1 回」および「完了」セグメントと相互に排他的であることを確認できます。

![画像 5](assets/Image-5.png)

## リテンション訪問インテントセグメントの作成

クルーズビジネスでは、多くのお客様が弊社のウェブサイトに来て予約を管理しますが、必ずしも購入する必要はありません。 サイトに来て、旅行情報を入力したり、旅程を確認したり、夕食の予約をしたり、他の多くのものを、クルーズに買い物をしないで行くことができます。 また、お客様は、ショアでの行き来や体験の向上を購入することもできます。 これらの機能強化は保持の一部と見なされるので、予約セグメント（このブログシリーズでは「購入」と呼んでいます）とは別に保持しています。

小売の顧客は、返品をしたり、ロイヤルティプログラムを管理したりできます。 メディアまたはテクノロジーの購読者が製品を使用している可能性があります。 お客様が Web サイトを訪問して、お客様との関係を管理している場合、これはリテンション訪問であり、これらのシグナルを確認する必要があります。 また、メディア、テクニカル、オンラインバンキングなどのオンライン製品を提供する場合、このシリーズでは説明しない他の多くの種類の訪問意図セグメントが存在する可能性があります。

購入目的セグメントと同様に、目的が明確に示されていることを探しています。 私にとっては、サイトのセクション全体がクルーズの管理専用なので、ページを簡単に特定できます。 これは、他の企業にとってはより複雑な作業になる場合があります。 ログイン数、アカウント管理数、サポートページへの訪問数などのシグナルを探します。

訪問者がサイトにいないので、「リテンション」はこの訪問目的では少しぎこちない名前です。「お客様として保持できます」という理由です。 リテンションは、その訪問に対する当社の意図です。 お客様に共感を持って、お客様に最初の焦点を合わせてください。

### Analytics Workspace を使用したリテンションインテントシグナルの特定

繰り返しますが、Analytics Workspace はリテンションインテントを識別するのに役立ちます。 ページ、サイトセクションまたはカスタムセグメントディメンションを使用して、ページを分類できます。 購入コンバージョン率の低いページを探します。 この例では、オンラインチェックインページとショアエクスカージョン (Shorex) ページは、買い物と購入により論理的に関連した他のページよりも、コンバージョン率が比較的低いことがわかります。

![画像 6](assets/Image-6.png)

また、Workspace で高トラフィックのページを調べることもお勧めします。 高トラフィックのページのリストをスキャンし、リテンションの意図を示しているかどうかを判断します。

## 他のセグメントの除外

繰り返しますが、訪問インテントのセグメントは、相互に排他的で完全に網羅的である必要があります。 まだこれを読むのに飽きないなら、そうなるでしょう！ リテンションインテントセグメントでは、購入インテントの行動を除外することが非常に重要です。

ほとんどのユーザーにとって、購入意図とリテンション意図は相互に排他的な行動ではありません。 今後のクルーズを管理するために Web サイトに来たお客様がいますが、次回の旅行を予約するために来られました（ありがとうございます）。 レストランの場合、訪問者は、ロイヤルティポイントを確認し、オンラインで注文をすることができます。

動作が相互に排他的でない場合でも、セグメントは顧客ジャーニー分析用にする必要があります。 他の非常に興味深いセグメントを作成して、購入行動とロイヤルティ行動の間の重複を分析できます。 ただし、現在の目的では、これらのセグメントを相互に排他的にする必要があります。

需要生成はマーケティングの主な目標の 1 つなので、リテンションインテントセグメントは購入意図を除外します。 つまり、誰かがクルーズを管理するためにサイトを訪れ、新しいクルーズを予約する意図を示した場合、その訪問は購入目的セグメントに移動します。

### セグメントビルダーのリテンションインテントセグメント

セグメント定義がもう少し一般的になってきています。 訪問回数をセグメントに含めます。 リテンションインテントシグナルを追加します。 私にとって、これは単純でした。 ページ名が「bge:」（予約済みのゲストページ）で始まる場合、このセグメントに属しています。 追加の測定のために、ページビュー数が 1 より大きいを追加しました（ただし、以下のヒット数の驚異は 1 つ除外されます）。

次に、「1 回のヒットの奇跡」と「購入意図」の訪問用の除外コンテナを追加します。 コンテナが「And」条件と結合されていることを確認します。

![画像 7](assets/Image-7.png)

再度、訪問意図データ品質ワークスペースを調べて、セグメントが相互に排他的であることを確認します。 訪問意図セグメントがうまく形成されています。

![画像 8](assets/Image-8.png)

この時点で、5 つの訪問インテントセグメントのうち 3 つを設定しました。 これらのセグメントは相互に排他的です。 次の投稿では、最終的な訪問目的のセグメント、検討と認識を作成し、すべてのセグメントを完全に網羅的に説明します。 訪問の目的セグメントを設定したら、それらを訪問者ベースのセグメントにまとめ、分析やパーソナライゼーションに非常に役立てます。

## 作成者

このドキュメントの作成者：

![アロンフォッサム](assets/aaron-headshot.png)

**アロンフォッサム**, Director, Digital Analytics

Adobe Analytics チャンピオン

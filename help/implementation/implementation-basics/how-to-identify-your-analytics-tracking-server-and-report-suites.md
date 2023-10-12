---
title: Analytics トラッキングサーバーとレポートスイート ID を識別する方法
description: Adobe Analyticsを設定する場合、または他のExperience Cloudソリューションで参照する場合、多くの場合、使用している Analytics の「トラッキングサーバー」や、データの送信先の「レポートスイート」を把握しておくことが役立ちます。 このビデオでは、Adobe Analytics が実装済みかどうかに関係なく両方の値を見つける方法を説明します。
feature: Implementation Basics
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 2358
role: Developer, Data Engineer
level: Beginner
exl-id: 3925026f-69f1-4425-b3a9-6fef26375fed
source-git-commit: 42bf16df9585d1f41206b81bf509a72c10f1d7f2
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 17%

---

# 分析を識別する方法 [!DNL tracking server] および [!UICONTROL レポートスイート ID] {#how-to-identify-your-analytics-tracking-server-and-report-suites}

Adobe Analyticsを設定する場合、または他のExperience Cloudソリューションで参照する場合、多くの場合、使用している Analytics の「トラッキングサーバー」や「[!UICONTROL レポートスイート]」と入力します。 このビデオでは、Adobe Analytics が実装済みかどうかに関係なく両方の値を見つける方法を説明します。

>[!IMPORTANT]
>
>この記事とビデオは、Web SDK を使用した実装ではなく、Adobe Analyticsの「AppMeasurement」実装に適用されます。

## 導入後 {#after-implementation}

サイトに Analytics を実装した後、 [!DNL tracking server] そして [!DNL report suite ID] トラッキングビーコン内で The [!DNL tracking server] がビーコン内のホスト名なので、見つけやすくなります。 The [!UICONTROL レポートスイート] ID は、ビーコンのパス名の「/b/ss/」の直後にある、コンマ区切りのリストです。

ビーコンを確認するには、および Analytics やその他のExperience Cloudソリューションで利用できるその他すべての情報と共に、 [「Experience Cloud Debugger」Chrome 拡張機能](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj?hl=ja).

## 実装前 {#before-implementation}

**[!DNL Tracking server]** - Adobe Analyticsの実装をまだ開始していない場合、「.sc.omtrdc.net」のサブドメインを選択します。 [!DNL tracking server]. 例えば、「Jim&#39;s Brims」というオンラインの帽子店があるとします。 この場合は、[!DNL tracking server] を次のように設定するだけです。

&quot;jimsbrims.sc.omtrdc.net&quot;.

**[!UICONTROL レポートスイート]**  — リストを検索するには、 [!UICONTROL レポートスイート] 作成済みの [!DNL Analytics] をクリックし、 [!UICONTROL 管理者] > [!UICONTROL レポートスイート] をクリックして、 [!UICONTROL レポートスイート]（ID やタイトルを含む）

詳しくは、以下のビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/26061/?quality=12&learn=on)

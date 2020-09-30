---
title: Analyticsトラッキングサーバーとレポートスイートの識別方法
description: Adobe Analyticsを設定する場合、または他のExperience Cloudソリューションでこのレポートを参照する場合、多くの場合、使用しているAnalyticsの「トラッキングサーバー」や、データを送信する「レポートスイート」を知っておく必要があります。 このビデオでは、Adobe Analyticsを既に導入済みかどうかに関係なく、両方の値を見つける方法を説明します。
feature: implementation basics
topics: null
audience: implementer
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 2358
translation-type: tm+mt
source-git-commit: 60f4ce4f563a990576b3331b01cd87c29d424f43
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Analyticsおよび [!DNL Tracking Server][!UICONTROL レポートスイートの識別方法] {#how-to-identify-your-analytics-tracking-server-and-report-suites}

Adobe Analyticsを設定する場合、または他のExperience Cloudソリューションでを参照する場合は、多くの場合、使用している「 [!DNL Analytics] 」や、データを送信する「[!DNL Tracking Server]レポートスイート」を知っておくことが役立ちます。 このビデオでは、Adobe Analyticsを既に導入済みかどうかに関係なく、両方の値を見つける方法を説明します。

## 導入後 {#after-implementation}

サイト [!DNL Analytics] に導入した後、トラッキングビーコン [!DNL tracking server] の「」と「」 [!DNL report suite ID] の右側を確認できます。 は、ビーコン [!DNL tracking server] 内のホスト名であるため、見つけやすくなります。 レ [!UICONTROL ポートスイート] IDは、ビーコンのパス名の「/b/ss/」の直後にあるコンマ区切りのリストです。

ビーコン、およびその他のExperience Cloudソリューションで使用されるすべての情報を確認するに [!DNL Analytics] は、 [「Experience Cloud Debugger」 Chrome Extension](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj?hl=ja)。

## 導入前 {#before-implementation}

**[!DNL Tracking Server]**  — まだAdobe Analyticsの実装を開始していない場合は、「.sc.omtrdc.net」のサブドメインを選択 [!DNL tracking server]します。 例えば、「Jim’s Brims」という名前のオンライン帽子店があるとします。 私は次のように設定するだけ [!DNL tracking server] です。

&quot;jimsbrims.sc.omtrdc.net&quot;と入力します。

**[!UICONTROL Report Suite]** — 作成済みのレポートスイートのリストを探すには、ログインして管理 [!UICONTROL 者][!DNL Analytics]/レポートスイートに移動します。トップメニューには、リストのレポートスイートのIDタイトルとIDタイトルが含まれています。

詳しくは、以下のビデオを参照してください。

>[!VIDEO](https://video.tv.adobe.com/v/26061/?quality=12)

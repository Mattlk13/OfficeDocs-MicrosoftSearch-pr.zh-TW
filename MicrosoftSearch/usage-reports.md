---
title: 搜尋使用方式報告
ms.author: ankmis
author: jeffkizn
manager: parulm
ms.topic: article
ms.service: mssearch
audience: Admin
ms.audience: Admin
ms.date: 09/24/2021
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
description: 複查 Microsoft 搜尋流量報告
ms.openlocfilehash: d8322921b9008f9000c035d21a06cc5aa9d87d8c
ms.sourcegitcommit: 31b48dace4cf397f72bf28d7ec1e239e0f8a431c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/30/2021
ms.locfileid: "61234412"
---
# <a name="microsoft-search-usage-reports"></a>Microsoft 搜尋使用方式報告

搜尋使用方式報告可讓您深入瞭解搜尋在組織中的運作方式。 從這些報告產生的洞察力會協助您採取動作，讓使用者更有意義和 delightful 的體驗。

> [!IMPORTANT]
> Microsoft 搜尋使用狀況報告目前正在預覽中

[Microsoft 搜尋使用狀況報告](https://admin.microsoft.com/Adminportal/Home?#/MicrosoftSearch/insights)包含從搜尋所產生的圖形和表格，該搜尋會從 SharePoint Home (所執行的網站，該網站的 URL 會以/SharePoint .aspx) 、Office .com 及 Microsoft 搜尋于 Bing 工作] 索引標籤搜尋方塊中。 您可以看到過去31天、每天或每月過去一年的資料。 這些報告只會產生，所以需要一些時間才能累算歷史資料。

> [!div class="mx-imgBorder"]
> ![搜尋使用方式報告儀表板。](media/usage-reports/usage_reports_v2.png)

## <a name="overview-of-search-reports"></a>搜尋報告概述

| 報告 | 描述 |
|:-----|:-----|
|查詢磁片區|此報告顯示所執行的搜尋查詢數。 使用此報告可識別搜尋查詢量的趨勢，並決定高和低搜尋活動的時段。|
|主要查詢|此報告顯示最常用的搜尋查詢。 當搜尋至少三次以按一下結果時，會將查詢新增至此報告。 使用此報告可瞭解使用者搜尋的資訊類型。|
|放棄的查詢|此報告顯示可接收低點擊式的常用搜尋查詢。 使用此報告可識別出可能造成使用者不滿意的搜尋查詢，以改善內容的可探索性。 然後，您就可以判斷是否建立答案（如書簽），或透過 Graph 連接器 ingesting 新內容是正確的動作。|
|無結果查詢|此報告顯示傳回查無結果的常用搜尋查詢。 使用此報告可識別出可能造成使用者不滿意的搜尋查詢，以改善內容的可探索性。 然後，您就可以判斷是否建立答案（如書簽），或透過 Graph 連接器 ingesting 新內容是正確的動作。|

>[!NOTE]
>目前有一個已知問題，如書簽等答案所滿足的查詢會計為放棄的查詢。

## <a name="viewing-reports"></a>查看報告

當您流覽至 [使用狀況報告] 頁面時，所有報告都可供查看。 您可以使用日期篩選器挑選要查看的特定日或月份。

下載報告可讓您查看更多時間範圍內的報告。 按一下 [下載箭號]，然後選取 [ **過去31天** ] 或 [ **最近12個月**]。 報表會下載成 Excel 試算表。 如果您選取過去31天，試算表會每日有個別的索引標籤。 過去12個月下載將每月都有一個 tab 鍵。

## <a name="frequently-asked-questions"></a>常見問題集

**當我選取過去31天或過去12個月時，我為何必須選擇特定的一天或特定月份。**

Microsoft search 流量報告中的 [行事曆] 視圖是兩個步驟的處理常式。 先從下拉式清單中選取日期範圍 (過去31天或過去12個月內) ，然後選取 [開始日] 或 [月]。

上、放棄和失敗的查詢表會顯示從一天或一個月份所選擇的結果。

**何時會看到過去7天、過去30天的匯總資料，等等 ...？**

我們正在考慮這種類型的匯總，並簡化未來版本報告的資料範圍篩選。

**為什麼我無法透過不同的應用程式 (來源來查看使用狀況報告的明細) ？**

目前不提供依來源篩選的功能。 報告會合並搜尋 SharePoint Home 和 Office .com。 我們的下一個版本將會包含來源篩選，因此您可以看到每個應用程式特有的計量。

**其他的使用方式報告篩選？**

我們正在處理更多篩選器，可協助您的組織更細微地瞭解搜尋使用方式。 例如，您將可以查看特定地理位置或部門的查詢磁片區。

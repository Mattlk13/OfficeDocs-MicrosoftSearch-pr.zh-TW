---
title: 搜尋使用方式報告
ms.author: ankmis
author: jeffkizn
manager: parulm
ms.topic: article
ms.service: mssearch
audience: Admin
ms.audience: Admin
ms.date: 01/04/2022
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
description: 複查 Microsoft 搜尋流量報告
ms.openlocfilehash: 18f41397ba6490add9a86f4b9beedcafb246f97d
ms.sourcegitcommit: c53585e119ada9875816d35423e6babcf2534652
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2022
ms.locfileid: "61787975"
---
# <a name="microsoft-search-usage-reports"></a>Microsoft 搜尋使用方式報告

搜尋使用方式報告可讓您深入瞭解搜尋在組織中的運作方式。 從這些報告產生的洞察力會協助您採取動作，讓使用者更有意義和 delightful 的體驗。

[Microsoft 搜尋使用狀況報告](https://admin.microsoft.com/Adminportal/Home?#/MicrosoftSearch/insights)包含從搜尋所產生的圖形和表格，該搜尋會從 SharePoint Home (所執行的網站，該網站的 URL 會以/SharePoint .aspx) 、Office .com 及 Microsoft 搜尋于 Bing 工作] 索引標籤搜尋方塊中。 您可以看到過去7天、14天、31天或每月的資料（去年）。

:::image type="content" source="media/usage-reports/usage-reports-v3.png" alt-text="顯示 [搜尋使用狀況] 圖表和表格的報表儀表板。" lightbox="media/usage-reports/usage-reports-v3.png":::

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

下載報告可讓您查看更多時間範圍內的報告。 報表會根據選取的日期篩選，下載為 Excel 試算表。 如果您選擇 [7]、[14] 或 [31 天]，試算表每日會有個別的索引標籤。 過去12個月下載將每月都有一個 tab 鍵。

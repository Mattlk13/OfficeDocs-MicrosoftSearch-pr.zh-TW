---
title: 搜尋使用量報告
ms.author: efrene
author: efrene
manager: scotv
ms.topic: article
ms.service: mssearch
audience: Admin
ms.audience: Admin
ms.date: ''
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
description: 檢閱 Microsoft Search 使用量報告
ms.openlocfilehash: 064ab3a68daf2cc8c147dd8dc54324aa54ea27aa
ms.sourcegitcommit: 1fd99bd7e15392dba3a0d9339263469bbb021c01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/14/2022
ms.locfileid: "66795151"
---
# <a name="microsoft-search-usage-reports"></a>Microsoft 搜尋使用量報告

搜尋使用量報告可讓您深入瞭解組織中的人員如何使用 Microsoft Search。 從這些報表產生的深入解析，可協助您採取可讓所有使用者更實用且令人滿意的搜尋體驗的動作。   

**Microsoft 搜尋使用量報告** 包含從 SharePoint 起始頁執行的搜尋產生的圖表和資料表， (網站的 URL 結尾為 /SharePoint.aspx) 、Office.com，以及 Bing 中 Microsoft Search 的工作索引標籤搜尋方塊。 您可以看到過去 7 天、過去 14 天、過去 31 天或過去 12 個月的資料。   

目前您可以依國家/地區、國家/地區、部門或部門篩選這些報告。 為了保護隱私權，如果任何篩選器顯示五個或更少個人的資料，這些結果將不會包含在搜尋使用量報告中。 此外，您可以在 [組織設定] 頁面上，針對整個組織開啟或關閉這些篩選準則，以防您的組織有特定的隱私權需求。  

:::image type="content" source="media/usage-reports/usage-analytics.png" alt-text="包含圓形圖、圖表和搜尋分析報表資料的儀表板。" lightbox="media/usage-reports/usage-analytics.png":::

## <a name="how-to-get-to-the-microsoft-search-usage-reports"></a>如何取得 Microsoft Search 使用量報告？ 

1. 在 [Microsoft 365 系統管理中心中，選取 [**設定]**，然後選取 **[搜尋和智慧]**。  
2. 在 [ **搜尋與智慧]** 頁面上，選取 [ **深入解析] 索引** 標籤，然後選取 [ **使用方式分析]**。 

搜尋使用量報告可供具有 **搜尋系統管理員**、 **搜尋編輯** 器或 **全域系統管理員** 角色的使用者使用。

## <a name="what-reports-are-available-to-me"></a>有哪些報表可供我使用？ 

[Microsoft 搜尋使用量報告] 頁面會透過下列四份報告提供搜尋資料：

- **最近的搜尋活動** – 此圖表提供人員如何在組織中使用搜尋的快速檢視。 
- **查詢** – 本節顯示依使用者動作、國家/地區、國家/地區、部門或部門的查詢活動明細。 它也可讓您移至查詢詳細資料頁面，以更詳細地檢視和分析查詢。 
- **使用者** – 本節顯示已對搜尋應用程式執行搜尋的唯一使用者和參與使用者總數，以及使用頁面頂端的篩選準則選取的日期範圍。 它也可讓您移至使用者詳細資料頁面，以更詳細地檢視和分析使用者的資料。
- **連線分析** – 本節提供連線的分析。 檢閱使用連線中搜尋結果的查詢和按一下。 它也可讓您移至連線分析詳細資料頁面，以更詳細地檢視和分析連線資料。 

您可以按一下連結來檢視 [更多有關查詢](queries-usage-reports.md)、 [使用者](users-search-reports.md)和 [連線分析](connection-analytics-reports.md) 區段的詳細資料。 

> [!NOTE]
> 這些搜尋使用量報告會根據 Bing (工作垂直) 、Office.com 和 SharePoint 起始頁面的搜尋流量來顯示集體搜尋資料。 您也可以透過個別的網站集合使用方式報告，檢視和分析個別新式 SharePoint 網站的搜尋使用量報告。 如需詳細資訊，請 [參閱檢視新式網站中的搜尋使用量報告](/sharepoint/view-search-usage-reports-modern-sites)。

## <a name="recent-search-activity-report"></a>最近的搜尋活動報告

在 Microsoft 搜尋使用量報表中，您可以透過 [ **最近的搜尋活動** ] 圖表，檢視人員如何在組織中使用搜尋的快速摘要。 

:::image type="content" source="media/usage-reports/recent-search-activity.png" alt-text="顯示最近搜尋活動資料的圖表。" lightbox="media/usage-reports/recent-search-activity.png"::: 

圖表上方的資料會顯示下列計量在所選時段內的變更： 

| 計量 | 描述 |
|:-----|:-----|
|查詢總數 |已執行的搜尋查詢總數。  |
|每日作用中使用者 |已執行查詢的唯一使用者總數。  |
|平均結果位置 |代表搜尋結果清單中按一下專案的平均位置，其中數位一代表最上層位置 (值越低越好) 。|
|點選速率 |使用者按一下一或多個答案或搜尋結果的查詢百分比， (值越高，) 越好。 |

[最近的搜尋活動] 圖表會顯示查詢計數和點擊查詢速率一段時間的趨勢活動。 例如，如果選取 7 天篩選準則，這會比較目前的 7 天期間資料與先前的 7 天期間資料。 在向下趨勢的情況下，箭號和線條會以紅色顯示。 如果是向上趨勢，則會以綠色顯示。 趨勢資料不適用於 12 個月檢視。 

## <a name="filters"></a>篩選
在 [最近的搜尋活動] 圖表頂端，您可以使用下列計量來篩選資料。 請注意，這些篩選不僅適用于 [最近的搜尋活動] 圖表，也會套用至 [Microsoft 搜尋使用量報告] 頁面上的其他報表。 

| 篩選器 | 描述 |
|:-----|:-----|
|日期範圍 |頁面上顯示的分析日期範圍：過去 7 天、過去 14 天、過去 31 天和過去 12 個月。  |
|搜尋應用程式 |使用者執行查詢的搜尋應用程式：SharePoint 起始頁面、Office、Bing，或這三個搜尋應用程式。  |

### <a name="accessing-search-data-prior-to-the-start-of-new-generation-reports"></a>在新一代報告開始之前存取搜尋資料 

針對不同的租使用者，處理新的搜尋使用量報告會有所不同。 如果您在開始處理日期之前選取日期範圍，您會看到一則訊息，指出 **已選取整個期間的資料無法使用**。 若要在此日期之前檢視資料，您必須使用先前的使用方式分析報告。 

:::image type="content" source="media/usage-reports/data-not-available.png" alt-text="資料無法使用訊息。" lightbox="media/usage-reports/data-not-available.png":::

若要檢視先前的搜尋分析報告，請選取頁面右上角的 [ **新增使用量報告** ] 切換開關。 

:::image type="content" source="media/usage-reports/new-usage-toggle.png" alt-text="切換按鈕。" lightbox="media/usage-reports/new-usage-toggle.png":::

## <a name="you-can-download-reports"></a>您可以下載報表
Microsoft 搜尋使用量報表頁面中的每個報表和資料表都有一個下載選項，可讓您下載您在螢幕上以 Excel 格式看到之報表的背景資料。 當您在顯示的報表中限制為前五到十個數據列時，下載的報表最多會有 2000 筆前置記錄。  

下載報表可讓您從更廣泛的時間查看報表。 報表會根據選取的日期篩選器下載為 Excel 試算表。 如果您選擇過去 7 天、14 天或 31 天，試算表每天會有個別索引標籤。 過去 12 個月的下載每個月都會有一個索引標籤

## <a name="prevent-filtering-by-country-occupation-department-or-division"></a>防止依國家/地區、國家/地區、部門或部門進行篩選
根據預設，具有全域管理員、搜尋系統管理員和搜尋編輯器角色的使用者可以依國家/地區、職業或部門/部門篩選搜尋資料。 如果您不想讓系統管理員使用這些維度來篩選報表資料，您可以移至Microsoft 365 系統管理中心中的組織設定並設定此設定。  取消核取此設定時，系統管理員將無法依這些篩選篩選 **查詢詳細資料** 或 **連線分析詳細** 資料包告。  

只有全域管理員可以設定此設定。

若要設定此設定：
1. 在 [Microsoft 365 系統管理中心中，選取 [**設定]**，然後選取 [**組織設定]**。 
2. 在 [組織設定] 頁面上，選 **取 [搜尋&智慧使用方式分析]**。 
3. 在 [搜尋&智慧使用方式分析] 頁面上，取消核取 [ **允許依國家/地區、事業、部門或部門篩選使用量報告]**。
4. 選取 [儲存 **]**。 

## <a name="related-articles"></a>相關文章

[Microsoft 搜尋使用量報告 - 查詢](queries-usage-reports.md)</br>
[Microsoft 搜尋使用量報告 - 使用者](users-search-reports.md)</br>
[Microsoft 搜尋使用量報告 - 連線分析](connection-analytics-reports.md)</br>
[檢視新式網站中的搜尋使用量報告](/sharepoint/view-search-usage-reports-modern-sites)



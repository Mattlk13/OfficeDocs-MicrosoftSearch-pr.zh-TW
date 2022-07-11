---
title: Microsoft 搜尋使用量報告 – 連線分析
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
description: 檢閱 Microsoft Search 使用方式連線分析報告。
ms.openlocfilehash: 137eeba8ecf951f1b828273592f3944cff05d538
ms.sourcegitcommit: 2d32579d3f10e38acdcc185fa891b0a43a750489
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2022
ms.locfileid: "66713666"
---
# <a name="microsoft-search-usage-report--connection-analytics"></a>Microsoft 搜尋使用量報告 – 連線分析

在 [Microsoft 搜尋使用量報表](usage-reports.md)中， **[連線分析** ] 區段可讓您使用連線的搜尋結果來分析查詢。   

:::image type="content" source="media/usage-reports/connection-analytics.png" alt-text="顯示連線分析之搜尋使用量圖表和資料表的報表儀表板。" lightbox="media/usage-reports/connection-analytics.png":::

圖表上方的資料會顯示下列計量在所選時段內的變更： 

| 計量 | 描述 |
|:-----|:-----|
|具有連線結果的查詢|包含一或多個連接結果的查詢數目。|
|點選查詢  |使用者按一下一或多個連線結果的查詢數目。|
|已編制索引的專案總數|所有連接的索引項目目總數。|
|作用中連線|目前作用中的連接數目。|

[ **查詢和隨時間點** 選] 圖表會顯示所選時段的趨勢，其中顯示具有連線結果的查詢數目，以及使用者按一下一或多個連線結果的查詢數目。

您可以按一下 **[下載報表** ] 連結，將報表下載為 Excel 檔案，並查看更多詳細資料。  

您可以選取 [使用 **情況分析** ] 主頁面之 [連線分析] 區段底部的 [檢 **視詳細** 資料] 按鈕，以檢視 [連線分析詳細資料] 頁面。  

## <a name="connection-analytics-details-page"></a>連線分析詳細資料頁面
[連線分析詳細資料] 頁面可讓您使用連線的搜尋結果來分析查詢。   

:::image type="content" source="media/usage-reports/connection-analytics-details.png" alt-text="顯示連線分析詳細資料包表之搜尋使用量圖表和資料表的報表儀表板。" lightbox="media/usage-reports/connection-analytics-details.png":::

在 [ **篩選] 功能表中** ，使用下列一或多個專案來篩選報表中的資料： 

| 篩選器 | 描述 |
|:-----|:-----|
|日期範圍 |頁面上顯示的分析日期範圍。 可用的選項為 7 天、14 天、31 天和過去 12 個月。|
|搜尋應用程式  |用來執行查詢的搜尋應用程式。 可用的選項包括 SharePoint 起始頁、Office.com、Bing.com (工作索引標籤) ，或全部三個應用程式合併。  |
|國家/地區  |使用者在 Azure Active Directory 中根據其 **國家** /地區屬性執行查詢的國家/地區。 |
|職業    |使用者根據其在 Azure Active Directory 中的 **title** 屬性執行查詢的佔用。  |
|部門或部門    |執行查詢之使用者的部門或部門，根據在 Azure Active Directory 中執行搜尋之使用者管理鏈結中第二個最上層使用者的 **部門** 屬性。 |

[連線分析詳細資料] 頁面包含下列三份報告： 
- 依連線的查詢和點選 
- 依連線編制索引的專案總數
- 連線 

### <a name="queries-and-click-throughs-by-connection"></a>依連線的查詢和點選
此報表會比較具有連線結果的查詢數目，以及最多六個最常使用之資料連線的按一下次數。

:::image type="content" source="media/usage-reports/queries-clicks-by-connection.png" alt-text="橫條圖圖表，顯示查詢，並依連線類型按一下資料。" lightbox="media/usage-reports/queries-clicks-by-connection.png":::

### <a name="total-indexed-items-by-connection"></a>依連線編制索引的專案總數
此報表顯示每個資料連線所使用之索引項目總數的比較。  

:::image type="content" source="media/usage-reports/index-by-connection.png" alt-text="橫條圖圖形，顯示依資料連線編制索引的專案。" lightbox="media/usage-reports/index-by-connection.png":::

### <a name="connections"></a>連線 
此報表顯示連線類型 (詳細資料、具有連線結果的查詢、按一下已建立之所有連線的查詢和索引項目目) 。 它會使用連線的搜尋結果來分析查詢，這有助於識別哪些連線對組織有價值。 這些重要計量對於採用圖形連接器、識別微調的潛在區域，以及合理化投資和連線配額很有用。 

:::image type="content" source="media/usage-reports/connections.png" alt-text="顯示連線詳細資料的資料表。" lightbox="media/usage-reports/connections.png":::

## <a name="download-reports"></a>下載報告
每個報表和資料表都有一個下載選項，可讓您下載您在螢幕上以 Excel 格式看到之報表的背景資料。 當顯示的報表限制為前五到十個數據列時，下載的報表最多會有 2000 筆前置記錄。   

下載報表可讓您從更廣泛的時間查看報表。 報表會根據選取的日期篩選器下載為 Excel 試算表。 如果您選擇過去 7 天、14 天或 31 天，試算表每天會有個別索引標籤。 過去 12 個月的下載每個月都會有一個索引標籤。

## <a name="prevent-filtering-by-country-occupation-department-or-division"></a>防止依國家/地區、國家/地區、部門或部門進行篩選 
根據預設，具有全域管理員、搜尋系統管理員和搜尋編輯器角色的使用者可以依國家/地區、職業或部門/部門篩選搜尋資料。 如果您不想讓系統管理員使用這些維度來篩選報表資料，您可以移至Microsoft 365 系統管理中心中的組織設定，並設定此設定。  取消核取此設定時，系統管理員將無法篩選這些篩選準則的連線 **分析詳細** 資料包告。  

只有全域管理員可以設定此設定。 

若要設定此設定： 
1. 在 [Microsoft 365 系統管理中心中，選取 [**設定]**，然後選取 [**組織設定]**。
2. 在 [組織設定] 頁面上，選 **取 [搜尋&智慧使用方式分析]**。 
3. 在 [搜尋&智慧使用方式分析] 頁面上，取消核取 [ **允許依國家/地區、事業、部門或部門篩選使用量報告]**。
4. 選取 **[儲存]**。 

## <a name="related-topics"></a>相關主題
[Microsoft 搜尋使用量報告](usage-reports.md)</br>
[Microsoft 搜尋使用量報告 - 查詢](queries-usage-reports.md)</br>
[Microsoft 搜尋使用量報告 - 使用者](users-search-reports.md)</br>
[檢視新式網站中的搜尋使用量報告](/sharepoint/view-search-usage-reports-modern-sites.md)




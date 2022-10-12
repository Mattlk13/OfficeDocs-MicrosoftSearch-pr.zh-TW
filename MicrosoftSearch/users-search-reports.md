---
title: Microsoft 搜尋使用量報告 – 使用者
ms.author: efrene
author: efrene
manager: scotv
ms.topic: article
ms.service: mssearch
audience: Admin
ms.audience: Admin
ms.date: ''
ms.localizationpriority: medium
ms.collection:
- scotvorg
search.appverid:
- BFB160
- MET150
- MOE150
description: 檢閱 Microsoft 搜尋使用者使用量報告
ms.openlocfilehash: 8d7cfada2c7146062169ea5a69aff75ed7e29da1
ms.sourcegitcommit: 6ae319b4da98b45ac2c7cbce15bc1fdc9d799cea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2022
ms.locfileid: "68523677"
---
# <a name="microsoft-search-usage-report--users"></a>Microsoft 搜尋使用量報告 – 使用者

在 [[Microsoft 搜尋使用量報告](usage-reports.md)] 區段中，[使用者] 區段會顯示已執行搜尋搜尋應用程式的使用中和參與使用者總數，以及頁面頂端的篩選準則所選取的日期範圍。  

- **參與的使用者** – 在一個月內至少搜尋了五天的使用者。 只有在選取 12 個月的日期範圍時，才會顯示這些值。
- **作用中使用者** – 每個月至少搜尋一天的使用者。

:::image type="content" source="media/usage-reports/users-reports.png" alt-text="顯示橫條圖和圖表的儀表板頁面。" lightbox="media/usage-reports/users-reports.png":::

下列報表提供使用者的搜尋資料： 

- **依應用程式的使用者參與** – 此橫條圖顯示搜尋應用程式 (Office.com、SharePoint 起始頁或 Bing.com) 的使用中和參與使用者總數。只有在篩選中選取 12 個月檢視時，才會顯示此圖表。
- **一段時間的作用中使用者** – 此圖表顯示在指定期間內使用搜尋應用程式搜尋的作用中使用者數目。  

您可以按一下 **[下載報表** ] 連結，將報表下載為 Excel 檔案，並查看更多詳細資料。 

## <a name="user-details"></a>使用者詳細資料

[使用者詳細資料] 頁面會顯示組織中有多少人是作用中或參與的搜尋使用者，以您選取的篩選來測量。  這些篩選條件包括: 

| 篩選器 | 描述 |
|:-----|:-----|
|日期範圍 |頁面上顯示的分析日期範圍。 可用的選項為 7 天、14 天、31 天和過去 12 個月。|
|搜尋應用程式  |用來執行查詢的搜尋應用程式。  可用的選項包括 SharePoint 起始頁、Office.com、Bing.com (工作索引標籤) ，或全部三個應用程式合併。  |
|國家/地區  |使用者在 Azure Active Directory 中根據其 **國家** /地區屬性執行查詢的國家/地區。 |
|職業    |使用者根據其在 Azure Active Directory 中的 **title** 屬性執行查詢的佔用。  |
|部門或部門    |執行查詢之使用者的部門或部門，根據在 Azure Active Directory 中執行搜尋之使用者管理鏈結中第二個最上層使用者的 **部門** 屬性。 |

您可以選取 [使用方式分析] 主頁面 [使用者] 區段底部的 [ **檢視詳細** 資料] 按鈕，以檢視 [ **使用者** 詳細資料] 頁面。 

使用者詳細資料頁面包含下列兩個圖表：
- 作用中的使用者 
- 參與的使用者   

### <a name="active-users-chart"></a>作用中使用者圖表
[作用中使用者] 圖表會依搜尋應用程式顯示作用中使用者的總數。 

:::image type="content" source="media/usage-reports/active-users-chart.png" alt-text="依搜尋應用程式顯示作用中使用者的圖表。" lightbox="media/usage-reports/active-users-chart.png":::

### <a name="engaged-users-chart"></a>參與的使用者圖表
[參與的使用者] 圖表會依搜尋應用程式顯示參與的使用者總數。 此圖表只會針對 12 個月檢視顯示，因為 **參與的使用者** 計量僅供每月使用。

:::image type="content" source="media/usage-reports/engaged-users-chart.png" alt-text="圖表，顯示依搜尋應用程式參與的使用者。" lightbox="media/usage-reports/engaged-users-chart.png":::

## <a name="download-reports"></a>下載報告
每個報表和資料表都有一個下載選項，可讓您下載您在螢幕上以 Excel 格式看到之報表的背景資料。 當顯示的報表限制為前五到十個數據列時，下載的報表最多會有 2000 筆前置記錄。   

下載報表可讓您從更廣泛的時間查看報表。 報表會根據選取的日期篩選器下載為 Excel 試算表。 如果您選擇過去 7 天、14 天或 31 天，試算表每天會有個別索引標籤。 過去 12 個月的下載每個月都會有一個索引標籤。

## <a name="related-topics"></a>相關主題

[Microsoft 搜尋使用量報告](usage-reports.md)</br>
[Microsoft 搜尋使用量報告 - 查詢](queries-usage-reports.md)</br>
[Microsoft 搜尋使用量報告 - 連線分析](connection-analytics-reports.md)</br>
[檢視新式網站中的搜尋使用量報告](/sharepoint/view-search-usage-reports-modern-sites)
---
title: 'Microsoft 搜尋使用量報告 – 查詢 '
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
description: 檢閱 Microsoft Search 使用量 - 查詢報告
ms.openlocfilehash: 12f7f28b0df7b341c219a68e2e3cef56e44478b3
ms.sourcegitcommit: 6ae319b4da98b45ac2c7cbce15bc1fdc9d799cea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2022
ms.locfileid: "68523659"
---
# <a name="microsoft-search-usage-report--queries"></a>Microsoft 搜尋使用量報告 – 查詢

在 [Microsoft 搜尋使用量報](usage-reports.md)表中， **[查詢]** 區段會比較已按一下、放棄或未傳回任何結果的搜尋查詢數目。 它也會比較其他因素的查詢，例如職業、部門或部門。 圖表會顯示在頁面頂端選取的篩選準則。  

:::image type="content" source="media/usage-reports/queries-report.png" alt-text="儀表板頁面，其中包含四個帶有查詢報表資料的圓形圖。" lightbox="media/usage-reports/queries-report.png":::

查詢資料會以四個圓形圖提供： 

- **依使用者動作的查詢總數** – 比較沒有結果的查詢數目與使用者按一下結果或未執行任何動作的查詢數目， (放棄) 。  
- **依國家/地區的查詢總數** – 根據使用者的國家/ **地區 Azure** Active Directory 屬性，比較不同國家/地區的使用者搜尋查詢。 
- **依同盟的查詢總數** – 根據使用者在 Azure Active Directory 中的 **標題** 屬性，比較不同同盟中的使用者所進行的搜尋查詢數目。
- **依部門或部門的查詢總數** – 比較組織中不同部門或部門使用者的搜尋查詢數目。 這是以在 Azure Active Directory 中執行搜尋之使用者管理鏈結中第二個最上層使用者的 **部門** 屬性為基礎。 

每個圓形圖都會顯示前五個值，其餘的值則會摘要在 [ **其他** ] 類別中。 您可以按一下 **[下載報表** ] 連結，將報表下載為 Excel 檔案，並查看更多詳細資料。 

## <a name="filters"></a>篩選

使用 [**流量分析**] 頁面頂端的 [**篩選**] 功能表，依下列方式篩選您的查詢資料總計： 

| 篩選器 | 描述 |
|:-----|:-----|
|日期範圍 |頁面上顯示的分析日期範圍：過去 7 天、過去 14 天、過去 31 天和過去 12 個月。  |
|搜尋應用程式 |使用者執行查詢的搜尋應用程式：SharePoint 起始頁面、Office、Bing，或這三個搜尋應用程式。  |
 
## <a name="query-details-page"></a>查詢詳細資料頁面

[查詢詳細資料] 頁面會顯示組織中經常使用搜尋的人員所進行的搜尋查詢，以及未傳回任何結果或使用者未選取任何搜尋結果的查詢。   

您可以選取主要使用方式分析頁面 [查詢] 區段底部的 [檢 **視詳細** 資料] 按鈕，以檢視 [ **查詢** 詳細資料] 頁面。 

:::image type="content" source="media/usage-reports/query-details.png" alt-text="顯示三個圖表的儀表板頁面。" lightbox="media/usage-reports/query-details.png":::

您可以在查詢詳細資料頁面上取得的三份報告包括： 

- 最受歡迎的搜尋字詞 
- 前 10 個無結果查詢
- 最常放棄的搜尋字詞 

在 [ **篩選] 功能表中** ，使用下列一或多個專案來篩選報表中的資料： 

| 篩選器 | 描述 |
|:-----|:-----|
|日期範圍 |頁面上顯示的分析日期範圍。 可用的選項為 7 天、14 天、31 天和過去 12 個月。|
|搜尋應用程式  |用來執行查詢的搜尋應用程式。  可用的選項包括 SharePoint 起始頁、Office.com、Bing.com (工作索引標籤) ，或全部三個應用程式合併。  |
|按下最上層結果 |連結至此查詢所選取的前三個結果。</br> **注意** 連結不適用於書簽和其他回應功能。|
|國家/地區  |使用者在 Azure Active Directory 中根據其 **國家** /地區屬性執行查詢的國家/地區。 |
|職業    |使用者根據其在 Azure Active Directory (AAD) 中的 **title** 屬性執行查詢的佔用。  |
|部門或部門    |執行查詢之使用者的部門或部門，根據在 Azure Active Directory 中執行搜尋之使用者管理鏈結中第二個最上層使用者的 **部門** 屬性， (AAD) 。 |


### <a name="most-popular-search-terms"></a>最受歡迎的搜尋字詞 
此報表顯示前 10 個最受歡迎的搜尋查詢。 它會顯示最上層查詢，以及每個查詢的前三個點選結果。 使用此報告來瞭解使用者正在搜尋的資訊類型，以及前三個結果的效能。 

每個最上層搜尋專案都會提供下列資料。 

| 欄 | 描述 |
|:-----|:-----|
|查詢總數  |執行此查詢的總次數。 |
|按下最上層結果 |某人選取此查詢所傳回搜尋結果的次數百分比。|
|按下最上層結果  |連結至此查詢所選取的前三個結果。</br>**注意**：連結不適用於書簽和其他回應功能。  |
|結果類型  |前三個結果的實體類型 (例如檔案、書簽或外部) 。  |
|結果點選|某人按一下此搜尋結果的次數百分比，超出此查詢的點擊總數。  |
|結果的平均位置  |此搜尋結果在搜尋結果頁面上的平均相對位置。 |

### <a name="top-10-no-result-queries"></a>前 10 個無結果查詢
此報表顯示未傳回任何結果的熱門搜尋字詞。 使用此報告來識別可能會造成使用者不滿意的搜尋查詢，並改善內容的可探索性。 然後，您可以判斷建立答案，例如書簽，或透過 Graph 連接器內嵌新內容是否是正確的動作。  

> [!NOTE]
> 在某些情況下，搜尋字詞可以在無結果報表中表示，即使其具有書簽或列為其中一個最熱門的查詢也一樣。 其中一個範例是，如果查詢是在未顯示書簽的垂直 (例如「Sites」 垂直) 。

### <a name="top-abandoned-search-terms"></a>最常放棄的搜尋字詞 
此報表顯示接收低點擊率的熱門搜尋字詞。 使用此報告來識別可能會造成使用者不滿意的搜尋查詢，並改善內容的可探索性。 然後，您可以判斷建立答案，例如書簽，或透過 Graph 連接器內嵌新內容是否是正確的動作。  

## <a name="prevent-filtering-by-country-occupation-department-or-division"></a>防止依國家/地區、國家/地區、部門或部門進行篩選 

根據預設，具有全域管理員、搜尋系統管理員和搜尋編輯器角色的使用者可以依國家/地區、職業或部門/部門篩選搜尋資料。 如果您不想讓系統管理員使用這些維度來篩選報表資料，您可以移至Microsoft 365 系統管理中心中的組織設定，並設定此設定。  取消核取此設定時，系統管理員將無法依這些篩選篩選 **查詢詳細** 資料包告。  

只有全域管理員可以設定此設定。 

若要設定此設定： 
1. 在 [Microsoft 365 系統管理中心中，選取 [**設定]**，然後選取 [**組織設定]**。
2. 在 [組織設定] 頁面上，選 **取 [搜尋&智慧使用方式分析]**。 
3. 在 [搜尋&智慧使用方式分析] 頁面上，取消核取 [ **允許依國家/地區、事業、部門或部門篩選使用量報告]**。
4. 選取 [儲存]。 

## <a name="download-reports"></a>下載報告
每個報表和資料表都有一個下載選項，可讓您下載您在螢幕上以 Excel 格式看到之報表的背景資料。 當顯示的報表限制為前五到十個數據列時，下載的報表最多會有 2000 筆前置記錄。   

下載報表可讓您從更廣泛的時間查看報表。 報表會根據選取的日期篩選器下載為 Excel 試算表。 如果您選擇過去 7 天、14 天或 31 天，試算表每天會有個別索引標籤。 過去 12 個月的下載每個月都會有一個索引標籤。 

###  <a name="special-note-for-the-most-popular-search-items-download-report"></a>熱門搜尋專案下載報表的特殊注意事項 

在 **最受歡迎的搜尋專案** 報告中，請注意，在報表的使用者介面中，查詢最多可以有三個熱門搜尋字詞的前三個結果。 當您下載報表並在 Excel 中檢視報表時，具有一個以上結果的搜尋字詞會顯示每個結果的資料列。 前三個數據行會與查詢 (相關，例如， (查詢文字、計數和按一下) ，而且會相同。 搜尋專案之資料列中的其餘資料行會與特定結果相關，而且會有所不同。

:::image type="content" source="media/usage-reports/excel-report.png" alt-text="顯示多個資料列的 Top 查詢報表 Excel 試算表。" lightbox="media/usage-reports/excel-report.png":::

以下是可下載報表中的資料行概觀。 **[套用至] 資料** 行會指定資料行值是否與 **查詢** 或 **結果** 有關。

| 欄 | 適用於 | 描述 |
|:-----|:--------|:-----|
|查詢文字 |查詢  |最常執行的搜尋字詞。 |
|計數 |查詢 |此搜尋字詞的查詢總數。 |
|點擊 |查詢 |此搜尋字詞按一下一或多次的查詢總數。 | 
|URL |結果 |前三個搜尋結果的 URL。 請注意，URL 不適用於書簽、外部內容和其他回應功能。   |
|顯示名稱|結果 |目前為空白。 未來會使用它來顯示回應專案的檔案名和標題。  |
|類型 |結果 | 結果類型，例如檔案、書簽或縮寫。|
|閱聽 |結果 |此查詢顯示此特定結果的次數。  |
|點選 |結果 | 針對此查詢按一下結果的次數。 |
|結果的平均位置 |結果  |此查詢的結果所顯示的平均位置。  |

## <a name="related-topics"></a>相關主題

[Microsoft 搜尋使用量報告](usage-reports.md)</br>
[Microsoft 搜尋使用量報告 - 使用者](users-search-reports.md)</br>
[Microsoft 搜尋使用量報告 - 連線分析](connection-analytics-reports.md)</br>
[檢視新式網站中的搜尋使用量報告](/sharepoint/view-search-usage-reports-modern-sites)
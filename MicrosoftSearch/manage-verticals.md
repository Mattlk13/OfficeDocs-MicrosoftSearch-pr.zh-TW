---
title: 管理垂直搜尋
ms.author: jypal
author: jypal6
manager: jeffkizn
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
ms.date: 03/15/2022
search.appverid:
- BFB160
- MET150
- MOE150
description: 管理結果頁面上的搜尋垂直
ms.openlocfilehash: 5bb2871b081097bff78392c71fbac6343f8aa494
ms.sourcegitcommit: d7837641df3c0459e62ea7a4c518c64486589706
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/20/2022
ms.locfileid: "66168830"
---
# <a name="manage-search-verticals"></a>管理垂直搜尋

搜尋垂直是搜尋結果頁面上的索引標籤，會顯示特定類型或選取來源的結果。 例如，[檔案] 垂直會顯示分類為檔案的結果，讓想要尋找檔的使用者更容易找到。 您可以在Microsoft 搜尋中自訂垂直，以符合組織或個別部門的需求。 Microsoft 搜尋有兩種類型的垂直，即預設或自訂垂直。 預設垂直，例如 All、Files 和 People，可讓您輕鬆存取最常使用的搜尋結果。

您可以在兩個層級管理垂直：

- **組織層級**– 當使用者 [從其SharePoint](https://sharepoint.com/)開始 [頁面、Microsoft Office](https://office.com)和Microsoft 搜尋中搜尋時，搜尋結果頁面上會出現垂直 [Bing](https://bing.com)
- **網站層級**– 當使用者在SharePoint網站上搜尋時，搜尋結果頁面上會出現一個垂直的網站層級。 例如，您可能想要讓客戶服務員工直接從其部門的SharePoint網站搜尋嚴重性 1 事件。

## <a name="default-verticals"></a>預設垂直

預設垂直會出現在組織層級的體驗中[，例如Bing中的SharePoint](https://sharepoint.com/)、[Microsoft Office](https://office.com/)和[Microsoft 搜尋](https://bing.com/)，或在每個網站的搜尋結果頁面中的SharePoint網站層級。 

以下是現成垂直的自訂功能摘要。

|自訂類型   |組織層級     |網站層級   |
|---------|---------|---------|
| 重新命名垂直    | 是 |是  |
| 停用垂直   | 部分       |是  |
| 新增查詢      | 部分       |是  |

## <a name="custom-verticals"></a>自訂垂直
您可以新增與組織相關的搜尋垂直。 例如，您可以根據每個部門所需的資訊類型，為行銷相關內容建立垂直的 ，並為銷售建立另一個。 您可以新增垂直，以顯示由Graph連接器或從SharePoint編制索引之內容的結果。

## <a name="create-or-modify-search-verticals"></a>建立或修改垂直搜尋

垂直管理體驗是以精靈為導向，系統會引導您逐步定義要搜尋之內容的垂直名稱、內容來源和範圍。 您可以使用一組有限的[關鍵字查詢語言 (KQL) ](#keyword-query-language-kql)來定義指定內容來源的垂直搜尋範圍。 篩選器也可以新增至組織和網站層級的現成可用和自訂垂直。 如需篩選的詳細資訊，請 [參閱管理篩選](/microsoftsearch/custom-filters)。

### <a name="manage-organization-level-verticals"></a>管理組織層級垂直

1. 在 [Microsoft 365 系統管理中心](https://admin.microsoft.com)中，移至 [**自訂**] 區段中的 [[**垂直**](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/verticals)] 頁面。
1. 選取現有的垂直，然後按一下 **[編輯]** 或按一下 [ **新增** ] 以建立新的垂直。
1. 完成設定步驟之後，您可以檢閱並儲存垂直。  

### <a name="manage-site-level-verticals"></a>管理月臺層級垂直

1. 在您要管理垂直的SharePoint網站中，按一下齒輪來開啟設定面板。
1. 選 **取 [網站資訊]**，然後選 **取 [檢視所有網站設定]**。  
1. 尋找 [Microsoft 搜尋] 區段，然後選取 [設定 **搜尋設定]**。
1. 在流覽窗格中，移至 [自訂體驗]，然後選取 [ **垂直]**。
1. 選取現有的垂直，然後按一下 **[編輯]** 或按一下 [ **新增** ] 以建立新的垂直。
1. 設定設定之後，您可以檢閱並儲存垂直。  

## <a name="view-the-vertical-in-the-search-result-page"></a>在搜尋結果頁面中檢視垂直

需要[搜尋結果配置](manage-result-types.md)，Graph連接器結果才能在搜尋垂直頁面上呈現。 在確保有適當的結果配置時，您可以啟用垂直搜尋。 在您啟用或更新垂直之後，會有幾個小時的延遲，您才能在搜尋頁面上檢視變更。 您可以將 cacheClear=true 附加至 SharePoint 中的 URL，並Office立即檢視變更。 在Bing中，將 &features=uncachedVerticals 附加至工作垂直 URL，以立即檢視變更。

> [!NOTE]
> 從行動網頁瀏覽器檢視時[，SharePoint](https://sharepoint.com/)和[Office](https://office.com)上看不到新增的垂直。

## <a name="advanced-configuration-options"></a>進階組態選項

### <a name="multiple-connections-in-a-vertical"></a>垂直的多個連接

垂直搜尋可以呈現來自多個連接器來源的結果。 此選項可讓您彈性地設計搜尋結果頁面。 垂直安裝程式可讓系統管理員在「內容來源」步驟中選取多個連線。

如果您正確地盡可能地獲得任意數量 *的語意標籤* ，則會增強此體驗。 您會在架構定義和擷取時新增語意標籤。 [深入瞭解如何建立和管理語意標籤](configure-connector.md#step-6-assign-property-labels)。
[以下是](configure-connector.md#step-6-assign-property-labels) 有關如何建立和管理語意標籤的其他資訊。

> [!NOTE]
> - 垂直功能中的多個連線目前為預覽狀態。 如需詳細資訊，請 [參閱連接器預覽功能](connectors-overview.md#what-are-the-preview-features)。
> - 連接可以新增為單一垂直下的內容來源。 您無法在多個垂直下使用連線。

若要針對已新增多個連接來源的搜尋垂直設定查詢，請使用通用來源屬性來建立查詢。

### <a name="keyword-query-language-kql"></a>關鍵字查詢語言 (KQL) 

您可以將查詢新增至垂直，以使用 [關鍵字查詢語言](/sharepoint/dev/general-development/keyword-query-language-kql-syntax-reference) (KQL)  (有限支援) ，縮小搜尋垂直上顯示的結果範圍。 此頁面會列出可用的屬性。 建議您搭配布林運算子使用 free-text 關鍵字和屬性限制來建立KQL。 不支援 XRANK、鄰近運算子和單字等動態排名運算子。

以下是一些範例查詢。

|案例         | 查詢   |  
| --------- | ------ |
|從封存網站排除結果           |NOT (路徑：HTTP//contoso.sharepoint.com/archive OR path：HTTP//contoso.sharepoint.com/CompanyArchive) |
| 根據檔案類型屬性排除結果 | NOT (FileType：htm) |  

在垂直的 [KQL 查詢] 區段中使用變數，以提供動態資料作為垂直查詢的輸入。 「設定檔」和「查詢字串」是可用的查詢變數類型。

#### <a name="profile-query-variables"></a>設定檔查詢變數

您可以使用設定檔查詢變數，將搜尋結果內容化為已登入的使用者。 設定檔查詢變數會從登入使用者的 [設定檔](/graph/api/resources/profile)擷取值。 例如，若要為使用者建立「票證」垂直，以尋找指派給他們的支援票證，您可以在系統管理頁面的垂直建立期間，于 [查詢] 區段中指定下列查詢。

`AssignedTo:{Profile.accounts.userPrincipalName}`

這會修剪搜尋結果，只顯示指派給進行搜尋之人員的專案。

[設定檔資源](/graph/api/resources/profile) 會將屬性公開為集合。 例如，電子郵件地址的相關資訊是透過電子郵件收集、工作位置做為位置集合來公開，依此類推。 使用者設定檔中所有可用的屬性都會公開為查詢變數。

請考慮電子郵件集合中有三個可用電子郵件地址的使用者，如下所示：

```json
"emails": [{ 

        "address": "Megan.Bowen@contoso.com",
        "id": "xyz", 
        "source": { 
            "CreatedBy": "xyz", 
            "CreatedOn": "2222", 
            "Type": "official" 
        },
        "type": "main" 
    }, { 
        "address": "meganb@hotmail.com",
        "id": "abc", 
        "source": { 
            "CreatedBy": "abc",
            "CreatedOn": "3333", 
            "Type": "non-official",
        },
        "type": "work"
    }, { 
        "address": "meganb@outlook.com",
        "id": "pqr", 
        "source": { 
            "CreatedBy": "pqr", 
            "CreatedOn": "4444", 
            "Type": "personal" 
        },
        "type": "personal" 
    } 
] 
```

- 查詢 `MyProperty: {Profile.emails.address}` 會解析為 *MyProperty：「Megan.Bowen@contoso.com」*。  

- 若要解析 address 屬性的所有值，請使用多重值擴充語法。 查詢 `{|MyProperty:{Profile.emails.address}}` 會解析為 *( (MyProperty：「Megan.Bowen@contoso \. com」)* OR *(MyProperty： 「meganb@hotmail \. com」)* OR  *(MyProperty：「meganb@outlook \. com」) )*。

使用 「|」 運算子來解析多重值變數。 如需設定檔擴充的更多範例，請參閱下表。

| #         | 語法 |  傳回值  |
| --------- | ------ | --- |
| 1    | MyProperty：{Profile.emails.address}  |   「Megan \. Bowen@contoso.com」  |
| 2 | MyProperty：{Profile.emails}   |    {Profile.emails} 因為 *電子郵件* 是物件，所以無法解決此問題。|
| 3    | {?MyProperty：{Profile.emails}}  |  因為 *電子郵件* 是物件，所以無法解決此問題。 「？」 運算子會忽略未解析的查詢變數。 當進一步向下傳遞查詢堆疊時，將會移除此變數。   |
| 4  | {&#124;MyProperty： {Profile.emails.source.Type}}    |   ( (MyProperty：「official」) OR (MyProperty：「non-official」) OR (MyProperty：「personal」) )     |

#### <a name="query-string-variables"></a>查詢字串變數

查詢字串變數可讓您根據使用者與SharePoint網站互動的方式，將搜尋結果個人化。 這是藉由將索引鍵/值組新增至搜尋 URL 來完成。 例如，假設您有一個SharePoint網站，其中提供專案的相關資訊，其中包含顯示進行中工作的簡單網頁元件。 按一下 [進行中] 網頁元件，將使用者連結至 「工作專案」搜尋垂直，其中的結果會進行精簡，只顯示標記為 **InProgress** 的專案。

這可以藉由在系統管理頁面的垂直建立期間，于 [查詢] 區段中指定下列查詢來完成。

`Status:{QueryString.state}`

SharePoint網站按鈕網頁元件上的 URL 必須更新，才能將下列機碼值組傳遞 HTTPs://{your-domain}.sharepoint.com/sites/{site-name}/_layouts/15/search.aspx/{vertical-ID}？state=InProgress

查詢狀態：{QueryString.state} 會解析為 status：InProgress。

以下是更多查詢字串擴充的範例。

| #         | 查詢語法 | URL 語法 | 傳回值 |
| --------- | --------- | --------- | --------- |
| 1    | MyProperty：{QueryString.state}  |   HTTPs://{your-domain}.sharepoint.com/sites/{site-name}/_layouts/15/search.aspx/{vertical-ID}？state=InProgress  |   MyProperty：InProgress  |
| 2 | MyProperty：{QueryString.state} 或 MyProperty：{QueryString.priority}   |    HTTPs://{your-domain}.sharepoint.com/sites/{site-name}/_layouts/15/search.aspx/{vertical-ID}？state=InProgress&priority=1 |   MyProperty：InProgress 或 MyProperty：1  |
| 3    | {?MyProperty：{QueryString.state}}  |  HTTPs://{your-domain}.sharepoint.com/sites/{site-name}/_layouts/15/search.aspx/{vertical-ID}？State=InProgress   |   此處的狀態將無法解決，因為 QueryStrings 會區分大小寫。  「？」 運算子會忽略未解析的查詢變數。 當進一步向下傳遞查詢堆疊時，將會移除此變數。  |
| 4  | { \| MyProperty： {QueryString.state}}    |  HTTPs://{your-domain}.sharepoint.com/sites/{site-name}/_layouts/15/search.aspx/{vertical-ID}？state=InProgress，Closed    |    (MyProperty：InProgress) OR (MyProperty：Closed)   <br /> 運 \| 算符是用來解析 muti-value 變數。 變數的值應該使用逗號分隔符號傳遞，如 URL 語法所示。 |
| 5 | {MyProperty： {QueryString.state}}    |  HTTPs://{your-domain}.sharepoint.com/sites/{site-name}/_layouts/15/search.aspx/{vertical-ID}？state=InProgress，Closed   |   MyProperty：InProgress <br /> 這裡只會從 URL 挑選狀態的第一個值，因為查詢語法不會將它定義為多重值變數。 |


## <a name="limitations"></a>限制
- 語言當地語系化不適用於修改後的現成垂直名稱。 
- 自訂垂直不會出現在Microsoft 搜尋的行動檢視上。 
- 人員垂直不支援新增查詢。 
- 組織中的來賓使用者看不到垂直修改和新的垂直。 
- 不支援垂直重新排序。
- Bing中的Microsoft 搜尋不支援 [全部] 索引標籤的垂直重新命名。
- 查詢字串變數只能用於SharePoint網站。

## <a name="troubleshooting"></a>疑難排解

以下是您可能會遇到的常見問題清單，以及修正這些問題的動作。

|問題  |動作  |
|---------|---------|
| 我在垂直上看到「發生錯誤」錯誤訊息。 | 完成設定時需要垂直和結果類型。 請確定兩者都已針對內容來源進行設定。 |
| 我在垂直頁面上看不到任何內容來源。 | 請確定您已設定連接器和索引資料。   |



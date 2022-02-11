---
title: 管理搜尋行業
ms.author: jypal
author: jypal6
manager: jeffkizn
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
ms.date: 10/27/2021
search.appverid:
- BFB160
- MET150
- MOE150
description: 在 [結果] 頁面上管理搜尋縱向
ms.openlocfilehash: 6385b9f09356e7b4baedfc6ed968f1198696b42e
ms.sourcegitcommit: acc24e01c99242fef7401de079bd6060cb1ba301
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2022
ms.locfileid: "62540327"
---
# <a name="manage-search-verticals"></a>管理搜尋行業

搜尋縱向是搜尋結果頁面上的索引標籤，顯示特定類型的結果或從 [選取來源]。 例如，檔會顯示分類為檔案的結果，並可讓尋找檔的使用者輕鬆。 您可以在 Microsoft 搜尋中自訂各行業，以符合組織或個別部門的需求。 Microsoft 搜尋有兩種類型的縱向，現成或預設和自訂的縱向。 預設的縱向（如「所有」、「檔案」及「人員」）可輕鬆存取最常用的搜尋結果。

您可以在兩個層次管理縱向：

- **組織層級**-當使用者從 [SharePoint](https://sharepoint.com/)開始頁面、 [Microsoft Office](https://office.com)及 Microsoft 搜尋搜尋時，會顯示在 [搜尋結果] 頁面上的垂直位置 [Bing](https://bing.com)
- **網站層級**-當使用者在 SharePoint 網站上搜尋時，會在 [搜尋結果] 頁面上顯示該網站層級的垂直位置。 例如，您可能想要讓客戶服務員工直接從部門的 SharePoint 網站搜尋嚴重性1事件。

## <a name="default-verticals"></a>預設的縱向

在組織層級（如[Bing](https://bing.com/)或在每個網站搜尋結果頁面的 SharePoint 網站層級）中，會顯示預設的縱向[SharePoint](https://sharepoint.com/)、 [Microsoft Office](https://office.com/)和 Microsoft 搜尋。 

以下是盒中的縱向自訂功能摘要。

|自訂類型   |組織層級     |網站層級   |
|---------|---------|---------|
| 重新命名垂直    | 是 |是  |
| 停用垂直   | 部分       |是  |
| 新增查詢      | 部分       |是  |

## <a name="custom-verticals"></a>自訂的縱向
您可以新增與您組織相關的搜尋行業。 例如，您可以根據每個部門所需的資訊類型，為行銷相關的內容及另一個銷售人員建立垂直。 您可以新增縱向，以顯示由 Graph 連接器或從 SharePoint 編制索引的內容結果。

## <a name="create-or-modify-search-verticals"></a>建立或修改搜尋縱向

「垂直管理經驗」是由嚮導驅動，您可以逐步指導您定義要搜尋之內容的豎直名稱、內容來源及範圍。 您可以使用一組有限的 [關鍵字查詢語言 (KQL) ](#keyword-query-language-kql) 來定義指定內容來源的垂直搜尋範圍。 您也可以在組織和網站層級，將篩選新增至現成和自訂的行業。 如需篩選的詳細資訊，請參閱 [管理篩選器](/microsoftsearch/custom-filters)。

### <a name="manage-organization-level-verticals"></a>管理組織層級的縱向

1. 在 [Microsoft 365 系統管理中心](https://admin.microsoft.com)中，移至 [**自訂**] 區段中的 [[**縱向**](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/verticals)] 頁面。
1. 選取現有的垂直，然後按一下 [ **編輯** ]，或按一下 [ **新增** ] 以建立新的垂直。
1. 在完成設定步驟之後，您可以檢查並儲存垂直。  

### <a name="manage-site-level-verticals"></a>管理網站層級的縱向

1. 在您要管理縱向的 SharePoint 網站中，按一下齒輪以開啟 [設定] 面板。
1. 選取 [ **網站資訊**]，然後選取 [ **查看所有網站設定**]。  
1. 尋找 [Microsoft 搜尋] 區段，然後選取 [ **設定搜尋設定**]。
1. 在功能窗格中，移至 [自訂經驗]，然後選取 [ **縱向**]。
1. 選取現有的垂直，然後按一下 [ **編輯** ]，或按一下 [ **新增** ] 以建立新的垂直。
1. 設定好設定後，您可以檢查並儲存垂直。  

## <a name="view-the-vertical-in-the-search-result-page"></a>在搜尋結果頁面中查看垂直

搜尋[結果版面](manage-result-types.md)配置是在搜尋類別頁面上轉譯的 Graph 連接器結果所需。 在確保有適當的結果版面配置時，您可以啟用搜尋類別。 在您啟用垂直時，會有幾個小時的延遲，您才能進行查看。 您可以將 cacheClear = true 新增至 SharePoint 和 Office 中的 URL，以便立即查看垂直方向。 在 Bing 中，append &features = uncachedVerticals 至工作垂直 URL，以立即查看垂直。

> [!NOTE]
> 從行動網頁瀏覽器中查看時，已新增的縱向不會顯示在[SharePoint](https://sharepoint.com/)和[Office](https://office.com)上。

## <a name="advanced-configuration-options"></a>高級設定選項

### <a name="multiple-connections-in-a-vertical"></a>垂直中的多個連接

搜尋類別可以呈現來自多個連接器來源的結果。 此選項可提供設計搜尋結果頁面的彈性。 垂直設定程式可讓系統管理員在「內容來源」步驟中選取多個連線。

如果您正確指派盡可能多的 *語義標籤* ，則會增強這種體驗。 您可以在架構定義及攝取的點加入語義標籤。 [深入瞭解如何建立及管理語義標籤](configure-connector.md#step-6-assign-property-labels)。
[以下](configure-connector.md#step-6-assign-property-labels) 是如何建立及管理語義標籤的其他資訊。

> [!NOTE]
> - 垂直功能中的多個連線目前正在預覽中。 如需詳細資訊，請參閱 [連接器預覽功能](connectors-overview.md#what-are-the-preview-features)。
> - 連線可以新增為單一垂直的內容來源。 您無法在多個行業下使用連線。

若要設定已新增多個連線來源之搜尋類別的查詢，請使用常見來源屬性來建立查詢。

### <a name="keyword-query-language-kql"></a>關鍵字查詢語言 (KQL) 

您可以使用 [關鍵字查詢語言 (KQL) ](/sharepoint/dev/general-development/keyword-query-language-kql-syntax-reference) (有限支援) ，將查詢新增至垂直，以縮小搜尋類別上顯示的結果。 此頁面會列出可用的屬性。 建議您使用具有 boolean 運算子的任意文字關鍵字和屬性限制，以建立 KQL。 動態排名運算子（如 XRANK），不支援近程運算子和字。

以下是一些範例查詢。

|案例         | 查詢   |  
| --------- | ------ |
|排除來自封存網站的結果           |不 (路徑:HTTP//contoso。 .com/封存或路徑:HTTP//contoso。 .com/CompanyArchive) |
| 排除以檔案類型屬性為基礎的結果 | 不 (FileType： htm) |  

#### <a name="profile-query-variables"></a>設定檔查詢變數

使用垂直的 [KQL 查詢] 區段中的變數，以提供動態資料做為垂直查詢的輸入。 您可以使用設定檔查詢變數，讓搜尋結果成為已登入使用者的上下文。 設定檔查詢變數會從已登入使用者的 [設定檔](/graph/api/resources/profile)中取得值。

例如，若要為使用者建立「票據」垂直，以尋找所指派的支援票證，您可以在 [管理] 頁面中的垂直建立期間，于 [查詢] 區段中指定下列查詢：  

`AssignedTo:{Profile.accounts.userPrincipalName}`

這種語言會縮小搜尋結果，只顯示受託人為執行搜尋之使用者的專案。

[設定檔資源](/graph/api/resources/profile) 公開屬性做為集合。 例如，電子郵件地址相關的資訊會透過電子郵件集合、工作職位集合等方式公開。 使用者設定檔中所有可用的屬性都會公開為查詢變數。

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

- 查詢 `MyProperty: {Profile.emails.address}` 會解析為 *MyProperty： "Megan.Bowen@contoso.com"*。  

- 若要解決 address 屬性的所有值，請使用多重值擴充語法。 查詢 `{|MyProperty:{Profile.emails.address}}` 會解析為 *( (MyProperty： "Megan.Bowen@contoso \. com" )* 或 *(MyProperty： "meganb@hotmail \. com" )* 或  *(MyProperty： "meganb@outlook \. com" ) )*。

使用 "|" 運算子來解析多重值變數。 請參閱下表，以取得更多有關設定檔擴充的範例。

| #         | 語法 |  傳回值  |
| --------- | ------ | --- |
| 1    | MyProperty： {設定檔. 電子郵件地址}  |   "Megan \. Bowen@contoso.com"  |
| 第 | MyProperty： {Profile} 電子郵件}   |    因為 *電子郵件* 是物件，所以 {Profile} 電子郵件} 這不會解決。|
| 3     | {?MyProperty： {Profile. 電子郵件}}  |  這不會解決，因為 *電子郵件* 是物件。 "？" 運算子會忽略未解析的查詢變數。 在查詢堆疊上進一步傳遞時，將會移除此變數。   |
| 4  | {&#124;MyProperty： {Profile. Type}}    |   ( (MyProperty： "官方" ) 或 (MyProperty： "非官方" ) 或 (MyProperty： "personal" ) )     |

## <a name="limitations"></a>限制
- 在修改後，語言當地語系化不適用於 box 縱向的名稱。 
- KQL 不適用於從使用者 OneDrive 所呈現的內容。 
- 自訂的縱向不會出現在 Microsoft 搜尋的行動裝置視圖上。 
- 在 [人員] 垂直上不支援新增查詢。 
- 組織中的來賓使用者看不到縱向修改和新的縱向。 
- 不支援縱向重新排序。
- 在 Bing 中的 Microsoft search 中，所有索引標籤的垂直重新命名功能都不受支援。

## <a name="troubleshooting"></a>正在疑難排解

以下列出您可能會遇到的常見問題，以及修正這些問題的動作。

|問題  |動作  |
|---------|---------|
| 在垂直上看到「發生錯誤」錯誤訊息。 | 需要有垂直和結果類型，才可完成設定。 請確定內容來源已設定兩者。 |
| 在垂直頁面上沒有看到任何內容來源。 | 請確定您已設定連接器和索引的資料。   |



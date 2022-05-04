---
title: 'Dynamics 365 會產生 Microsoft 搜尋 (Preview) '
ms.author: dawholl
author: dawholl
manager: kellis
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
ms.date: 05/03/2022
description: 管理 Dynamics 365 內容在搜尋結果中的顯示方式
ms.openlocfilehash: 4d234ffe67f6f4ed2eeb03cb89e7c4d23e36e53b
ms.sourcegitcommit: 00c673527e6806c9652c8e3de76ab4f6522b7c23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2022
ms.locfileid: "65187182"
---
# <a name="dynamics-365-results-in-microsoft-search-preview"></a>Dynamics 365 會產生 Microsoft 搜尋 (Preview) 

Microsoft Dynamics 365 是一系列智慧型商務應用程式，專為企業資源規劃和客戶關係管理所設計。 透過 Dynamics 365 產生Microsoft 搜尋，使用者可以輕鬆地找到儲存在 Dynamics 365 中最相關的客戶和商務資料。 Dynamics 365 連接器提供一些主要優點：

* **容易使用：** 使用者可以輕鬆快速地尋找儲存在 Dynamics 365 中的重要資訊，而不需要流覽至新的應用程式或頁面。
* **易於尋找：** Bing.com、Office.com 和 SharePoint 中的使用者可以看到 Dynamics 365 內容。
* **內建資料保護：** Dynamics 365 結果只會針對具有已連線實例存取權的使用者顯示。 
* **快速設定：** 輕鬆設定及維護與 Dynamics 365 實例的搜尋連線。
* **整合搜尋體驗：** 為了維持一致的體驗，Dynamics 365 結果會在所有搜尋進入點之間保持一致。 無論您在何處搜尋，都會以相同的外觀和風格取得相同的結果。

我們的 Dynamics 365 連接器目前處於預覽狀態。 如果您有興趣加入預覽版，請在 [aka.ms/D365-ACS-Preview-MicrosoftSearch](https://aka.ms/D365-ACS-Preview-MicrosoftSearch)中讓我們知道。

## <a name="user-experience"></a>使用者體驗

Dynamics 365 答案會出現在所有Microsoft 搜尋畫布的搜尋結果中，包括 SharePoint Online、Bing 和 Office。

:::image type="content" alt-text="SharePoint、Bing 和 Office 上的 Dynamics 365 解答螢幕擷取畫面。" source="media/dynamics365/dynamics365-answer.png" lightbox="media/dynamics365/dynamics365-answer.png":::

從答案中，使用 [更多 Dynamics 365 結果] 連結可輕鬆查看更多 **Dynamics 365 搜尋結果** 。 它會將使用者帶至專用的 Dynamics 365 結果頁面，其中包含更多與其查詢相關的結果。

:::image type="content" alt-text="Dynamics 365 垂直的螢幕擷取畫面，以及SharePoint、Bing和Office的結果。" source="media/dynamics365/dynamics365-vertical.png" lightbox="media/dynamics365/dynamics365-vertical.png":::

按一下或點選任何結果會開啟 Dynamics 365，並顯示詳細資訊。

:::image type="content" alt-text="Dynamics 365 中詳細資料頁面的螢幕擷取畫面。" source="media/dynamics365/dynamics365-detail-page.png" lightbox="media/dynamics365/dynamics365-detail-page.png":::

無論您的使用者從何處開始搜尋，其體驗都會一致，並可讓他們快速找到最相關的 Dynamics 365 結果。 查看我們的 Microsoft Build 2021 影片以取得示範。

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4P83t]

### <a name="supported-query-patterns"></a>支援的查詢模式

使用者會在專用的 Dynamics 365 和所有垂直上看到結果。 任一垂直上的 Dynamics 365 搜尋都不區分大小寫。

在 Dynamics 365 垂直版上，搜尋支援 Dynamics 365 應用程式中使用的相同語言，包括 AND、OR 和 NOT 等簡單運算子。 如需詳細資訊，請 [參閱使用運算子](/power-apps/user/relevance-search#working-with-operators)。

在 [全部] 垂直上，當使用者搜尋 Dynamics 結果時，會觸發 Dynamics 答案。 自然語言查詢 (依名稱或位置包含一般實體的查詢，例如，包含 Dynamics 應用程式名稱的) 和查詢可以觸發答案。 以下是一些範例：

* 神秘是 Contoso 的連絡人
* 西雅圖的帳戶是什麼
* 高優先順序通話
* 連絡人遺失的電子郵件
* D365 連絡人
* Contoso Dynamics Sales

## <a name="admin-experience"></a>系統管理員體驗

在 Dynamics 365 連接器中，您可以輕鬆地設定、自訂和編輯。 如果您在使用預覽連接器時有意見反應或問題，請 [與我們連絡](https://aka.ms/Dynamics365ConnectorFeedback)。

### <a name="configure"></a>設定

透過這個簡單的設定，您可以為組織中的人員啟用 Dynamics 365 結果Microsoft 搜尋。 若要成功設定此連線，建議您在開始之前先確認這些設定：

* 已針對您想要連線的 Dynamics 365 環境啟用 Dataverse 搜尋。 如需詳細資訊， [請參閱為您的環境設定 Dataverse 搜尋](/power-platform/admin/configure-relevance-search-organization)。
* 設定連接器的搜尋系統管理員具有使用 Dynamics 365 的正確授權。 如需詳細資訊， [請參閱指派授權](/power-platform/admin/assign-licenses)。
* 搜尋系統管理員具有您想要設定之 Dynamics 365 環境的系統管理員存取權。 如需詳細資訊，請 [參閱將使用者新增至環境](/power-platform/admin/add-users-to-environment)。

確認這些設定之後，請遵循下列步驟來設定連接器：

1. 在[Microsoft 365 系統管理中心](https://admin.microsoft.com)中，移至[[資料來源]](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/connectors)。

2. 在 [Microsoft 應用程式和服務] 區段的 [Microsoft Dynamics 365] 下，選取 [ **管理** ] 以開啟 [Microsoft Dynamics 365] 面板。

3. 為您的組織啟用連接器。

4. 在 [ **端點] 清單中** ，選取您的 Dynamics 365 環境。

5. 在 [ **連線名稱]** 中，輸入此連線的描述性名稱。

6. 檢閱並選取同意核取方塊。

7. 選 **取 [儲存** ] 以完成連線設定。

:::image type="content" alt-text="Microsoft 365 系統管理中心中 Dynamics 365 安裝面板的螢幕擷取畫面。" source="media/dynamics365/dynamic365-connection-setup.png" lightbox="media/dynamics365/dynamic365-connection-setup.png":::

> [!TIP]
> 若要厘清使用者可在搜尋垂直中找到的內容類型，建議您更新垂直名稱。 若要自訂 Dynamics 365 垂直的名稱，請按一下 **[編輯垂直]**。 如需詳細資訊，請 [參閱管理垂直搜尋](/microsoftsearch/manage-verticals)。

安裝程式完成時，專用的 Dynamics 365 垂直和答案最多可能需要 24 小時才會出現。 Dynamics 結果只會針對具有有效 Dynamics 365 授權和已連線 Dynamics 365 環境存取權的使用者顯示。 您可以隨時變更連線端點環境或停用連線。

### <a name="customize"></a>自訂

透過 Dataverse 搜尋快速尋找檢視，您可以修改可搜尋的實體和欄位。 您也可以自訂要針對每個實體類型顯示的欄位。 對快速尋找檢視所做的變更會出現在Microsoft 搜尋結果和您的 Dynamics 365 應用程式中。 如需修改快速尋找檢視的相關資訊，請 [參閱選取每個資料表的可搜尋欄位和篩選](/power-platform/admin/configure-relevance-search-organization#select-searchable-fields-and-filters-for-each-table)。

### <a name="edit"></a>編輯

啟用連線之後，您可以修改端點和連線名稱。 在 [[資料來源](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/connectors)] 的已設定連線下方，選取 [ **編輯** ] 進行變更。
:::image type="content" alt-text="Microsoft 365 系統管理中心中 Dynamics 365 連接器 [編輯] 按鈕和麵板的螢幕擷取畫面。" source="media/dynamics365/dynamics365-edit-connector.png" lightbox="media/dynamics365/dynamics365-edit-connector.png":::

若要停用連線，請清除 [ **為您的組織啟用此聯** 機] 核取方塊和 [ **儲存]**。

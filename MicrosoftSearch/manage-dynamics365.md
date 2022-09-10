---
title: Microsoft Search 中的 Dataverse 和 Dynamics 365 結果
ms.author: dawholl
author: dawholl
manager: kellis
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
ms.date: 05/03/2022
description: 管理 Dataverse 和 Dynamics 365 內容在搜尋結果中的顯示方式
ms.openlocfilehash: 0dfd27fd1e49b7d24b8f7e3347bdf9df98c70fba
ms.sourcegitcommit: 53051510668d3e082444cf5b19c7bb27c9342b8e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2022
ms.locfileid: "67643050"
---
# <a name="dataverse-and-dynamics-365-results-in-microsoft-search"></a>Microsoft Search 中的 Dataverse 和 Dynamics 365 結果

Microsoft Dataverse 是一個雲端儲存平臺，可讓您安全地儲存和管理商務應用程式所使用的資料。 Microsoft Dynamics 365 是一系列以 Dataverse 搜尋平臺為基礎的智慧型商務應用程式，專為企業資源規劃和客戶關係管理而設計。 在 Microsoft Search 中使用 Dataverse 結果時，傳統 Dynamics 365 應用程式和以 Dataverse 為基礎的自訂模型驅動 Power Apps 的使用者都能夠輕鬆地找到其相關客戶資料。 Dataverse 連接器提供一些主要優點：

* **容易使用：** 使用者可以輕鬆快速地尋找儲存在 Dataverse 和 Dynamics 365 中的重要資訊，而不需要流覽至新的應用程式或頁面。
* **易於尋找：** Bing.com、Office.com 和 SharePoint 中的使用者可以看到 Dataverse 和 Dynamics 365 內容。
* **內建資料保護：** Dataverse 和 Dynamics 365 結果只會針對具有已連線實例和記錄存取權的使用者顯示。 
* **快速設定：** 輕鬆設定及維護 Dataverse 實例的搜尋連線。
* **整合搜尋體驗：** 為了維持一致的體驗，Dataverse 結果會在所有搜尋進入點之間保持一致。 無論您在何處搜尋，都會以相同的外觀和風格取得相同的結果。

## <a name="user-experience"></a>使用者體驗

Dataverse 答案會出現在所有 Microsoft 搜尋畫布的搜尋結果中，包括 SharePoint Online、Bing 和 Office。

:::image type="content" alt-text="SharePoint、Bing 和 Office 上 Dynamics 365 答案的螢幕擷取畫面。" source="media/dynamics365/dynamics365-answer.png" lightbox="media/dynamics365/dynamics365-answer.png":::

從答案中，使用 [更多 Dynamics 365 結果] 連結可輕鬆查看更多 **Dynamics 365 搜尋結果** 。 它會將使用者帶至專用的 Dynamics 365 結果頁面，其中包含更多與其查詢相關的結果。

:::image type="content" alt-text="SharePoint、Bing 和 Office 上 Dynamics 365 垂直和結果的螢幕擷取畫面。" source="media/dynamics365/dynamics365-vertical.png" lightbox="media/dynamics365/dynamics365-vertical.png":::

按一下或點選任何結果會開啟 Dynamics 365 或您的自訂應用程式，並顯示詳細資訊。

:::image type="content" alt-text="Dynamics 365 中詳細資料頁面的螢幕擷取畫面。" source="media/dynamics365/dynamics365-detail-page.png" lightbox="media/dynamics365/dynamics365-detail-page.png":::

無論您的使用者從何處開始搜尋，其體驗都會一致，並可讓他們快速找到最相關的 Dataverse 結果。 查看我們的 Microsoft Build 2022 影片以取得示範。

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4Zf9u]

### <a name="supported-query-patterns"></a>支援的查詢模式

使用者會在專用的 Dataverse 和所有垂直上看到結果。 在任一垂直上搜尋都不區分大小寫。

在專用垂直上，搜尋支援 Dataverse 搜尋和傳統 Dynamics 365 應用程式中使用的相同語言，包括 AND、OR 和 NOT 等簡單運算子。 如需詳細資訊，請 [參閱使用運算子](/power-apps/user/relevance-search#working-with-operators)。

在 [全部] 垂直上，當使用者搜尋 Dynamics 結果時，會觸發 Dynamics 答案。 自然語言查詢 (依名稱或位置包含一般實體的查詢，例如，包含 Dynamics 應用程式名稱的) 和查詢可以觸發答案。 以下是一些範例：

* 誰是 Contoso 的連絡人
* 西雅圖的帳戶是什麼
* 高優先順序通話
* 連絡人遺失的電子郵件
* D365 連絡人
* Contoso Dynamics Sales

## <a name="admin-experience"></a>管理員體驗

Dataverse 連接器很容易設定、自訂和編輯。 如果您在使用連接器時有意見反應或問題，請 [與我們連絡](https://aka.ms/Dynamics365ConnectorFeedback)。

### <a name="configure"></a>設定

透過這個簡單的設定，您可以在 Microsoft Search 中為組織中的人員啟用 Dataverse 結果。 若要成功設定此連線，建議您在開始之前先確認這些設定：

* 已針對您想要連線的 Dynamics 365 環境啟用 Dataverse 搜尋。 如需詳細資訊， [請參閱為您的環境設定 Dataverse 搜尋](/power-platform/admin/configure-relevance-search-organization)。
* 設定連接器的搜尋系統管理員具有使用 Dynamics 365 的正確授權。 如需詳細資訊， [請參閱指派授權](/power-platform/admin/assign-licenses)。
* 搜尋系統管理員具有您想要設定之 Dynamics 365 或 Dataverse 環境的系統管理員存取權。 如需詳細資訊，請 [參閱將使用者新增至環境](/power-platform/admin/add-users-to-environment)。

確認這些設定之後，請遵循下列步驟來設定連接器：

1. 在[Microsoft 365 系統管理中心](https://admin.microsoft.com)中，移至[[資料來源]](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/connectors)。

2. 在 [Microsoft 應用程式和服務] 區段中，選取 [ **新增應用程式或服務]**，然後選取 [ **連線到 Dynamics 365]**。 選 **取 [下一步** ] 以開啟 [連線詳細資料] 窗格。

3. 輸入連線名稱和描述。 在 [ **Dynamics 365 環境** ] 下拉式清單中，選取您要連線的環境。

4. 檢閱並選取同意核取方塊。 選 **取 [下一步** ]，然後檢閱連線詳細資料。

5. 選 **取 [完成**]，然後選取 [ **完成** ] 以完成連線設定。

6. 安裝成功之後，您的 Dynamics 365 連線應該會顯示 [已就緒] 的 [連線] 狀態。

:::image type="content" alt-text="Dynamics 365 連線成功設定的螢幕擷取畫面，並在Microsoft 365 系統管理中心中顯示 [就緒] 線上狀態。" source="media/dynamics365/dynamic365-connection-setup.png" lightbox="media/dynamics365/dynamic365-connection-setup.png":::

> [!TIP]
> 若要厘清使用者可在搜尋垂直中找到的內容類型，建議您更新垂直名稱。 若要自訂垂直的名稱，請按一下 **[編輯垂直]**。 如需詳細資訊，請 [參閱管理垂直搜尋](/microsoftsearch/manage-verticals)。

安裝程式完成時，專用的 Dataverse 垂直和答案最多可能需要 24 小時才會出現。 結果只會顯示給具有有效 Dynamics 365 授權和已連線 Dataverse 環境存取權的使用者。 您可以隨時變更連線端點環境或停用連線。

### <a name="customize"></a>自訂

透過 Dataverse 搜尋快速尋找檢視，您可以修改可搜尋的實體和欄位。 針對每個實體類型的快速尋找檢視中設定的前四個檢視資料行，將會顯示在您的 Microsoft 搜尋結果中。 對快速尋找檢視所做的變更會出現在 Microsoft 搜尋結果和您的 Dynamics 365 應用程式中。 如需修改快速尋找檢視的相關資訊，請 [參閱選取每個資料表的可搜尋欄位和篩選](/power-platform/admin/configure-relevance-search-organization#select-searchable-fields-and-filters-for-each-table)。

### <a name="edit"></a>編輯

啟用連線之後，您可以修改連線詳細資料，包括名稱、描述和環境。 在 [[資料來源](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/connectors)] 的已設定連線下方，選取 [ **編輯** ] 進行變更。
:::image type="content" alt-text="Microsoft 365 系統管理中心中 Dynamics 365 連接器 [編輯] 按鈕和麵板的螢幕擷取畫面。" source="media/dynamics365/dynamics365-edit-connector.png" lightbox="media/dynamics365/dynamics365-edit-connector.png":::

若要停用連線，請清除 [ **為您的組織啟用此聯** 機] 核取方塊和 [ **儲存]**。

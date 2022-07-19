---
title: Microsoft Graph 連接器的合規性解決方案
ms.author: vivg
author: vivg
manager: harshkum
audience: Admin
ms.audience: Admin
ms.topic: article
ms.service: mssearch
localization_priority: Normal
search.appverid:
- BFB160
- MET150
- MOE150
description: 電子檔探索的 Microsoft Graph 連接器概觀
ms.openlocfilehash: f241b482f005e56d8368e1dbe84f9043a562f8e4
ms.sourcegitcommit: 6ee362000b10ade490631eb707a89a04b51fff47
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2022
ms.locfileid: "66843842"
---
# <a name="microsoft-graph-connectors-overview-for-ediscovery"></a>電子檔探索的 Microsoft Graph 連接器概觀

電子搜索 (eDiscovery) 是識別與傳遞電子資訊的程序，而且此類資訊可在法律案件中做為呈堂證據。 您可以在 Microsoft Purview 中使用電子檔探索工具來搜尋 [Microsoft 365](https://www.microsoft.com/microsoft-365)中的內容。 使用 Microsoft Graph 連接器，您的組織可以編制協力廠商資料的索引，並將其包含在收集、檢閱和匯出的電子檔探索進階案例中。

本文旨在協助 Microsoft 365 系統管理員設定適用于電子檔探索的 Graph 連接器。

## <a name="before-you-get-started"></a>開始之前
* 若要存取和管理您的 Microsoft Graph 連接器，您必須被指定為租使用者的 **搜尋系統管理員** 。 如需詳細資訊， [請參閱指派系統管理員角色](/office365/admin/add-users/assign-admin-roles)。
* **需要 eDiscovery Premium** ，才能在案例中包含 Graph 連接器內容。 

## <a name="supported-data-sources"></a>支援的資料來源

### <a name="microsoft-graph-connectors"></a>Microsoft Graph 連接器

您可以使用 Microsoft 建立的連接器來連線到下列資料來源：

<!---Add links below when new docs are created--->
* [Azure DevOps 工作專案](azure-devops-connector.md)
* [Azure DevOps Wiki](azure-devops-wiki-connector.md)

## <a name="graph-connector-configuration-steps-for-ediscovery"></a>電子檔探索的圖形連接器設定步驟
完成下列步驟以設定任何 Microsoft Graph 連接器：

1. 在Microsoft 365 系統管理中心中登入您的系統[管理員](https://admin.microsoft.com)帳戶。


2. 在流覽窗格中，選取 [ **設定]**，然後選取 **[搜尋&智慧]**。 選取 [ [資料來源] 索引標籤](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/Connectors)。

3. 選取 **[+新增**]，然後從可用選項的功能表中選取您選擇的任何 [電子檔探索支援的資料來源](#supported-data-sources) 。

4. 在 [**選取體驗]** 步驟中，選擇 **[搜尋、智慧和探索**] 下的 [**合規性**]。

![選取 [體驗] 畫面的螢幕擷取畫面，其中已選取 [合規性] 選項。](./media/compliance-ediscovery/compliance-ediscovery-select-experiences.png)

> [!NOTE]
> 
> 您可以選擇連線的 **Microsoft Search** 和 **合規性** 選項。

5. 請閱讀 [設定您的 Microsoft Graph 連接器](configure-connector.md) 一文，以瞭解一般連接器設定指示。 完成連接器設定併發布連線。

## <a name="ediscovery-on-graph-connector-content"></a>Graph 連接器內容上的電子檔探索

### <a name="add-graph-connector-as-a-data-source-within-a-case"></a>將 Graph 連接器新增為案例中的資料來源

一旦為組織建立 Graph 連接器並啟用電子檔探索，將 Graph 連接器資料來源新增至案例的選項將會在非 Microsoft 365 位置下提供。 只有已建立並啟用的連接器可供電子檔探索管理員在案例中包含。  

完成下列步驟以建立案例：

1. 移至 <a href="https://go.microsoft.com/fwlink/p/?linkid=2077149" target="_blank">合規性入口網站</a> ，並使用已獲指派電子檔探索許可權之使用者帳戶的認證登入。 組織管理角色群組的成員也可以建立電子檔探索 (進階) 案例。

2. 在合規性入口網站的左側流覽窗格中，按一下 [**全部顯示**]，然後選取 **[電子檔探索進階**  >  ]，然後選取 [<a href="https://go.microsoft.com/fwlink/p/?linkid=2173764" target="_blank">**案例]** 索引標籤</a>。****

3. 選取 ****[建立案例]。

4. 在 [ **新增電子檔探索案例** ] 飛出視窗頁面上，提供案例 () 所需的名稱，然後輸入選擇性的案例編號和描述。 案例名稱在您的組織中必須是唯一的。

5. 按一下 **[儲存** ] 以建立案例。

![新 ediscovery 案例建立的螢幕擷取畫面。](./media/compliance-ediscovery/compliance-ediscovery-new-ediscovery-case.png)

6. 選取 **[資料來源] 索引** 標籤。按一下 **[新增資料來源]** ，然後選取 [ **新增資料位置]**。

![新增資料來源選項的螢幕擷取畫面。](./media/compliance-ediscovery/compliance-ediscovery-add-data-sources.png)

7. 在 **[M365 已連線的應用程式** ] 底下，按一下 **[編輯 M365 已連線的應用程式]**。

![編輯 M365 連線應用程式選項的螢幕擷取畫面。](./media/compliance-ediscovery/compliance-ediscovery-edit-m365-connected-apps.png)

8. 選取您要新增的連線，然後按一下 [ **新增]**。

![可新增之資料來源清單的螢幕擷取畫面。](./media/compliance-ediscovery/compliance-ediscovery-add-m365-connected-apps.png)

9. 按一下 **[新增]**。

10. 等到 [ **編制索引作業狀態** ] 變更為 [ *成功]*。

![已新增資料來源清單檢視的螢幕擷取畫面，其中顯示索引狀態。](./media/compliance-ediscovery/compliance-ediscovery-indexing-job-status-successful.png)

> [!NOTE]
> 
> 如需建立和管理 Microsoft Purview 電子檔探索 (Premium) 案例的詳細指引，請參閱在[Microsoft 365 中建立和管理電子檔探索 (Premium) 案例](/microsoft-365/compliance/create-and-manage-advanced-ediscoveryv2-case.md)的檔

### <a name="collect-graph-connectors-content"></a>收集圖形連接器內容 


將 Graph 連接器內容新增為數據源之後，即可使用此內容進行搜尋和收集。 在集合精靈中，選取 Graph 連接器內容作為 **非監管資料來源**，使用日期範圍、關鍵字等條件來搜尋連線的內容，只收集感興趣的內容。 精靈完成時，取得包含搜尋準則點擊內容數量的估計值，並將集合認可至檢閱集。

![在新集合建立中新增非監管資料來源之步驟的螢幕擷取畫面。](./media/compliance-ediscovery/compliance-ediscovery-new-collection-select-non-custodial-sources.png)

### <a name="review-content"></a>檢閱內容 

收集到檢閱集之後，電子檔探索管理員可以檢閱 Graph 連接器中的內容，以深入瞭解內容，並努力評估資訊是否重要且與案例相關。

![檢閱使用 Graph 連接器新增之內容的螢幕擷取畫面。](./media/compliance-ediscovery/compliance-ediscovery-review-content.png)


### <a name="export-content"></a>匯出內容 

一旦驗證收集到檢閱中的內容是正確的內容之後，就可以直接從檢閱集匯出此內容。 選取 [匯出選項] 並提交匯出作業，以便從檢閱集匯出連接器內容。 

<!---## Troubleshooting-->
<!---Insert troubleshooting recommendations-->

## <a name="limitations"></a>限制

1. 不支援檢閱圖表連接器內容的範例。

2. 不支援將圖形連接器內容置於合法保留，作為電子檔探索案例的一部分。

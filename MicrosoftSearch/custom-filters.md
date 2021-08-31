---
title: 管理篩選
ms.author: v-revathib
author: revathi-b
manager: jeffkizn
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
description: 管理 SERP 上使用的篩選
ms.openlocfilehash: c614d4b60c746f2e18fdb3352281891ea5134373
ms.sourcegitcommit: cc9d743bcf5e998720ce9cd6eefb4061d913dc65
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2021
ms.locfileid: "58702191"
---
# <a name="manage-filters"></a>管理篩選

篩選允許使用者精簡查詢的結果，並顯示精緻的結果。 您可以在 Microsoft 搜尋體驗中自訂使用者可用的篩選器。

[搜尋] 頁面上有兩種篩選類型可供使用。

- 篩選器現成
- 自訂篩選

> [!NOTE]
> 自訂篩選器目前是針對系統管理員和使用者在目標發行中的預覽。 如需預覽的詳細資訊，請參閱 [連接器預覽功能](connectors-overview.md#what-are-the-preview-features)。

## <a name="out-of-the-box-filters"></a>篩選器現成

在預設的搜尋行業（如所有、檔案、影像及新聞）中，可以使用現成的篩選器。 在 ' All ' 和 ' File ' 行業，您可以在 FileType 屬性和「上次修改」篩選上，看到 LastModifiedTime 屬性上的「檔案類型」篩選。 SharePoint Home、Office .com、SharePoint 網站及 Bing 中的工作垂直，都可以使用這些篩選器。

## <a name="custom-filters"></a>自訂篩選

篩選可以新增至組織和網站層級的自訂搜尋行業。 可精簡搜尋 managed 屬性是用來設定垂直管理嚮導中的篩選器。  然後，您可以在以 connection 屬性為基礎的垂直內部建立自訂篩選。 例如，您可以在垂直方向的 ServiceNow 連接上建立已發佈的 On filter。

在組織範圍內為縱向設定的篩選會在組織範圍內使用。 篩選也可在網站的範圍內設定。  

## <a name="create-organization-level-filters"></a>建立組織層級篩選

1. 在  [Microsoft 365 系統管理中心](https://admin.microsoft.com/)中，移至 [ [**縱向**](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/verticals)]
2. 選取您想要建立篩選的慣用垂直，然後按一下 [ **編輯**]。  
3. 流覽至豎直的嚮導中的 [篩選] 步驟。
4. 按一下 [ **新增篩選** ] 以設定可精簡搜尋 managed 屬性上的篩選器。
5. 新增篩選後，您可以檢查並儲存垂直。

## <a name="create-sharepoint-site-level-filters"></a>建立 SharePoint 網站層級篩選

1. 在 [SharePoint 系統管理中心](https://sharepoint.com/)，移至設定。
2. 尋找 [Microsoft 搜尋] 區段，然後 **為此網站集合選取 [設定 Microsoft 搜尋**]。
3. 在功能窗格中，移至 [自訂經驗]，然後選取 [  **縱向**]。
4. 選取您慣用的垂直方向以建立篩選，然後按一下 [ **編輯**]。
5. 流覽至豎直的嚮導中的 [篩選] 步驟。
6. 按一下 [ **新增篩選** ] 以設定可精簡搜尋 managed 屬性上的篩選器。
7. 新增篩選後，您可以檢查並儲存垂直。

## <a name="filter-across-multiple-properties"></a>跨多個屬性進行篩選

您可以使用一或多個內容來源來建立縱向。 當以多個內容來源設定垂直時，精簡器的屬性清單會顯示每個可精簡搜尋屬性所屬的內容來源。 通用 managed 屬性會根據名稱 (或別名) 和資料類型進行合併。 篩選也可以在這些一般屬性上進行設定。 若要執行此操作，您可以在通用別名上建立篩選，以在不同的連線上使用別名來源屬性。 例如，您可以建立別名 **，使其** 跨越 ServiceNow 和 Jira 連線，如下所示：

 | 連線 | 屬性	 | 別名 |
 | --- | --- | --- |
 | 服務現在 | 擁有者 | 作者 |
 | Jira | 發行者 | 作者 |

## <a name="important-details"></a>重要詳細資料

- 篩選只可以新增至自訂的縱向。 新的篩選器無法新增至現成的縱向縱向，像所有的檔案、人員、網站和新聞。
- 篩選可在 Text 和 DateTime 屬性上進行設定。
- 您的總數限制為50個篩選。
- 無法調整 box 篩選的順序。
- 篩選器不支援 OneDrive 內容。 對應于來自 OneDrive 內容之搜尋結果的篩選值，不會出現在篩選上。
- 自訂篩選值會顯示從 SharePoint 內容的選項，而非從某個磁片磁碟機內容。例如，如果您為「author」建立自訂篩選，而且 SharePoint 內容包含的結果只來自 author、「張瑾」和「OneDrive」內容，只會從名為「John」的作者取得結果，所以 Author 自訂篩選只會顯示「張瑾雯」為唯一的選項。
- 使用時所顯示的篩選值 SharePoint 內容會套用到 OneDrive 內容時使用。

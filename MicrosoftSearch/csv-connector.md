---
title: 適用于 Microsoft Search 的 CSV 連接器
ms.author: dawholl
author: dawholl
manager: kellis
audience: Admin
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
description: 設定適用于 SharePoint 或 Azure Data Lake Storage 來源的 Microsoft Search CSV 連接器。
ms.openlocfilehash: e564e61a57c76ab2eb010ed533eaee3ac3def74d
ms.sourcegitcommit: a821305e638808c376708289bd58ad2bb3272e1b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2022
ms.locfileid: "65959806"
---
# <a name="csv-connector"></a>CSV 連接器

CSV Graph 連接器可讓您的組織從儲存在 SharePoint 文件庫和 Azure Data Lake Storage (ADLS) 中的 CSV 檔案內嵌內容。 設定來自這些來源的連接器和索引內容之後，終端使用者就可以在 Microsoft Search 中找到 CSV 檔案。

> [!NOTE]
> 請閱讀 [**Graph 連接器的安裝**](configure-connector.md) 程式一文，以瞭解一般 Graph 連接器設定指示。

本文適用于設定、執行及監視 CSV 連接器的任何人。 它會補充一般設定程式，並顯示僅適用于此連接器的指示。

<!---## Before you get started-->
## <a name="before-you-get-started"></a>開始之前

針對 SharePoint 資料來源，您必須建立具有 Oauth 設定的 SharePoint 應用程式。 針對 ADLS 資料來源，您必須建立 ADLS 儲存體帳戶。

### <a name="create-a-sharepoint-app-with-oauth-configuration"></a>使用 Oauth 設定建立 SharePoint 應用程式

確認您想要編制索引的.csv檔案已上傳至 SharePoint 文件庫。 您可以使用現有的 SharePoint 網站或建立新的網站。

#### <a name="create-a-sharepoint-app"></a>建立 SharePoint 應用程式

1. 移至  `https://Org-Name.sharepoint.com/Site-Name/_layouts/15/appregnew.aspx` 。
2. 在 [用戶端識別碼] 和 [用戶端密碼] 欄位上，選取 [ **產生]**。
1. 針對 [標題]，輸入應用程式名稱。
1. 在 [應用程式域] 欄位中，輸入 `www.gcs.com` 。
1. 在 [重新導向 URL] 欄位中，輸入 `https://www.gcs.com` 。
1. 選取 **[建立]**。
1. 複製應用程式設定資訊，包括用戶端識別碼和用戶端密碼。 當您設定 CSV 連接器時，將會需要它。

#### <a name="enable-app-permissions-to-allow-customappauthentication"></a>啟用應用程式許可權以允許 CustomAppAuthentication

在 PowerShell 中，以系統管理模式執行這些命令。 使用設定連接器之系統管理員的電子郵件地址和您的組織名稱。 當密碼快顯視窗出現時，系統管理員應該輸入其密碼。

```powershell
Install-Module -Name Microsoft.Online.SharePoint.PowerShell
$adminUPN=”<admin@contoso.onmicrosoft.com>”
$orgName=“<contoso>”
$userCredential = Get-Credential -UserName $adminUPN -Message "Enter your password."
Connect-SPOService -Url https://$orgName-admin.sharepoint.com -Credential $userCredential
Set-spotenant –DisableCustomAppAuthentication $false
```

#### <a name="complete-the-app-configuration"></a>完成應用程式設定

1. 移至`https://Org-Name.sharepoint.com/Site-Name/_layouts/15/appinv.aspx`。
2. 在 [應用程式識別碼] 欄位中，貼上 SharePoint 應用程式的用戶端識別碼，然後選取 **[查閱]**。
3. 在 [許可權要求 XML] 欄位中，貼上此程式碼，然後選取 [ **建立]**。

```xml
<AppPermissionRequests AllowAppOnlyPolicy="true">
    <AppPermissionRequest Scope="http://sharepoint/content/sitecollection/web" Right="Read" />
</AppPermissionRequests>
```

4. 選取 **[信任]**。

### <a name="create-an-adls-storage-account"></a>建立 ADLS 儲存體帳戶

如需逐步指引，請參閱 [建立儲存體帳戶](/azure/storage/common/storage-account-create#create-a-storage-account-1)。 若要允許檔案儲存功能，請在 [進階] 索引標籤上，選取 [ **啟用階層命名空間** ] 和 **[建立此網站的容器]**。

當您設定 CSV 連接器時，您必須提供主要儲存體連接字串。 若要尋找它，請開啟您建立的儲存體帳戶，然後選 **取 [存取金鑰]**。 選 **取 [顯示金鑰** ]，然後複製 Key1 的連接字串。

## <a name="step-1-add-a-graph-connector-in-the-microsoft-365-admin-center"></a>步驟 1：在 Microsoft 365 系統管理中心新增 Graph 連接器

請遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup 
instructions.-->

## <a name="step-2-select-experiences"></a>步驟 2：選取體驗

目前，CSV 連接器僅支援搜尋體驗。

:::image type="content" source="media/csv-connector/csv-connector-search-experiences.png" alt-text="已選取 Microsoft 搜尋體驗的 CSV 連接器。" lightbox="media/csv-connector/csv-connector-search-experiences.png":::

## <a name="step-3-name-the-connection"></a>步驟 3：為連線命名

請遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup 
instructions.-->

## <a name="step-4-configure-connection-settings"></a>步驟 4：設定連線設定

SharePoint 和 ADLS 的資料來源設定不同。

### <a name="for-a-sharepoint-source"></a>針對 SharePoint 來源

1. 在 [資料來源設定] 中，選取 **[SharePoint** ] 作為您的資料來源。
1. 例如，在 **SharePoint 網站** 中，輸入網站 URL `https://Org-Name.sharepoint.com/Site-Name` 。
1. 在 **文件庫** 中，輸入儲存.csv檔案的文件庫名稱。
1. 在 **[驗證類型**] 中，選 **取 [Oauth2.0]， (用戶端認證)**。
1. 輸入您在建立 SharePoint 應用程式時複製的用戶端識別碼和用戶端密碼。
1. 選 **取 [測試連線]**。 您應該會收到 **連線成功** 訊息。

:::image type="content" source="media/csv-connector/csv-connector-data-source-settings.png" alt-text="具有 SharePoint 網站資料來源設定的 CSV 連接器。" lightbox="media/csv-connector/csv-connector-data-source-settings.png":::

若要控制檔案層級的存取權，請輸入 Azure AD 使用者或群組。

:::image type="content" source="media/csv-connector/csv-connector-acl.png" alt-text="包含使用者和群組的存取控制清單。" lightbox="media/csv-connector/csv-connector-acl.png":::

### <a name="for-an-adls-source"></a>針對 ADLS 來源

1. 在 [資料來源設定] 中，選取 **[Azure Data Lake Storage (ADLS)** 作為您的資料來源。
1. 在 **[主要儲存體連接字串**] 中，輸入您複製的連接字串。
1. 輸入 **[容器名稱** ] 和 **[檔案名]**。
1. 選 **取 [測試連線]**。 您應該會收到 **連線成功** 訊息。

:::image type="content" source="media/csv-connector/csv-connector-adls-data-source-settings.png" alt-text="具有 Azure Data Lake Storage 來源之資料來源設定的 CSV 連接器。" lightbox="media/csv-connector/csv-connector-adls-data-source-settings.png":::

> [!NOTE]
> 如果您的資料來源包含多個具有相同標頭的.csv檔案，請選取 [ **在位置包含所有 CSV 檔案]**。

若要控制檔案層級的存取權，請輸入 Azure AD 使用者或群組。

:::image type="content" source="media/csv-connector/csv-connector-acl.png" alt-text="包含使用者和群組的存取控制清單。" lightbox="media/csv-connector/csv-connector-acl.png":::

## <a name="step-5-multi-items-delimiter-optional"></a>步驟 5：選擇性)  (多重專案分隔符號

如果您的來源資料行可以接受多個值，請輸入多重專案分隔符號、分號 (;例如) 。

## <a name="step-6-parsed-properties-settings"></a>步驟 6：剖析的屬性設定

此頁面會將您.csv檔案中的第一個資料列傳回為來源屬性。 若要修改 Datatype，請在 [ **唯一識別碼** ] 清單中選取至少一個選項。

若要控制專案層級的存取權，請選取對應至 [允許的使用者] 和 [允許的群組] 的資料行。 您應該在.csv檔案中包含兩個數據行 AllowedUsers 和 AllowedGroups。 每個資料列都應該包含 Azure AD 識別碼。

:::image type="content" source="media/csv-connector/csv-connector-acl-item-level.png" alt-text="專案層級存取控制設定。" lightbox="media/csv-connector/csv-connector-acl-item-level.png":::

> [!NOTE]
> CSV 連接器支援檔案或專案層級存取控制。 如果兩者都已啟用，則只會套用檔案層級存取控制。

## <a name="step-7-assign-property-labels"></a>步驟 7：指派屬性標籤

請遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-8-manage-schema"></a>步驟 8：管理架構

請遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-9-manage-search-permissions"></a>步驟 9：管理搜尋許可權

- 針對檔案或專案層級存取控制，選取 **[僅限具有此資料來源存取權的人員]**。
- 選取 **[所有人** ] 可讓組織中的每個人查看此資料來源的搜尋結果。

:::image type="content" source="media/csv-connector/csv-connector-search-permissions.png" alt-text="只有已選取此資料來源存取權的人員可以進行搜尋許可權設定。" lightbox="media/csv-connector/csv-connector-search-permissions.png":::

## <a name="step-10-choose-refresh-settings"></a>步驟 10：選擇重新整理設定

請遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-11-review-connection"></a>步驟 11：檢閱連線

請遵循一般 [設定指示](./configure-connector.md)。

<!---## Limitations-->
## <a name="limitations"></a>限制

以下是 CSV 連接器的已知限制：
* 目前不支援設定檔擴充案例。
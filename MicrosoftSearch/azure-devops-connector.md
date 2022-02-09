---
title: Azure DevOps Graph 連接器 Microsoft 搜尋
ms.author: mecampos
author: mecampos
manager: umas
audience: Admin
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
description: 設定 Microsoft 搜尋的 Azure DevOps Graph 連接器
ms.openlocfilehash: 2eb7f3990b0daa2a64cab1e994b6f8089213645c
ms.sourcegitcommit: 2fc1bc29249d6342a10d85bca291a1bec8bc125c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2022
ms.locfileid: "62491905"
---
<!---Previous ms.author: shgrover --->

# <a name="azure-devops-graph-connector-preview"></a>Azure DevOps Graph 連接器 (預覽) 

Azure DevOps Graph 連接器可讓您的組織為其 Azure DevOps 服務實例中的工作專案編制索引。 從 Azure DevOps 設定連接器及索引內容之後，使用者就可以在 Microsoft 搜尋中搜尋這些專案。

> [!NOTE]
> 請閱讀 [**Graph 連接器**](configure-connector.md)文章的設定，以瞭解一般 Graph 連接器設定指示。

本文適用于設定、執行及監視 Azure DevOps Graph 連接器的任何人。 它會補充一般設定程式，並顯示只適用于 Azure DevOps Graph 連接器的指令。

>[!IMPORTANT]
>Azure DevOps 連接器只支援 Azure DevOps 雲端服務。 Azure DevOps Server 2019、tfs 2018、tfs 2017、tfs 2015 和 tfs 2013 都不受此連接器支援。

<!---## Before you get started-->
## <a name="before-you-get-started"></a>開始之前
您必須是組織之 M365 租使用者的系統管理員，以及組織 Azure DevOps 實例的管理員。

若要允許連接器連線到您的 Azure DevOps 組織，您必須透過 **OAuth 啟用協力廠商應用程式存取**。 請參閱 Azure DevOps 檔，以[管理安全性原則](/azure/devops/organizations/accounts/change-application-access-policies?view=azure-devops#manage-a-policy&preserve-view=true)以深入瞭解。

![透過 OAuth 的協力廠商應用程式存取](media/ado-workitems-connector-security-policies.png)

您必須將下列許可權授與在設定連接器時使用其認證的使用者帳戶：

| 許可權名稱 | 許可權類型 | 需要的 |
| ------------ | ------------ | ------------ |
| 查看專案層級資訊 | [Project 許可權](/azure/devops/organizations/security/permissions?view=azure-devops&tabs=preview-page#project-level-permissions&preserve-view=true) | 編目 Azure DevOps 的工作專案。 此許可權對於需要編制索引的專案是 **必要** 的。 |
| _View analytics_ | [Project 許可權](/azure/devops/organizations/security/permissions?view=azure-devops&tabs=preview-page#project-level-permissions&preserve-view=true) | 編目 Azure DevOps 的工作專案。 此許可權對於需要編制索引的專案是 **必要** 的。 |
| _查看此節點中的工作專案_ | [區域路徑](/azure/devops/organizations/security/permissions?view=azure-devops&tabs=preview-page#area-path-object-level&preserve-view=true) | 編目區域路徑中的工作專案。 這是 **選用** 的許可權。 只有那些區域路徑會進行編目，讓使用者帳戶具有許可權。 |

## <a name="step-1-add-a-graph-connector-in-the-microsoft-365-admin-center"></a>步驟1：在 Microsoft 365 系統管理中心中新增 Graph 連接器

遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup 
instructions.-->

## <a name="step-2-name-the-connection"></a>步驟2：命名連線

遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup 
instructions.-->

## <a name="step-3-configure-the-connection-settings"></a>步驟3：設定連接設定

若要連線至您的 Azure DevOps 實例，您需要 Azure DevOps[組織](/azure/devops/organizations/accounts/create-organization)名稱、其應用程式識別碼，以及 OAuth 驗證的用戶端密碼。

### <a name="register-an-app"></a>註冊應用程式

在 Azure DevOps 中註冊應用程式，讓 Microsoft 搜尋應用程式可以存取實例。 若要深入瞭解，請參閱 Azure DevOps 檔，瞭解如何[註冊應用程式](/azure/devops/integrate/get-started/authentication/oauth?preserve-view=true&view=azure-devops#register-your-app)。

下表提供如何填寫 [應用程式註冊] 表單的指導方針：

必要欄位 | 描述 | 建議值
--- | --- | ---
| 公司名稱         | 您公司的名稱。 | 使用適當的值   |
| 應用程式名稱     | 識別您要授權之應用程式的唯一值。    | Microsoft 搜尋     |
| 應用程式網站  | 在連接器設定期間要求存取 Azure DevOps 實例之應用程式的 URL。  (必要) 。  | HTTPs://<span>gc。</span>com
| 授權回撥 URL        | 授權伺服器重新導向所需的回撥 URL。 | HTTPs://<span>gc。</span>com/v 1.0/admin/oauth/callback|
| 授權範圍 | 應用程式的存取範圍 | 選取下列範圍： Identity (讀取) 、工作專案 (讀取) 、變數群組 (讀取) 、Project 和團隊 (讀取) ，Graph (讀取) ，分析 (讀取) |

>[!IMPORTANT]
>您為應用程式選取的授權範圍應與上述範圍完全相符。 如果您省略清單中的其中一個授權範圍，或新增其他範圍，則授權會失敗。

在註冊具有上述詳細資料的應用程式時，您會取得將用來設定連接器的 **應用程式識別碼** 和 **用戶端密碼** 。

>[!NOTE]
>若要撤銷對 Azure DevOps 所註冊之任何應用程式的存取權，請移至 Azure DevOps 實例右邊的 [使用者設定]。 選取 [設定檔]，然後選取側邊窗格的 [安全性] 區段中的 [授權]。 將游標移到授權的 OAuth 應用程式上，以查看應用程式詳細資料右下角的 [撤銷] 按鈕。

### <a name="connection-settings"></a>連接設定

使用 Azure DevOps 註冊 Microsoft 搜尋應用程式之後，即可完成 [連線設定] 步驟。 輸入您的組織名稱、應用程式識別碼和用戶端密碼。

![連接應用程式設定。](media/ADO_Connection_settings_2.png)

### <a name="configure-data-select-projects-and-fields"></a>設定資料：選取專案和欄位

您可以選擇建立整個組織或特定專案之索引的連線。

如果您選擇編制整個組織的索引，組織中所有專案中的專案將會獲得索引。 新專案和專案會在建立後的下一個編目期間編制索引。

如果您選擇個別專案，則只有那些專案中的工作專案將會編制索引。

> [!NOTE]
> 在授與專案的專案 _層級資訊_ 和 _view analytics_ 許可權之後，可將 Azure DevOps 專案編目。

![設定資料。](media/ADO_Configure_data.png)

接下來，選取您要連線索引及預覽這些欄位中資料的欄位，然後再繼續進行。

![選擇 [屬性]。](media/ADO_choose_properties.png)

## <a name="step-4-manage-search-permissions"></a>步驟4：管理搜尋許可權

Azure DevOps 連接器只支援可供  **存取此資料來源** 或 **所有人** 的使用者看到的搜尋許可權。 如果您選擇 [**只有可存取此資料來源的人員**]，則根據組織的使用者或群組的許可權，使用者或 Azure DevOps 中的 Project 或區域路徑層級，可存取的索引資料將會出現在搜尋結果中。 如果您選擇 [ **任何人**]，索引資料將會出現在所有使用者的搜尋結果中。

## <a name="step-5-assign-property-labels"></a>步驟5：指派屬性標籤

遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-6-manage-schema"></a>步驟6：管理架構

遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-7-choose-refresh-settings"></a>步驟7：選擇重新整理設定

Azure DevOps 連接器支援完整和累加編目的更新排程。
建議的排程為一小時用於增量編目，而一天則是完整編目。

## <a name="step-8-review-connection"></a>步驟8：檢查連線

遵循一般 [設定指示](./configure-connector.md)。

>[!TIP]
>**預設結果類型**
>* 在發佈連接器之後，Azure DevOps 連接器會自動註冊[結果類型](./customize-search-page.md#step-2-create-result-types)。 結果類型會根據在步驟3中選取的欄位，使用動態產生的 [結果版面](./customize-results-layout.md) 配置。 
>* 您可以流覽至 [Microsoft 365 系統管理中心](https://admin.microsoft.com)中的 [**結果類型**](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/resulttypes)來管理結果類型。 預設結果類型將命名為 " `ConnectionId` default"。 例如，如果您的連線識別碼為 `AzureDevOps` ，您的結果版面配置將會命名為： "AzureDevOpsDefault"
>* 此外，您也可以視需要選擇建立您自己的結果類型。

<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup 
instructions.-->

## <a name="troubleshooting"></a>正在疑難排解
在設定連接器時或在編目期間，發現下列常見錯誤及其可能的原因。

| 步驟 | 錯誤訊息 | 可能的原因 (s)  |
| ------------ | ------------ | ------------ |
| 連接設定 | `Invalid Credentials detected. Try signing in with a different account or check the permissions for your account` | 可能會停用 *OAuth 的協力廠商應用程式存取*。 遵循 [管理安全性原則](/azure/devops/organizations/accounts/change-application-access-policies?view=azure-devops#manage-a-policy&preserve-view=true) 以啟用 OAuth 的步驟。 |
| 連接設定 | `Bad state` 顯示 URL 的 OAuth 快顯視窗中的訊息說明 `error=InvalidScope` | 向登錄的應用程式提供錯誤範圍。 |
| 連接設定 | `400 - Bad request` OAuth 快顯視窗中的訊息 | 不正確的應用程式識別碼 |
| 連接設定 | `BadRequest: Bad Request on api request` OAuth 快顯視窗中的訊息 | 不正確的用戶端密碼 |
|  (後置後設定) 的編目時間 | `The account associated with the connector doesn't have permission to access the item.` | 已註冊的應用程式沒有任何必要的 OAuth 範圍。  (記事-已于8/31/2021 引進新的 OAuth 範圍需求 ' Analytics： read ')  |
|  (後置後設定) 的編目時間 | `You don't have permission to access this data source. You can contact the owner of this data source to request permission.` | 已停用 *OAuth 的協力廠商應用程式存取*。 遵循 [管理安全性原則](/azure/devops/organizations/accounts/change-application-access-policies?view=azure-devops#manage-a-policy&preserve-view=true) 以啟用 OAuth 的步驟。 |
|  (後置後設定) 的編目時間 | `Credentials associated with this data source have expired. Renew the credentials and then update the connection` | 註冊的應用程式可能已遭刪除或過期。 |

<!---## Limitations-->
<!---Insert limitations for this data source-->
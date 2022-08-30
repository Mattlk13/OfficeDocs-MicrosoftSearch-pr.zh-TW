---
title: 使用 Windows 搜尋尋找公司或學校結果
ms.author: dawholl
author: dawholl
manager: kellis
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
ms.assetid: f980b90f-95e2-4b66-8b21-69f601ff4b50
ROBOTS: NoIndex
description: 使用 Windows 搜尋從您的桌面尋找公司或學校檔案、網站、人員等等。
ms.openlocfilehash: 21383de3fa72014cb1fdd9d428de458806d5cbbf
ms.sourcegitcommit: 2032add1816919c2cbf6acf9fa7682e9ad36f859
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2022
ms.locfileid: "67461238"
---
# <a name="use-windows-search-to-find-work-or-school-results"></a>使用 Windows 搜尋尋找公司或學校結果

Windows 搜尋是桌面搜尋體驗，可協助使用者尋找相關結果。 當使用者從工作列搜尋時，他們會從下列專案取得結果：

- **您的組織**：使用公司或學校帳戶登入 Windows 搜尋時，使用者會看到 SharePoint、商務用 OneDrive、Microsoft Graph 和其他連線到 Microsoft Search 的資料來源的建議和結果。
- **Web**：使用者會從 Bing 取得相關的搜尋建議和結果。
- **裝置**：使用者可以在其電腦上找到本機檔案、設定和應用程式。
  
## <a name="microsoft-search-in-windows"></a>Windows 中的 Microsoft 搜尋

Windows Search 會將 Microsoft Search 結果帶入每部電腦。 只要開始在整合式 Windows 搜尋方塊中輸入，即可尋找組織的相關答案和結果，包括人員、書簽、位置、Q&As、檔案等等。

| Windows 11搜尋結果中的人員答案 | Windows 11搜尋結果中的書簽答案 |
| ------- | -------- |
| :::image type="content" alt-text="Microsoft Search 人員在 Windows Search 中回答的螢幕擷取畫面。" source="media/windows-search/windows-search-people-answer.png"::: | :::image type="content" alt-text="Windows 搜尋中 Microsoft Search 書簽答案的螢幕擷取畫面。" source="media/windows-search/windows-search-bookmark-answer.png"::: |

## <a name="prepare-for-microsoft-search-in-windows"></a>準備 Windows 中的 Microsoft Search

若要在 Windows 搜尋中提供公司或學校結果，必須符合一些需求：

- 使用 Windows 10 1809 版、組建 17763、RS5 2018 年 10 月更新或更新版本
- 已為您的組織開啟 Bing 中的 Microsoft Search
- 已啟用 Windows 中的 Web 搜尋
- 為公司或學校帳戶啟用雲端內容
- 連線到 Azure AD (公司或學校帳戶的 Windows 搜尋) 

> [!NOTE]
>當 Windows 搜尋連線到使用者的公司或學校帳戶時，您的組織標誌會出現在 Windows 搜尋中。 在 Windows 工作列上的搜尋方塊中顯示標誌的能力為預覽狀態。 若要確保您的使用者看到適當的商標，請在組織設定中確認您的標誌和主題。 若要深入瞭解，請參閱 [為您的組織自訂 Microsoft 365 主題](/microsoft-365/admin/setup/customize-your-organization-theme)。 只有全域系統管理員可以變更組織的主題或標誌。

### <a name="turn-on-microsoft-search-in-bing"></a>在 Bing 中開啟 Microsoft Search

對於大部分的組織，包括企業和教育，Bing 中的 Microsoft Search 預設為開啟。 若要在 Bing 中開啟 Microsoft Search，請移至Microsoft 365 系統管理中心中的 [設定[] 頁面。](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/configurations) 在 [Bing 中的 Microsoft 搜尋] 設定下，選擇 [ **變更** ]，然後選取 **[在您組織的 Bing 中啟用 Microsoft 搜尋]**。 此變更最多需要 24 小時才會生效。

如果此設定已關閉，使用者在 Windows 搜尋、Microsoft Edge 或 Bing 上搜尋時，將不會取得內部結果。 在 Bing 中關閉 Microsoft Search 並不會停止或防止內部內容新增至您的搜尋索引。 它只會停用 Microsoft Search 的這些進入點。

:::image type="content" alt-text="Microsoft 365 系統管理中心中 Bing 中 Microsoft Search 切換的螢幕擷取畫面。" source="media/windows-search/admin-center-microsoft-search-bing-setting.png" lightbox="media/windows-search/admin-center-microsoft-search-bing-setting.png":::

### <a name="enable-web-search-in-windows"></a>在 Windows 中啟用 Web 搜尋

如果本機裝置上已啟用 Web 搜尋，您應該會在 [Windows 搜尋] 方塊中看到 [Web] 索引標籤。

:::image type="content" alt-text="Windows 搜尋的螢幕擷取畫面，其中顯示 [Web] 索引標籤的圖說文字。" source="media/windows-search/windows-search-web-tab.png":::

如果在 Windows 中停用 Web 搜尋，您的使用者將不會看到組織的搜尋建議或結果。 若要允許公司或學校的建議和結果，請使用群組原則和登錄機碼啟用 Web 搜尋：

- 群組原則路徑和設定： ```Computer Configuration/Administrative Templates/Windows Components/Search/Don’t search the web or display web results in Search``` 此原則應設定為 [已停用]。 深入瞭解 [DoNotUseWebResults MDM 原則 CSP](/windows/client-management/mdm/policy-csp-search#search-donotusewebresults)。
- 登錄機碼路徑和設定： ```HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Search\BingSearchEnabled``` 此登錄機碼值應為 1。

### <a name="enable-cloud-content"></a>啟用雲端內容

如果您開啟雲端內容搜尋的 [公司或學校帳戶] 設定，Windows 搜尋會顯示來自 Microsoft Search 商務用 OneDrive、Outlook、SharePoint 等專案的結果。

:::image type="content" alt-text="雲端內容搜尋的 Windows 設定螢幕擷取畫面。" source="media/windows-search/windows-setting-cloud-content-search.png":::

您可以使用群組原則和登錄機碼來驗證是否已在本機裝置中啟用雲端內容搜尋許可權：

- 群組原則路徑和設定： ```Computer Configuration/Administrative Templates/Windows Components/Search/Allow Cloud Search``` 此原則應設定為 [已啟用]。 深入瞭解 [允許雲端搜尋 MDM 原則 CSP](/windows/client-management/mdm/policy-csp-search#search-allowcloudsearch)。
- 登錄機碼路徑和設定： ```HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\SearchSettings\IsAADCloudSearchEnabled``` 和 ```HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Windows SearchAllowCloudSearch``` 兩個登錄機碼值都應該是 1。

### <a name="connect-work-or-school-account-azure-ad-to-windows-search"></a>將公司或學校帳戶 (Azure AD) 連線到 Windows 搜尋服務

為了驗證使用者的身分識別，並判斷他們可以存取的資訊和檔案，Microsoft Search 會使用其公司或學校帳戶。 您的使用者可以遵循下列步驟，將 Windows 搜尋與其公司或學校帳戶連線：

1. 開啟 **[設定]** 應用程式。
2. 選 **取 [帳戶]**。
3. 選 **取 [存取公司或學校]**。
4. 檢查您的帳戶。 如果未列出，請選取 [ **連線]** 按鈕加以新增。
5. 使用您的公司或學校認證登入。
6. 遵循螢幕上的提示以完成連線。  
7. 完成時，您的帳戶將會新增為連線。 您將可存取您組織提供的搜尋建議、結果和其他資源。  

## <a name="search-highlights-in-windows"></a>Windows 中的搜尋醒目提示

[Windows 10](https://blogs.windows.com/windows-insider/2022/03/14/releasing-windows-10-build-19044-1618-to-release-preview-channel/)和[Windows 11 (Insider Preview 中的](https://blogs.windows.com/windows-insider/2022/03/09/announcing-windows-11-insider-preview-build-22572/)搜尋重點) 提供您組織的最新更新，以及建議的人員、檔案等等。 使用者可以流覽檔案，或流覽組織的人員圖表。 一如往常，使用者可以直接開始輸入來尋找與您組織相關的所有專案，只要使用搜尋即可。

:::image type="content" alt-text="Windows 搜尋醒目提示的螢幕擷取畫面，其中顯示組織結構。" source="media/windows-search/search-highlights-organization.png":::

### <a name="manage-search-highlights"></a>管理搜尋重點

使用者能夠顯示或隱藏搜尋醒目提示。 若要關閉或重新開啟，請以滑鼠右鍵按一下工作列，選取 [ **搜尋**]，然後選取或清除 **[顯示搜尋醒目提示]**。

Windows 和 Microsoft 365 IT 系統管理員也可以控制如何針對Windows 10和Windows 11受管理裝置設定工作列上的搜尋醒目提示。 深入瞭解 [允許搜尋醒目提示 MDM 原則 CSP](/windows/client-management/mdm/policy-csp-search#search-allowsearchhighlights)。

若要使用群組原則管理搜尋醒目提示，請移至原則設定 ```Computer Configuration/Administrative Templates/Windows Components/Search/Allow search highlights``` 。 使用 設定來停用或啟用搜尋醒目提示體驗。 如果您將設定保留為 **[未設定]**，則預設會啟用體驗。
Windows 10中支援的設定值：

- 啟用 (預設) 或未設定：啟用或未設定此設定會開啟工作列搜尋方塊和 Windows 搜尋首頁中的搜尋醒目提示。
- 停用：停用此設定會關閉工作列搜尋方塊和 Windows 搜尋首頁中的搜尋醒目提示。

Windows 11中支援的值：

- 啟用 (預設) 或未設定：啟用或未設定此設定會開啟 [開始] 功能表搜尋方塊和 Windows 搜尋首頁中的搜尋醒目提示。
- 停用：停用此設定會關閉 [開始] 功能表搜尋方塊和 Windows 搜尋首頁中的搜尋醒目提示。

若要存取搜尋重點的原則，請在具有 2022 年 3 月累積更新預覽版或 2022 年 4 月每月品質更新的裝置上，移至 **C：\Windows\PolicyDefinitions** 並找出 **Search.admx**。 如有需要，Microsoft 下載中心會有更新版本的系統管理[範本](https://www.microsoft.com/download/details.aspx?id=104042) (.admx) 和群組原則版本 20H2 Windows 10[設定參考](https://www.microsoft.com/download/details.aspx?id=104043)。 Microsoft 端點管理員提供相同的原則設定選項。

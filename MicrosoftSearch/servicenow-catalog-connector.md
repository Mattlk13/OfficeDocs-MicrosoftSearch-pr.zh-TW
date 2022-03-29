---
title: ServiceNow Microsoft 搜尋的目錄 Graph 連接器
ms.author: kam1
author: TheKarthikeyan
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
description: 設定 Microsoft 搜尋的 ServiceNow 目錄 Graph 連接器
ms.openlocfilehash: 8390487a1bf4fc489cee05c4edeacadebd17c31d
ms.sourcegitcommit: 214ff6bb8e22320b4ac45c5cddbe7c37b3df923b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2022
ms.locfileid: "64504034"
---
<!---Previous ms.author: kam1 --->

# <a name="servicenow-catalog-graph-connector"></a>ServiceNow 目錄 Graph 連接器

使用 Microsoft Graph Connector ServiceNow 時，您的組織可以[服務](https://www.servicenow.com/products/it-service-automation-applications/service-catalog.html)所有使用者都能看見的目錄專案，或以組織內的使用者準則許可權加以限制的目錄專案。 從 ServiceNow 設定連接器和索引內容之後，使用者可以從任何 Microsoft 搜尋用戶端搜尋這些目錄專案。

本文適用于 Microsoft 365 系統管理員或任何設定、執行及監視 ServiceNow 目錄 Graph 連接器的人員。 它會補充[設定 Graph 連接器](configure-connector.md)文章中提供的一般指示。 若尚未這麼做，請閱讀整個設定 Graph 連接器文章，以瞭解一般的設定程式。

安裝程式中的每個步驟都會列在下面，也就是指出應該遵循一般設定指示或僅適用于 ServiceNow Graph 連接器（包括[疑難排解](#troubleshooting)及[限制](#limitations)的相關資訊）的說明。

## <a name="step-1-add-a-graph-connector-in-the-microsoft-365-admin-center"></a>步驟1：在 Microsoft 365 系統管理中心中新增 Graph 連接器。
遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-2-name-the-connection"></a>步驟2：命名連線。
遵循一般 [設定指示](./configure-connector.md)。


## <a name="step-3-connection-settings"></a>步驟3：連接設定
若要連線至您的 ServiceNow 資料，您需要組織的 **ServiceNow 實例 URL**。 組織的 ServiceNow 實例 URL 一般會類似 **HTTPs:// &lt; 您的組織網域> service-now.com**。 

除了此 URL 之外，您還需要一個 **服務帳戶**，用以設定 ServiceNow 的連線，以及允許 Microsoft 搜尋定期更新以重新整理排程為基礎的目錄專案。 服務帳戶必須具有下列 **ServiceNow 表記錄** 的讀取權限，才可成功編目各種實體。

功能 | 讀取 access 所需的表格 | 描述
--- | --- | ---
索引目錄專案可供<em>所有人</em>使用 | sc_cat_item | 編目目錄專案
索引及支援使用者準則許可權 | sc_cat_item_user_criteria_mtom | 神秘可以存取此目錄專案
| | sc_cat_item_user_criteria_no_mtom | 神秘無法存取此目錄專案
| | sys_user | 讀取使用者表格
| | sys_user_has_role | 讀取使用者的角色資訊
| | sys_user_grmember | 使用者的讀取群組成員資格
| | user_criteria | 讀取使用者準則許可權

您可以為您用來連線 Microsoft 搜尋的服務帳戶 **建立並指派角色**。 [瞭解如何指派 ServiceNow 帳戶的角色](https://docs.servicenow.com/bundle/paris-platform-administration/page/administer/users-and-groups/task/t_AssignARoleToAUser.html)。 您可以在建立的角色上指派對表格的讀取權限。 若要瞭解如何設定表記錄的「讀取」存取權，請參閱 [保護資料表記錄](https://developer.servicenow.com/dev.do#!/learn/learning-plans/orlando/new_to_servicenow/app_store_learnv2_securingapps_orlando_creating_and_editing_access_controls)。 


>[!NOTE]
> ServiceNow catalog Graph Connector 可以索引目錄專案和使用者準則許可權，而不需要高級腳本。 如果使用者準則包含 advanced script，所有相關的目錄專案將會從搜尋結果中隱藏。

若要驗證及同步處理 ServiceNow 中的內容，請選擇下列 **其中一** 項支援的方法： 
 
- 基本驗證 
- ServiceNow OAuth (建議) 
- Azure AD OpenID 連線

## <a name="step-31-basic-authentication"></a>步驟3.1：基本驗證

輸入具有 **目錄** 角色的 ServiceNow 帳戶的使用者名稱和密碼，以驗證您的實例。

## <a name="step-32-servicenow-oauth"></a>步驟3.2： ServiceNow OAuth

若要使用 ServiceNow OAuth 進行驗證，ServiceNow 系統管理員必須布建 ServiceNow 實例中的端點，這樣 Microsoft 搜尋應用程式才能存取它。 若要深入瞭解，請參閱在 ServiceNow 檔中 [建立用戶端存取實例的端點](https://docs.servicenow.com/bundle/newyork-platform-administration/page/administer/security/task/t_CreateEndpointforExternalClients.html) 。

下表提供如何填寫端點建立表單的指導方針：

欄位 | 描述 | 建議值 
--- | --- | ---
名稱 | 識別您需要 OAuth 存取之應用程式的唯一值。 | Microsoft 搜尋
用戶端識別碼 | 應用程式的唯讀、自動產生的唯一識別碼。 當實例要求存取權杖時，會使用用戶端識別碼。 | NA
用戶端密碼 | 使用此共用的機密字串，ServiceNow 實例和 Microsoft 搜尋會授權彼此進行通訊。 | 遵循安全性最佳作法，將密碼當做密碼對待。
重新導向 URL | 授權伺服器重新導向所需的回撥 URL。 | https://gcs.office.com/v1.0/admin/oauth/callback
標誌 URL | 包含應用程式標誌之圖像的 URL。 | NA
作用中 | 選取此核取方塊，讓應用程式登錄成為使用中。 | 設定為 active
重新整理權杖生命週期 | 重新整理權杖有效的秒數。 根據預設，重新整理權杖會在100天內到期 (8640000 秒) 。 | 31536000 (1 年) 
存取權杖使用壽命 | 存取權杖有效的秒數。 | 43200 (12 小時) 

輸入用戶端識別碼和用戶端密碼以連接至您的實例。 連接後，請使用 ServiceNow 帳號憑證來驗證編目的許可權。 帳戶至少應具有 **目錄** 角色。 請參閱「 [步驟3：連線設定](#step-3-connection-settings) 」一開始的表格，以提供更多 ServiceNow 表記錄的讀取權，以及索引使用者準則許可權。

## <a name="step-33-azure-ad-openid-connect"></a>步驟3.3： Azure AD OpenID 連線

若要使用 Azure AD OpenID 連線進行驗證，請遵循下列步驟。

### <a name="step-331-register-a-new-application-in-azure-active-directory"></a>步驟3.3.1：在 Azure Active Directory 中註冊新的應用程式

若要瞭解如何在 Azure Active Directory 中註冊新的應用程式，請參閱[註冊應用程式](/azure/active-directory/develop/quickstart-register-app#register-an-application)。 選取 [單一承租人組織目錄]。 不需要重新導向 URI。 註冊後，請記下應用程式 (用戶端) ID 及目錄 (承租人) 識別碼。

### <a name="step-332-create-a-client-secret"></a>步驟3.3.2：建立用戶端密碼

若要瞭解如何建立用戶端密碼，請參閱 [建立用戶端密碼](/azure/active-directory/develop/quickstart-register-app#add-a-client-secret)。 記錄用戶端密碼。

### <a name="step-333-retrieve-service-principal-object-identifier"></a>步驟3.3.3：取回服務主體物件識別碼

遵循下列步驟以取得服務主體物件識別碼

1. 執行 PowerShell。

2. 使用下列命令安裝 Azure PowerShell。

   ```powershell
   Install-Module -Name Az -AllowClobber -Scope CurrentUser
   ```

3. 連線 Azure。

   ```powershell
   Connect-AzAccount
   ```

4. 取得服務主體物件識別碼。

   ```powershell
   Get-AzADServicePrincipal -ApplicationId "Application-ID"
   ```
   將 "Application ID" 取代為您在步驟3中所註冊應用程式的應用程式 (用戶端) ID (但不) 引號。 請注意，PowerShell 輸出中的 ID 物件的值。 這是服務主體識別碼。

現在，您已具備 Azure 入口網站所需的所有資訊。 下表提供資訊的快速摘要。

屬性 | 描述 
--- | ---
目錄識別碼 (租使用者識別碼)  | 步驟 3 Azure Active Directory 租使用者的唯一識別碼。
 (用戶端識別碼的應用程式識別碼)  | 在步驟3中註冊之應用程式的唯一識別碼。
用戶端密碼 | 從步驟 3 () 的應用程式的機密機碼。 請將它當作密碼對待。
服務主體識別碼 | 作為服務執行之應用程式的身分識別。 步驟 3 () 

### <a name="step-334-register-servicenow-application"></a>步驟3.3.4：註冊 ServiceNow 應用程式

ServiceNow 實例需要下列設定：

1. 註冊新的 OAuth OIDC 實體。 若要瞭解，請參閱 [Create a OAUTH OIDC provider](https://docs.servicenow.com/bundle/orlando-platform-administration/page/administer/security/task/add-OIDC-entity.html)。

2. 下表提供如何填寫 OIDC 提供者註冊表單的指導方針。

   欄位 | 描述 | 建議值
   --- | --- | ---
   名稱 | 識別 OAuth OIDC 實體的唯一名稱。 | Azure AD
   用戶端識別碼 | 在協力廠商 OAuth OIDC server 中註冊之應用程式的用戶端識別碼。 實例在要求存取權杖時使用用戶端識別碼。 | Application (Client) ID 從步驟3。
   用戶端密碼 | 在協力廠商 OAuth OIDC server 中註冊之應用程式的用戶端密碼。 | 步驟3的用戶端密碼。 b

   其他所有值都可以是預設值。

3. 在 OIDC 提供者註冊表單中，您必須新增新的 OIDC 提供者設定。 根據 *OAUTH OIDC 提供者* 設定] 欄位，選取要開啟 OIDC 設定記錄的搜尋圖示。 選取 [新增]。

4. 下表提供如何填寫 OIDC 提供者設定表單的指導方針

   欄位 | 建議值
   --- | ---
   OIDC 提供者 |  Azure AD
   OIDC 中繼資料 URL | URL 的格式必須為 HTTPs \: //login.microsoftonline.com/<tenandId ">/.well-known/openid-configuration <br/>以步驟3的目錄 (租使用者) 識別碼取代 "tenantID"。
   OIDC 設定快取壽命範圍 |  120
   應用程式 | 全域
   使用者宣告 | 子
   使用者欄位 | 使用者識別碼
   啟用 JTI 宣告驗證 | 停用

5. 選取 [提交並更新 OAuth OIDC 實體表單]。

### <a name="step-335-create-a-servicenow-account"></a>步驟3.3.5：建立 ServiceNow 帳戶

請參閱指示建立 ServiceNow 帳戶、 [在 ServiceNow 中建立使用者](https://docs.servicenow.com/bundle/paris-platform-administration/page/administer/users-and-groups/task/t_CreateAUser.html)。

下表提供如何填寫 ServiceNow 使用者帳戶註冊的指導方針。

欄位 | 建議值
--- | ---
使用者識別碼 | 步驟3中的服務主體識別碼。 c
僅 Web 服務存取權 | Checked

其他所有值都可以保留預設值。

### <a name="step-336-enable-catalog-role-for-the-servicenow-account"></a>步驟3.3.6：啟用 ServiceNow 帳戶的目錄角色

存取您用 ServiceNow 主體識別碼建立的 ServiceNow 帳戶做為使用者識別碼並指派目錄角色。 您可以在這裡找到將角色指派給 ServiceNow 帳戶的指示， [將角色指派給使用者](https://docs.servicenow.com/bundle/paris-platform-administration/page/administer/users-and-groups/task/t_AssignARoleToAUser.html)。 請參閱「 [步驟3：連線設定](#step-3-connection-settings) 」一開始的表格，以提供更多 ServiceNow 表記錄的讀取權，以及索引使用者準則許可權。

使用應用程式識別碼做為用戶端識別碼 (從步驟3。系統管理中心) 中的) 和用戶端密碼 (，以使用 ServiceNow Azure AD OpenID 來驗證您的連線實例。

## <a name="step-4-select-properties-and-filter-data"></a>步驟4：選取屬性和篩選資料

在這個步驟中，您可以從 ServiceNow 資料來源新增或移除可用屬性。 Microsoft 365 已經預設會選取一些屬性。

使用 ServiceNow 查詢字串，您可以指定同步處理文章的條件。 就像 **SQL Select** 語句中的 **Where** 子句。 例如，您可以選擇只為作用中的專案編制索引。 若要瞭解如何建立您自己的查詢字串，請參閱 [使用篩選產生編碼的查詢字串](https://docs.servicenow.com/bundle/rome-platform-user-interface/page/use/using-lists/task/t_GenEncodQueryStringFilter.html)。

使用 [預覽結果] 按鈕，檢查所選屬性和查詢篩選器的範例值。

## <a name="step-5-manage-search-permissions"></a>步驟5：管理搜尋許可權

ServiceNow 連接器支援 **所有人都** 可以看到的搜尋許可權，或是 **只有存取此資料來源的人員才能使用**。 已編制索引的資料會顯示在搜尋結果中，並可供組織中的所有使用者或可以透過使用者準則許可權存取的使用者看到。 如果未啟用具有使用者準則的目錄專案，它就會出現在組織中每個人的搜尋結果中。

ServiceNow Catalog Graph Connector 支援預設使用者條件許可權，但沒有高級腳本。 當連接器使用 advanced script 遇到使用者準則時，所有使用該使用者準則的資料都不會出現在搜尋結果中。

如果您只選擇可 **存取此資料來源的人員**，您需要進一步選擇是否 ServiceNow 實例具有 Azure Active Directory (AAD) 已布建的使用者或非 AAD 的使用者。

若要找出適合您組織的選項：

1. 如果 ServiceNow 使用者的電子郵件識別碼與) 中使用者的 UserPrincipalName (UPN AAD **相同**，請選擇 **AAD** 選項。
2. 如果 ServiceNow 使用者的電子郵件識別碼 **不同** 于) 中使用者的 UserPrincipalName (UPN AAD，請選擇 [**非 AAD** ] 選項。 

>[!NOTE]
> * 如果您選擇 AAD 做為身分識別來源的類型，連接器會將透過 ServiceNow 直接從取得之使用者的電子郵件 IDs，對應到 AAD 中的 UPN 屬性。
> * 如果您為身分識別類型選擇「非 AAD」，請參閱[對應您的非 Azure AD](map-non-aad.md)身分識別，以取得對應身分識別的指示。 您可以使用此選項，提供從電子郵件識別碼到 UPN 的對應正則運算式。

## <a name="step-6-assign-property-labels"></a>步驟6：指派屬性標籤

遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-7-manage-schema"></a>步驟7：管理架構

遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-8-choose-refresh-settings"></a>步驟8：選擇重新整理設定

遵循一般 [設定指示](./configure-connector.md)。

>[!NOTE]
>針對身分識別，只會套用已排程的完整編目。

## <a name="step-9-review-connection"></a>步驟9：檢查連線

遵循一般 [設定指示](./configure-connector.md)。

在發佈連線後，您必須自訂搜尋結果頁面。 若要瞭解如何自訂搜尋結果，請參閱 [自訂搜尋結果頁面](/microsoftsearch/configure-connector#next-steps-customize-the-search-results-page)。

## <a name="limitations"></a>限制
ServiceNow Catalog Graph connector 在其最新版本中有下列限制：

- *只有存取此資料來源功能的使用者才可* 在 [管理搜尋許可權] 底下執行 [僅限 [使用者準則](https://hi.service-now.com/kb_view.do?sysparm_article=KB0550924) ] 許可權。 任何其他類型的存取權限都不會套用到搜尋結果中。
- 不支援在目錄類別上設定的使用者準則許可權。 
- 目前的版本不支援具有高級腳本的使用者準則。 任何具有這種存取限制的目錄專案都會以「拒絕所有人」存取的方式編制索引，也就是說，除非我們支援，否則這些專案不會出現在搜尋結果中。

## <a name="troubleshooting"></a>疑難排解
在發佈連線後，自訂 [結果] 頁面，您可以在系統 [管理中心](https://admin.microsoft.com)的 [**資料來源**] 索引標籤底下查看狀態。 若要瞭解如何進行更新和刪除，請參閱 [管理您的連接器](manage-connector.md)。
您可以在下面找到常見問題的疑難排解步驟。
### <a name="1-unable-to-log-in-due-to-single-sign-on-enabled-servicenow-instance"></a>1. 因單一 Sign-On 啟用 ServiceNow 實例而無法登入

如果您的組織已啟用單一 Sign-On (SSO) ServiceNow，您可能無法使用服務帳戶進行記錄。 您可以新增<em> `login.do` </em>至 ServiceNow 實例 URL，以開啟使用者名稱和密碼基礎的登入。 例子。 `https://<your-organization-domain>.service-now.com./login.do` 

### <a name="2-unauthorized-or-forbidden-response-to-api-request"></a>2. API 要求的未授權或已禁止回應

#### <a name="21-check-table-access-permissions"></a>2.1。 檢查表存取許可權
如果您在線上狀態中看到禁止回應或未經授權的回應，請檢查服務帳戶是否需要存取 [步驟3：連線設定](#step-3-connection-settings)中所述的資料表。 請檢查表格中的所有資料行是否都有讀取權。

#### <a name="22-change-in-account-password"></a>2.2。 變更帳戶密碼
Graph 連接器會使用代表服務帳戶取得的存取權杖，以進行編目。 存取權杖每12小時會更新一次。 確定服務帳戶密碼在發佈連線之後未變更。 如果密碼變更，您可能需要重新驗證連線。

#### <a name="23-check-if-servicenow-instance-behind-firewall"></a>2.3。 檢查防火牆背後 ServiceNow 實例是否
Graph 連接器可能無法到達網路防火牆之後的 ServiceNow 實例。 您將需要明確允許存取 Graph Connector service。 您可以在下表中找到 Graph 連接器服務的公用 IP 位址範圍。 根據您的租使用者區域，將其新增至您的 ServiceNow 實例網路允許清單。

 環境 | 區域 | 範圍
--- | --- | ---
促使 | 北美 | 52.250.92.252/30、52.224.250.216/30
促使 | 歐洲 | 20.54.41.208/30、51.105.159.88/30 
促使 | 亞太地區 | 52.139.188.212/30、20.43.146.44/30 

#### <a name="24-access-permissions-not-working-as-expected"></a>2.4。 存取權未如預期般運作
如果您觀察套用至搜尋結果的存取權限中的差異，請確認使用者準則設定 [將使用者準則套用至目錄專案](https://docs.servicenow.com/bundle/orlando-it-service-management/page/product/service-catalog-management/task/t_AppUserCritItemsCat.html)。

### <a name="3-issues-with-only-people-with-access-to-this-data-source-permission"></a>3. *只有存取此資料來源許可權的人員才* 會發生問題

#### <a name="31-unable-to-choose-only-people-with-access-to-this-data-source"></a>3.1 無法自行選擇 *存取此資料來源的人員*

如果服務帳戶對「[步驟3：連線設定](#step-3-connection-settings)」中的必要資料表沒有讀取權限，您可能無法選擇 [*只有存取此資料來源的人員*] 選項。 檢查服務帳戶是否可以讀取 *索引及支援使用者準則許可權* 功能下所述的表格。

#### <a name="32-user-mapping-failures"></a>3.2 使用者對應失敗

 ServiceNow Azure Active Directory 中沒有 M365 使用者的使用者帳戶不會對應。 非使用者，服務帳戶應該會失敗使用者對應。 在 [連線詳細資料] 視窗的 [身分識別狀態] 區域中，可以存取使用者對應失敗的數目。 失敗使用者對應的記錄可從 [錯誤] 索引標籤下載。

### <a name="4-issues-with-user-criteria-access-flow"></a>4. 使用者準則存取流程的問題

如果您在 ServiceNow 和 Microsoft 搜尋之間看到使用者準則驗證的差異，請將系統屬性設定 `glide.knowman.block_access_with_no_user_criteria` 為 `no` 。

如果您有任何其他問題，或想要提供意見反應，請寫信給我們 [aka.ms/TalkToGraphConnectors](https://aka.ms/TalkToGraphConnectors)

---
title: Microsoft 搜尋的 ServiceNow 知識 Graph 連接器
ms.author: kam1
author: TheKarthikeyan
manager: harshkum
audience: Admin
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
description: 設定 Microsoft 搜尋的 ServiceNow 知識 Graph 連接器
ms.openlocfilehash: 1b76523cb5a76a3e28b9d16e99cd6c2b17be9adb
ms.sourcegitcommit: 205f2b9c7ba9ea2371088c5e978afdf7752ef92f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/25/2022
ms.locfileid: "64464848"
---
<!---Previous ms.author: kam1 --->


# <a name="servicenow-knowledge-graph-connector"></a>ServiceNow 知識 Graph 連接器

透過使用 Microsoft Graph Connector ServiceNow，您的組織可以為您組織內的使用者準則許可權，編制對所有使用者可見或限制的知識庫文章的索引。 從 ServiceNow 設定連接器和索引內容之後，使用者可以從任何 Microsoft 搜尋用戶端搜尋這些文章。  

您也可以參考[這段影片](https://www.youtube.com/watch?v=TVSkJpk1RiE)，深入瞭解 Graph 連接器在管理搜尋許可權中的功能。

本文適用于 Microsoft 365 系統管理員或任何設定、執行及監視 ServiceNow 知識 Graph 連接器的人員。 它會補充[設定 Graph 連接器](configure-connector.md)文章中提供的一般指示。 若尚未這麼做，請閱讀整個設定 Graph 連接器文章，以瞭解一般的設定程式。

安裝程式中的每個步驟都會列在下面，也就是指出應該遵循一般設定指示或僅適用于 ServiceNow Graph 連接器（包括[疑難排解](#troubleshooting)及[限制](#limitations)的相關資訊）的說明。  

## <a name="step-1-add-a-graph-connector-in-the-microsoft-365-admin-center"></a>步驟1：在 Microsoft 365 系統管理中心中新增 Graph 連接器。
遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-2-name-the-connection"></a>步驟2：命名連線。
遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-3-connection-settings"></a>步驟3：連接設定
若要連線至您的 ServiceNow 資料，您需要組織的 **ServiceNow 實例 URL**。 組織的 ServiceNow 實例 URL 一般會類似 **HTTPs:// &lt; 您的組織網域> service-now.com**。 

除了此 URL 之外，您還需要一個 **服務帳戶**，用以設定 ServiceNow 的連線，以及允許 Microsoft 搜尋定期更新以重新整理排程為基礎的知識文章。 服務帳戶必須具有下列 **ServiceNow 表記錄** 的讀取權限，才可成功編目各種實體。

**功能** | **讀取 access 所需的表格** | **描述**
--- | --- | ---
可供<em>所有人</em>使用的索引知識文章 | kb_knowledge | 編目知識文章
索引及支援使用者準則許可權 | kb_uc_can_read_mtom | 神秘可以讀取此知識庫
| | kb_uc_can_contribute_mtom | 神秘可對此知識庫做貢獻
| | kb_uc_cannot_read_mtom | 神秘無法讀取此知識庫
| | kb_uc_cannot_contribute_mtom | 神秘無法參與此知識庫
| | sys_user | 讀取使用者表格
| | sys_user_has_role | 讀取使用者的角色資訊
| | sys_user_grmember | 使用者的讀取群組成員資格
| | user_criteria | 讀取使用者準則許可權
| | kb_knowledge_base | 閱讀知識文庫資訊
索引擴充表格屬性 (選用)  | sys_db_object | 讀取擴充表格詳細資料
| | sys_dictionary | 讀取擴充表格屬性

您可以為您用來連線 Microsoft 搜尋的服務帳戶 **建立並指派角色**。 [瞭解如何指派 ServiceNow 帳戶的角色](https://docs.servicenow.com/bundle/paris-platform-administration/page/administer/users-and-groups/task/t_AssignARoleToAUser.html)。 您可以在建立的角色上指派對表格的讀取權限。 若要瞭解如何設定表記錄的「讀取」存取權，請參閱 [保護資料表記錄](https://developer.servicenow.com/dev.do#!/learn/learning-plans/orlando/new_to_servicenow/app_store_learnv2_securingapps_orlando_creating_and_editing_access_controls)。 

若要從 *kb_knowledge* 的 [擴充表格](https://docs.servicenow.com/bundle/rome-platform-administration/page/administer/table-administration/concept/table-extension-and-classes.html_)中索引屬性，請提供 sys_dictionary 和 sys_db_object 的讀取權限。 這是選用的功能。 您可以編制索引 *kb_knowledge* 資料表屬性，但不能存取其他兩個數據表。


>[!NOTE]
> ServiceNow Graph 連接器可以索引不含高級腳本的知識文章和使用者準則許可權。 如果使用者準則包含 advanced script，所有相關的知識文章都會從搜尋結果中隱藏。

若要驗證及同步處理 ServiceNow 中的內容，請選擇下列 **其中一** 項支援的方法： 
 
- 基本驗證 
- ServiceNow OAuth (建議) 
- Azure AD OpenID 連線

## <a name="step-31-basic-authentication"></a>步驟3.1：基本驗證

輸入具有 **知識** 角色的 ServiceNow 帳戶的使用者名稱和密碼，以向您的實例驗證。

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
重新整理權杖生命週期 | 重新整理權杖有效的秒數。 根據預設，重新整理權杖會在100天內到期 (8640000 秒) 。 | 31536000 (一年) 
存取權杖使用壽命 | 存取權杖有效的秒數。 | 43200 (12 小時) 

輸入用戶端識別碼和用戶端密碼以連接至您的實例。 連接後，請使用 ServiceNow 帳號憑證來驗證編目的許可權。 帳戶至少應具備 **知識** 角色。 請參閱「 [步驟3：連線設定](#step-3-connection-settings) 」一開始的表格，以提供更多 ServiceNow 表記錄的讀取權，以及索引使用者準則許可權。

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

### <a name="step-336-enable-knowledge-role-for-the-servicenow-account"></a>步驟3.3.6：啟用 ServiceNow 帳戶的知識角色

存取您用 ServiceNow 主體識別碼建立的 ServiceNow 帳戶做為使用者識別碼並指派知識角色。 您可以在這裡找到將角色指派給 ServiceNow 帳戶的指示， [將角色指派給使用者](https://docs.servicenow.com/bundle/paris-platform-administration/page/administer/users-and-groups/task/t_AssignARoleToAUser.html)。 請參閱「 [步驟3：連線設定](#step-3-connection-settings) 」一開始的表格，以提供更多 ServiceNow 表記錄的讀取權，以及索引使用者準則許可權。

使用應用程式識別碼做為用戶端識別碼 (從步驟3。系統管理中心) 中的) 和用戶端密碼 (，以使用 ServiceNow Azure AD OpenID 來驗證您的連線實例。

## <a name="step-4-select-properties-and-filter-data"></a>步驟4：選取屬性和篩選資料

在這個步驟中，您可以從 ServiceNow 資料來源新增或移除可用屬性。 Microsoft 365 已經預設會選取一些屬性。

使用 ServiceNow 查詢字串，您可以指定同步處理文章的條件。 就像 **SQL Select** 語句中的 **Where** 子句。 例如，您可以選擇只為發佈和使用中的文章編制索引。 若要瞭解如何建立您自己的查詢字串，請參閱 [使用篩選產生編碼的查詢字串](https://docs.servicenow.com/bundle/paris-platform-user-interface/page/use/using-lists/task/t_GenEncodQueryStringFilter.html)。

使用 [預覽結果] 按鈕，檢查所選屬性和查詢篩選器的範例值。

## <a name="step-5-manage-search-permissions"></a>步驟5：管理搜尋許可權

ServiceNow 連接器支援 **所有人都** 可以看到的搜尋許可權，或是 **只有存取此資料來源的人員才能使用**。 已編制索引的資料會顯示在搜尋結果中，並可供組織中的所有使用者或可以透過使用者準則許可權存取的使用者看到。 如果沒有啟用使用者準則的知識文章，它就會出現在組織中每個人的搜尋結果中。

ServiceNow Graph 連接器支援不含高級腳本的預設使用者準則許可權。 當連接器使用 advanced script 遇到使用者準則時，所有使用該使用者準則的資料都不會出現在搜尋結果中。

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
ServiceNow 知識 Graph 連接器在其最新版本中有下列限制：

- *只有存取此資料來源功能的使用者才可* 在 [管理搜尋許可權] 底下執行 [僅限 [使用者準則](https://hi.service-now.com/kb_view.do?sysparm_article=KB0550924) ] 許可權。 任何其他類型的存取權限都不會套用到搜尋結果中。
- 目前的版本不支援具有高級腳本的使用者準則。 任何具有這類訪問限制的知識文章，都將會以「拒絕所有人」存取權來編制索引，也就是說，直到我們支援它們時，才會顯示在搜尋結果中。

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

**環境** | **地區** | **Range**
--- | --- | ---
促使 | 北美 | 52.250.92.252/30、52.224.250.216/30
促使 | 歐洲 | 20.54.41.208/30、51.105.159.88/30 
促使 | 亞太地區 | 52.139.188.212/30、20.43.146.44/30 

#### <a name="24-access-permissions-not-working-as-expected"></a>2.4。 存取權未如預期般運作

如果您觀察套用至搜尋結果的存取權限中的差異，請在 [管理知識庫和文章存取](https://docs.servicenow.com/bundle/rome-servicenow-platform/page/product/knowledge-management/concept/user-access-knowledge.html)中的使用者準則中驗證 access 流程圖表。

### <a name="3-change-the-url-of-the-knowledge-article-to-view-it-in-the-support-portal"></a>3. 變更知識文章的 URL，以在支援入口網站中進行查看

ServiceNow 知識 Graph 連接器會使用格式中的 `<instance_url>/kb_view.do?sys_kb_id<sysId>` sys_id 計算 AccessUrl 屬性。 它會在後端系統檢視中開啟知識文章。 如果您想要將文章重新導向至不同的 URL，請遵循下列指示。
#### <a name="31-edit-your-result-type"></a>3.1 編輯您的結果類型
在 [自訂] 索引標籤 Microsoft 365 系統管理中心的「*搜尋 & 情報*」區段中，流覽以編輯為您的 ServiceNow 知識連線設定的結果類型。
![編輯結果類型](media/servicenow-knowledge-connector/edit-result-type.png)

在 [編輯結果類型] 對話方塊開啟時，按一下 [結果版面配置] 區段旁邊的 [ **編輯** ]。 
![編輯結果版面配置](media/servicenow-knowledge-connector/edit-result-type-2.png)

#### <a name="32-find-the-items-block"></a>3.2 找出專案區塊
尋找包含 text 屬性 `shortDescription` 及 `AccessUrl` values 的 items 區塊。

![編輯結果類型中的專案區塊](media/servicenow-knowledge-connector/edit-result-type-3.png)

#### <a name="33-edit-accessurl-property"></a>3.3 編輯 AccessUrl 屬性

若要變更目的地 URL，請編輯 `AccessUrl` 專案區塊中的 text 屬性部分。 例如，如果 ServiceNow 知識庫文章應重新導向至 `https://contoso.service-now.com/sp` 服務 URL 入口前置詞所在的位置 `sp` ，請遵循下列步驟。

**原始值** | **新值**
--- | ---
`"[{shortdescription}]({AccessUrl})"` | `"[{shortdescription}](https://contoso.service-now.com/sp?id=kb_article_view&sysparm_article={number})"`

這裡 `number` 是知識文章編號屬性。 在建立連線期間，應將其標記為 [管理架構] 畫面中的 [已 *檢索* ]。

完成檢查您的結果類型更新及命中 **提交**。 請一兩分鐘，以拿出所做的變更。 您的搜尋結果現在應該會重新導向至所需的 URLs。

### <a name="4-issues-with-only-people-with-access-to-this-data-source-permission"></a>4. *只有存取此資料來源許可權的人員才* 會發生問題

#### <a name="41-unable-to-choose-only-people-with-access-to-this-data-source"></a>4.1 無法自行選擇 *存取此資料來源的人員*

如果服務帳戶在 [步驟3：連線設定](#step-3-connection-settings)中沒有必要表格的「讀取」許可權，您可能無法選擇 [*只有存取此資料來源的人員*] 選項。 檢查服務帳戶是否可以讀取 *索引及支援使用者準則許可權* 功能下所述的表格。

#### <a name="42-user-mapping-failures"></a>4.2 使用者對應失敗

 ServiceNow Azure Active Directory 中沒有 M365 使用者的使用者帳戶不會對應。 非使用者，服務帳戶應該會失敗使用者對應。 在 [連線詳細資料] 視窗的 [身分識別狀態] 區域中，可以存取使用者對應失敗的數目。 失敗使用者對應的記錄可從 [錯誤] 索引標籤下載。

### <a name="5-issues-with-user-criteria-access-flow"></a>5. 使用者準則訪問流程的問題

如果您在 ServiceNow 和 Microsoft 搜尋之間看到使用者準則驗證的差異，請將系統屬性設定 `glide.knowman.block_access_with_no_user_criteria` 為 `no` 。

如果您有任何其他問題，或想要提供意見反應，請寫信給我們 [aka.ms/TalkToGraphConnectors](https://aka.ms/TalkToGraphConnectors)

---
title: ServiceNow Tickets Microsoft Graph 連接器
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
description: 設定 Microsoft Search 的 ServiceNow Tickets Graph 連接器
ms.openlocfilehash: deed45d94a41647f5523ea2495e72730d0f721d3
ms.sourcegitcommit: 21391072f80fece9b421c89787812cdaa84324f1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2022
ms.locfileid: "66889646"
---
<!---Previous ms.author: kam1 --->

# <a name="servicenow-tickets-microsoft-graph-connector-preview"></a>ServiceNow Tickets Microsoft Graph 連接器 (Preview) 

使用 ServiceNow Tickets 的 Microsoft Graph 連接器，您的組織可以為使用者提供各種票證的索引。 從 ServiceNow 設定連接器和索引內容之後，使用者可以從任何 Microsoft Search 用戶端搜尋這些票證。  

>[!NOTE]
>ServiceNow Tickets 連接器處於預覽狀態。 如果您想要搶先存取以試用，請使用 [<b> 此表單 </b>](https://forms.office.com/r/JniPmK5bzm)註冊。

本文適用于 Microsoft 365 系統管理員或設定、執行及監視 ServiceNow Tickets Graph 連接器的任何人。 它補充Microsoft 365 系統管理中心文章[中設定 Microsoft Graph 連接器中](configure-connector.md)提供的一般指示。 如果您尚未這麼做，請閱讀整個設定 Graph 連接器一文，以瞭解一般設定程式。

安裝程式中的每個步驟都列在下方，並附上一個附注，指出您應該遵循一般設定指示或僅適用于 ServiceNow 連接器的其他指示，包括 [疑難排解](#troubleshooting) 和 [限制的相關](#limitations)資訊。  

## <a name="step-1-add-a-connector-in-the-microsoft-365-admin-center"></a>步驟 1：在Microsoft 365 系統管理中心中新增連接器。
請遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-2-name-the-connection"></a>步驟 2：為連線命名。
請遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-3-connection-settings"></a>步驟 3：連線設定
若要連線到您的 ServiceNow 資料，您需要組織的 **ServiceNow 實例 URL**。 貴組織的 ServiceNow 實例 URL 通常看起來像 **您 HTTPs:// &lt; 組織網域>.service-now.com**。 

除了此 URL，您還需要服務 **帳戶** 來設定 ServiceNow 的連線，並允許 Microsoft Search 根據重新整理排程定期更新票證詳細資料。 

在 ServiceNow 中，工作資料表是票證管理的基類。 您可以擴充它來建立票證應用程式，例如事件、問題和變更管理。 深入瞭解 [ServiceNow 工作資料表](https://docs.servicenow.com/en-US/bundle/sandiego-platform-administration/page/administer/task-table/concept/c_TaskTable.html)。

您用來設定連線的服務帳戶 **必須具有** 下列 ServiceNow 資料表記錄的讀取權限，才能成功編目預設票證欄位。

**功能** | **讀取存取必要資料表** | **描述**
--- | --- | ---
索引基 [底任務資料表欄位](https://docs.servicenow.com/bundle/sandiego-platform-administration/page/administer/task-table/reference/r_ImportantTaskTableFields.html#r_ImportantTaskTableFields) | `task` | 若要從現用的工作資料表編目預設欄位
同步使用者資料表 | `sys_user` | 為票證的使用者存取詳細資料編制索引


如果您想要從 *工作* 資料 [表的擴充資料表](https://docs.servicenow.com/en-US/bundle/sandiego-platform-administration/page/administer/table-administration/concept/table-extension-and-classes.html)編制自訂屬性的索引，請提供sys_dictionary和sys_db_object的讀取權限。 這是 **選擇性** 功能。 您將能夠編制 *工作* 資料表屬性的索引，而不需要存取兩個額外的資料表。

**功能** | **讀取存取必要資料表** | **描述**
--- | --- | ---
從您的組織選取自訂資料表| `sys_db_object` | 尋找包含自訂資料表的擴充工作資料表清單
從特定<table_name>編制自訂欄位的索引 | `sys_dictionary` | 從事件、問題或change_management等特定資料表編目自訂欄位

您可以為用來與 Microsoft Search 連線 **的服務帳戶建立並指派角色** 。 [瞭解如何指派 ServiceNow 帳戶的角色](https://docs.servicenow.com/en-US/bundle/sandiego-platform-administration/page/administer/users-and-groups/task/t_AssignARoleToAUser.html)。 資料表的讀取權限可以提供給已建立的角色。 若要瞭解如何設定資料表記錄的讀取權限，請參閱 [保護資料表記錄](https://developer.servicenow.com/dev.do#!/learn/learning-plans/sandiego/new_to_servicenow/app_store_learnv2_securingapps_sandiego_securing_table_records)。 


若要從 ServiceNow 驗證和同步處理內容，請選擇 **三種支援的方法之一** ：

- 基本驗證
- ServiceNow OAuth (建議) 
- Azure AD OpenID Connect

## <a name="step-31-basic-authentication"></a>步驟 3.1：基本驗證

輸入 ServiceNow 帳戶的使用者名稱和密碼，以讀取 `task` 和 `sys_user` 資料表來向您的實例進行驗證。

## <a name="step-32-servicenow-oauth"></a>步驟 3.2：ServiceNow OAuth

若要使用 ServiceNow OAuth，ServiceNow 系統管理員必須在 ServiceNow 實例中布建端點。 之後，Microsoft Search 應用程式將能夠存取它。 若要深入瞭解，請參閱 ServiceNow 檔中的 [建立端點供客戶](https://docs.servicenow.com/en-US/bundle/sandiego-platform-administration/page/administer/security/task/t_CreateEndpointforExternalClients.html) 端存取實例。

下表提供如何填寫端點建立表單的指引：

欄位 | 描述 | 建議值
--- | --- | ---
名稱 | 唯一值，識別您需要 OAuth 存取權的應用程式。 | Microsoft 搜尋
用戶端識別碼 | 應用程式的唯讀、自動產生的唯一識別碼。 實例會在要求存取權杖時使用用戶端識別碼。 | NA
用戶端密碼 | 使用這個共用的秘密字串，ServiceNow 實例和 Microsoft Search 會互相授權通訊。 | 請將秘密視為密碼，以遵循安全性最佳做法。
重新導向 URL | 授權伺服器重新導向的必要回呼 URL。 | `https://gcs.office.com/v1.0/admin/oauth/callback`
標誌 URL | 包含應用程式標誌影像的 URL。 | NA
作用中 | 選取核取方塊，讓應用程式登錄成為使用中狀態。 | 設定為使用中
重新整理權杖生命週期 | 重新整理權杖有效的秒數。 根據預設，重新整理權杖會在) 8，640，000 秒 (100 天后過期。 | 31，536，000 (一年) 
存取權杖存留期 | 存取權杖有效的秒數。 | 43，200 (12 小時) 

輸入用戶端識別碼和用戶端密碼以連線到您的實例。 連線之後，請使用 ServiceNow 帳號憑證來驗證編目許可權。 帳戶至少應具有 和 `sys_user` 資料表的 `task` 讀取權限。 請參閱 [步驟 3：連線設定](#step-3-connection-settings) 開頭的資料表，以提供更多 ServiceNow 資料表記錄的讀取權限，以及索引使用者準則許可權。

## <a name="step-33-azure-ad-openid-connect"></a>步驟 3.3：Azure AD OpenID Connect

若要使用 Azure AD OpenID Connect 進行驗證，請遵循下列步驟。

### <a name="step-331-register-a-new-application-in-azure-active-directory"></a>步驟 3.3.1：在 Azure Active Directory 中註冊新的應用程式

若要瞭解如何在 Azure Active Directory 中註冊新的應用程式，請參閱 [註冊應用程式](/azure/active-directory/develop/quickstart-register-app#register-an-application)。 選取單一租使用者組織目錄。 不需要重新導向 URI。 註冊之後，記下應用程式 (用戶端) 識別碼和目錄識別碼 (租使用者識別碼) 。

### <a name="step-332-create-a-client-secret"></a>步驟 3.3.2：建立用戶端密碼

若要瞭解如何建立用戶端密碼，請參閱 [建立用戶端密碼](/azure/active-directory/develop/quickstart-register-app#add-a-client-secret)。 記下用戶端密碼。

### <a name="step-333-retrieve-service-principal-object-identifier"></a>步驟 3.3.3：擷取服務主體物件識別碼

請遵循步驟來擷取服務主體物件識別碼

1. 執行 PowerShell。

2. 使用下列命令安裝 Azure PowerShell。

   ```powershell
   Install-Module -Name Az -AllowClobber -Scope CurrentUser
   ```

3. 連線到 Azure。

   ```powershell
   Connect-AzAccount
   ```

4. 取得服務主體物件識別碼。

   ```powershell
   Get-AzADServicePrincipal -ApplicationId "Application-ID"
   ```
   將 「Application-ID」 取代為應用程式 (用戶端) 識別碼， (不含您在步驟 3.a 中註冊之應用程式的引號) 。 請注意 PowerShell 輸出中 ID 物件的值。 這是服務主體識別碼。

現在您已擁有Azure 入口網站所需的所有資訊。 下表提供資訊的快速摘要。

屬性	 | 描述
--- | ---
租使用者識別碼 (目錄識別碼)  | 步驟 3.a 中 Azure Active Directory 租使用者的唯一識別碼。
應用程式識別碼 (用戶端識別碼)  | 步驟 3.a 中註冊之應用程式的唯一識別碼。
用戶端密碼 | 從步驟 3.b)  (應用程式的秘密金鑰。 將其視為密碼。
服務主體識別碼 | 作為服務執行之應用程式的身分識別。 從步驟 3.c)  (

### <a name="step-334-register-servicenow-application"></a>步驟 3.3.4：註冊 ServiceNow 應用程式

ServiceNow 實例需要下列設定：

1. 註冊新的 OAuth OIDC 實體。 若要瞭解，請 [參閱建立 OAuth OIDC 提供者](https://docs.servicenow.com/en-US/bundle/sandiego-platform-administration/page/administer/security/task/add-OIDC-entity.html)。

2. 下表提供如何填寫 OIDC 提供者註冊表單的指引

   欄位 | 描述 | 建議值
   --- | --- | ---
   名稱 | 識別 OAuth OIDC 實體的唯一名稱。 | Azure AD
   用戶端識別碼 | 在協力廠商 OAuth OIDC 伺服器中註冊之應用程式的用戶端識別碼。 實例會在要求存取權杖時使用用戶端識別碼。 | 步驟 3.a 中的應用程式 (用戶端) 識別碼
   用戶端密碼 | 在協力廠商 OAuth OIDC 伺服器中註冊之應用程式的用戶端密碼。 | 步驟 3.b 中的用戶端密碼

   所有其他值都可以是預設值。

3. 在 OIDC 提供者註冊表單中，您需要新增 OIDC 提供者設定。 針對 *[OAuth OIDC 提供者* 設定] 欄位選取搜尋圖示，以開啟 OIDC 設定的記錄。 選取 [新增]。

4. 下表提供如何填寫 OIDC 提供者組態表單的指引

   欄位 | 建議值
   --- | ---
   OIDC 提供者 |  Azure AD
   OIDC 中繼資料 URL | URL 的格式必須是 HTTPs \: //login.microsoftonline.com/<tenandId「>/.well-known/openid-configuration <br/>將 「tenantID」 取代為步驟 3.a (租使用者識別碼) 的目錄識別碼。
   OIDC 組態快取生命週期 |  120
   應用程式 | 全域
   使用者宣告 | 子
   使用者欄位 | 使用者識別碼
   啟用 JTI 宣告驗證 | 已停用

5. 選取 [提交] 並更新 [OAuth OIDC 實體] 表單。

### <a name="step-335-create-a-servicenow-account"></a>步驟 3.3.5：建立 ServiceNow 帳戶

請參閱建立 ServiceNow 帳戶、 [在 ServiceNow 中建立使用者的](https://docs.servicenow.com/en-US/bundle/sandiego-platform-administration/page/administer/users-and-groups/task/t_CreateAUser.html)指示。

下表提供如何填寫 ServiceNow 使用者帳戶註冊的指引

欄位 | 建議值
--- | ---
使用者識別碼 | 步驟 3.c 的服務主體識別碼
僅限 Web 服務存取 | Checked

所有其他值都可以保留為預設值。

### <a name="step-336-enable-task-user-table-access-for-the-servicenow-account"></a>步驟 3.3.6：啟用 ServiceNow 帳戶的工作、使用者資料表存取

存取您以 ServiceNow 主體識別碼作為使用者識別碼建立的 ServiceNow 帳戶，並將讀取權限指派給 `task` 和 資料 `sys_user` 表。 請參閱 [步驟 3：連線設定](#step-3-connection-settings) 開頭的資料表，以提供更多 ServiceNow 資料表記錄和索引自訂欄位的讀取權限。

使用步驟 3.a) 中的應用程式識別碼作為用戶端識別碼 (，以及在 M365 系統管理中心設定視窗中) 步驟 3.b (用戶端密碼，以使用 Azure AD OpenID Connect 向您的 ServiceNow 實例進行驗證。

## <a name="step-4-select-tables-properties-and-filter-data"></a>步驟 4：選取資料表、屬性和篩選資料

在此步驟中，您可以從 ServiceNow 資料來源新增或移除可用的資料表和屬性。 根據預設，Microsoft 365 已選取幾個資料表和屬性。

透過 ServiceNow 查詢字串，您可以指定同步票證的條件。 它就像 **SQL Select** 語句中的 **Where** 子句。 例如，您可以選擇只為過去六個月建立且處於開啟狀態的票證編制索引。 若要瞭解如何建立您自己的查詢字串，請參閱 [使用篩選產生編碼的查詢字串](https://docs.servicenow.com/en-US/bundle/sandiego-platform-user-interface/page/use/using-lists/task/t_GenEncodQueryStringFilter.html)。

使用 [預覽結果] 按鈕來驗證所選屬性和查詢篩選的範例值。

## <a name="step-5-manage-search-permissions"></a>步驟 5：管理搜尋許可權

ServiceNow Tickets Graph 連接器支援 **只有具有此資料來源存取權的人員** 才能看見搜尋許可權。 已編制索引的票證會出現在搜尋結果中，且可透過 `assigned_to` 和 `opened_by` 欄位存取這些票證的使用者可以看到。

當您選擇 **[僅限可存取此資料來源的人員**] 時，您必須進一步選擇您的 ServiceNow 實例是否具有 Azure Active Directory (Azure AD) 布建的使用者或非 Azure AD 使用者。

若要識別哪個選項適合您的組織：

1. 如果 ServiceNow 使用者的Email識別碼與 **Azure AD** 中使用者的 USERPrincipalName (UPN) **相同**，請選擇 [Azure AD] 選項。
2. 如果 ServiceNow 使用者的電子郵件識別碼與 **Azure AD** 中使用者的電子郵件識別碼 **不同** ，請選擇 [非 Azure AD] (UPN) 。 

>[!NOTE]
> * 如果您選擇 Azure AD 作為身分識別來源的類型，連接器會將從 ServiceNow 取得的使用者Email識別碼直接對應至 Azure AD 中的 UPN 屬性。
> * 如果您針對身分識別類型選擇 [非 Azure AD]，請參閱對應 [您的非 Azure AD 身](map-non-aad.md) 分識別以取得對應身分識別的指示。 您可以使用此選項來提供從EMAIL識別碼到 UPN 的對應正則運算式。


## <a name="step-6-assign-property-labels"></a>步驟 6：指派屬性標籤

請遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-7-manage-schema"></a>步驟 7：管理架構

請遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-8-choose-refresh-settings"></a>步驟 8：選擇重新整理設定

請遵循一般 [設定指示](./configure-connector.md)。

>[!NOTE]
>針對身分識別，只會套用完整編目排程。

## <a name="step-9-review-connection"></a>步驟 9：檢閱連線

請遵循一般 [設定指示](./configure-connector.md)。

發佈連線之後，您必須自訂搜尋結果頁面。 若要瞭解如何自訂搜尋結果，請參閱 [自訂搜尋結果頁面](/microsoftsearch/configure-connector#next-steps-customize-the-search-results-page)。

## <a name="limitations"></a>限制
ServiceNow Knowledge Microsoft Graph 連接器在其最新版本中具有下列限制：

- [管理搜尋許可權] 步驟下的 *[每個人*] 功能都不會處理任何許可權。 除非您想要在隔離的環境中測試所選小組成員之間的連線，否則請勿選取此選項。

## <a name="troubleshooting"></a>疑難排解
發佈連線、自訂結果頁面之後，您可以在 [系統管理中心的](https://admin.microsoft.com)[**資料來源**] 索引標籤下檢閱狀態。 若要瞭解如何進行更新和刪除，請參閱 [管理您的連接器](manage-connector.md)。
您可以在下方找到常見問題的疑難排解步驟。
### <a name="1-unable-to-log-in-due-to-single-sign-on-enabled-servicenow-instance"></a>1.無法登入，因為已啟用單一登入的 ServiceNow 實例

如果您的組織已啟用單一登入 (SSO) 至 ServiceNow，您可能無法使用服務帳戶登入。 您可以將 新<em> `login.do` </em>增至 ServiceNow 實例 URL，以顯示使用者名稱和密碼型登入。 例子。 `https://<your-organization-domain>.service-now.com./login.do`

### <a name="2-unauthorized-or-forbidden-response-to-api-request"></a>2.未經授權或禁止回應 API 要求

#### <a name="21-check-table-access-permissions"></a>2.1. 檢查資料表存取權限
如果您在線上狀態中看到禁止或未經授權的回應，請檢查服務帳戶是否具有 [步驟 3：連線設定](#step-3-connection-settings)中所述資料表的必要存取權。 檢查資料表中的所有資料行是否有讀取權限。

#### <a name="22-change-in-account-password"></a>2.2. 變更帳戶密碼
Microsoft Graph 連接器會使用代表服務帳戶擷取的存取權杖進行編目。 存取權杖會每隔 12 小時重新整理一次。 確定服務帳戶密碼在發佈連線之後不會變更。 如果密碼有變更，您可能需要重新驗證連線。

#### <a name="23-check-if-servicenow-instance-behind-firewall"></a>2.3. 檢查防火牆後方的 ServiceNow 實例
如果 ServiceNow 實例位於網路防火牆後方，則 Microsoft Graph 連接器可能無法連線到該實例。 您必須明確允許存取連接器服務。 您可以在下表中找到連接器服務的公用 IP 位址範圍。 根據您的租使用者區域，將它新增至您的 ServiceNow 實例網路允許清單。

**環境** | **地區** | **Range**
--- | --- | ---
PROD | 北美 | 52.250.92.252/30, 52.224.250.216/30
PROD | 歐洲 | 20.54.41.208/30, 51.105.159.88/30
PROD | 亞太地區 | 52.139.188.212/30, 20.43.146.44/30

#### <a name="24-access-permissions-not-working-as-expected"></a>2.4. 存取權限未如預期般運作

如果您觀察到套用至搜尋結果的存取權限不一致，請確認搜尋使用者是否為 和 `opened_by` 欄位的一 `assigned_to` 部分。


### <a name="3-issues-with-only-people-with-access-to-this-data-source-permission"></a>3. *只有具有此資料來源許可權存取權的人員* 的問題

#### <a name="31-user-mapping-failures"></a>3.1 使用者對應失敗

 在 Azure Active Directory 中沒有 Microsoft 365 使用者的 ServiceNow 使用者帳戶將不會對應。 非使用者的服務帳戶預期會使使用者對應失敗。 您可以在連線詳細資料視窗的身分識別統計資料區域中存取使用者對應失敗數目。 您可以從 [錯誤] 索引標籤下載失敗的使用者對應記錄。
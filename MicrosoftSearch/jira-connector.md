---
title: Atlassian Jira Cloud Microsoft Graph 連接器
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
description: 設定適用于 Microsoft Search 的 Atlassian Jira Cloud Graph 連接器
ms.openlocfilehash: ebfc621cfcbb9154ec0a762b65232a41f569f9a8
ms.sourcegitcommit: 1f8f69a9f7b48880ba23a38ed4bbd84d3e072f04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/03/2022
ms.locfileid: "67597044"
---
# <a name="atlassian-jira-cloud-microsoft-graph-connector"></a>Atlassian Jira Cloud Microsoft Graph 連接器

Atlassian Jira Cloud Microsoft Graph 連接器可讓您的組織為 Jira 問題編制索引。 從 Jira 網站設定連接器和索引內容之後，使用者可以在 Microsoft Search 中搜尋這些專案。

> [!NOTE]
> 請閱讀Microsoft 365 系統管理中心文章 [**中的設定 Microsoft Graph 連接器**](configure-connector.md)一文，以瞭解一般連接器設定指示。

本文適用于設定、執行及監視 Atlassian Jira Cloud 連接器的任何人。 它會補充一般設定程式，並顯示僅適用于 Atlassian Jira Cloud 連接器的指示。

>[!IMPORTANT]
>Atlassian Jira Cloud 連接器僅支援 Jira 雲端託管實例。 此連接器不支援 Jira Server 和 Jira 資料中心版本。

## <a name="before-you-get-started"></a>開始之前

您必須是組織 Microsoft 365 租使用者的系統管理員，以及貴組織 Jira 網站的系統管理員。

您需要將下列許可權授與在連接器設定期間使用認證的使用者帳戶：

| 許可權名稱 | 許可權類型 | 的必要專案 |
| ------------ | ------------ | ------------ |
| 流覽專案 | [專案許可權](https://support.atlassian.com/jira-cloud-administration/docs/manage-project-permissions/) | 編目 Jira 問題。 此許可權是需要編制索引之專案的 **必要** 許可權。 |
| 問題層級安全性許可權 | [問題層級安全性](https://support.atlassian.com/jira-cloud-administration/docs/configure-issue-security-schemes/) | 編目不同的問題類型。 此許可權是 **選擇性的**。 |
| 流覽使用者和群組   | [通用權限](https://support.atlassian.com/jira-cloud-administration/docs/manage-global-permissions/) | 搜尋結果的 ACL 修剪。 此許可權是 **選擇性的** ，必須選 `Only people with access to this data source` 取下列步驟 4 中的選項。 |
| 管理 Jira | [通用權限](https://support.atlassian.com/jira-cloud-administration/docs/manage-global-permissions/) | 搜尋結果的 ACL 修剪。 此許可權是 **選擇性的** ，必須選 `Only people with access to this data source` 取下列步驟 4 中的選項。 |

## <a name="step-1-add-a-connector-in-the-microsoft-365-admin-center"></a>步驟 1：在Microsoft 365 系統管理中心中新增連接器
請遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-2-name-the-connection"></a>步驟 2：命名連線
請遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-3-configure-the-connection-settings"></a>步驟 3：設定連線設定
若要連線到您的 Jira 網站，請使用您的 Jira 網站 URL。 Jira 雲端網站 URL 通常看起來像 *HTTPs：//<organization_name>.atlassian.net/*。 您可以選擇 [基本驗證] 或 [OAuth 2.0]， (建議) 向您的 Jira 網站進行驗證。

### <a name="basic-auth"></a>基本驗證
輸入您帳戶的使用者名稱 (通常是電子郵件識別碼) 和 API 權杖，以使用基本驗證進行驗證。若要深入瞭解如何產生 API 權杖，請參閱 Atlassian 的檔，以瞭解如何 [管理 Atlassian 帳戶的 API 權杖](https://support.atlassian.com/atlassian-account/docs/manage-api-tokens-for-your-atlassian-account/)。

### <a name="oauth-20"></a>OAuth 2.0
在 Atlassian Jira 中註冊應用程式，讓 Microsoft Search 應用程式可以存取實例。 若要深入瞭解，請參閱 Atlassian 支援檔，以瞭解如何 [啟用 OAuth 2.0](https://developer.atlassian.com/cloud/jira/platform/oauth-2-3lo-apps/#enabling-oauth-2-0--3lo-)。

下列步驟提供如何註冊應用程式的指引：

1. 使用 Atlassian Jira 系統管理員帳戶登入 [Atlassian Developer 主控台](https://developer.atlassian.com/console/myapps/) 。
2. 選取 [開啟 `Create` ]，然後選取 `OAuth 2.0 integration` 。
3. 為應用程式提供適當的名稱，並建立新的應用程式。
4. 從左側的流覽窗格巡覽至 `Permissions` 。 在 [細微許可權] 標頭下，選取 `Add` 。 `Jira API` 新增之後，請選取 [開啟 `Configure` ]，然後新增下列列範圍。

   | **#** | **範圍名稱** | **代碼** |
   | ------------ | ------------ | ------------ |
   | 1 | 檢視欄位 | `read:field:jira` |
   | 2 | 檢視虛擬人偶 | `read:avatar:jira` |
   | 3 | 檢視專案類別 | `read:project-category:jira` |
   | 4 | 檢視專案 | `read:project:jira` |
   | 5 | 讀取欄位組態 | `read:field-configuration:jira` |
   | 6 | 檢視問題類型 | `read:issue-type:jira` |
   | 7  | 檢視專案屬性 | `read:project.property:jira` |
   | 8  | 檢視使用者 | `read:user:jira` |
   | 9  | 檢視應用程式角色 | `read:application-role:jira` |
   | 10 | 檢視群組 | `read:group:jira` |
   | 11 | 讀取問題類型階層 | `read:issue-type-hierarchy:jira` |
   | 12  | 檢視專案版本 | `read:project-version:jira` |
   | 13 | 檢視專案元件 | `read:project.component:jira` |
   | 14  | 檢視問題詳細資料 | `read:issue-details:jira` |
   | 15  | 檢視稽核記錄 | `read:audit-log:jira` |
   | 16  | 檢視問題中繼 | `read:issue-meta:jira` |
   | 17  | 檢視專案角色 | `read:project-role:jira` |
   | 18  | 檢視問題安全性層級 | `read:issue-security-level:jira` |
   | 19 | 檢視問題安全性配置 | `read:issue-security-scheme:jira` |
   | 20 | 檢視許可權配置 | `read:permission-scheme:jira` |
   |  21 | 檢視許可權 | `read:permission:jira` |

5. 從左側的流覽窗格巡覽至 `Authorization` 。 針對 **M365 Government 新增 M365 Enterprise**： `https://gcs.office.com/v1.0/admin/oauth/callback` 的回呼 URL： `https://gcsgcc.office.com/v1.0/admin/oauth/callback` ，並儲存變更。
6. 從左側的流覽窗格巡覽至 `Settings` 。 您會從此頁面取得 `Client ID` 和 `Secret` 。

使用 **用戶端標識** 符和 **秘密** 完成連線設定步驟。

> [!NOTE]
>
> * 若要深入瞭解 Jira 許可權，請參閱 OAuth 2.0 應用程式 [的範圍清單](https://developer.atlassian.com/cloud/jira/platform/scopes-for-oauth-2-3LO-and-forge-apps/#list-of-scopes) 。
> * Jira 雲端的原始 (傳統) OAuth 許可權已被取代。 若要深入瞭解，請參閱 [changelog 公告](https://developer.atlassian.com/cloud/jira/platform/changelog/#CHANGE-517) 。

### <a name="step-3a-configure-data-select-projects"></a>步驟 3a：設定資料：選取專案

您可以選擇連線，只為整個 Jira 網站或特定專案編制索引。

* 如果您選擇為整個 Jira 網站編制索引，網站中所有專案中的 Jira 問題都會編制索引。 新專案和問題將會在建立之後的下一個編目期間編制索引。
* 如果您選擇個別專案，則只會編制這些專案中的 Jira 問題索引。

> [!NOTE]
> 當您將 _[流覽專案_ ] 許可權授與 Jira 專案時，將會列出它，而且可以進行編目。 如果專案遺失，請檢查您帳戶的許可權。

您可以進一步選擇篩選將以兩種方式編制索引的 Jira 問題。

* 指定 **問題修改時間週期**。 這 **只會根據目前的** 搜耙，在選取的時間週期內建立或修改的 Jira 問題編制索引。
* 指定 **JQL**。 這只會根據提供的 Jira 查詢語言 (JQL) ，為篩選後傳回的 Jira 問題編制索引。 若要深入瞭解如何使用 JQL，請參閱 Atlassian 支援檔，以瞭解如何 [搭配 Jira 查詢語言使用進階搜尋](https://support.atlassian.com/jira-service-management-cloud/docs/use-advanced-search-with-jira-query-language-jql/)

> [!TIP]
> 您可以使用 JQL 篩選器，只使用 「*issueType in (Bug，Improvement)*」 為特定 Jira 問題類型編制索引

### <a name="step-3b-configure-data-select-properties"></a>步驟 3b：設定資料：選取屬性

在繼續之前，請選取您想要連線到這些欄位中索引和預覽資料的欄位。 預設已經選取某些欄位，而且無法移除。

Atlassian Jira 連接器可以為預設問題欄位和自訂建立的問題欄位編制索引。

> [!NOTE]
> 如果某些 Jira 問題類型 (的) 中沒有選取的自訂建立欄位，則欄位會擷取為 *Null* (空白) 。

## <a name="step-4-manage-search-permissions"></a>步驟 4：管理搜尋許可權

Atlassian Jira 連接器支援  **「所有人** 」或 **「僅限具有此資料來源存取權的人員**」可看見的搜尋許可權。 如果您選擇 [ **所有人**]，已編制索引的資料會出現在所有使用者的搜尋結果中。 如果您選擇 **[僅限可存取此資料來源的人員**]，則已編制索引的資料會出現在可存取此資料來源之使用者的搜尋結果中。 在 Atlassian Jira 中，安全性許可權是使用包含網站層級群組和專案角色的專案許可權配置來定義。 問題層級安全性也可以使用問題層級許可權配置來定義。

如果您選擇 **[僅限可存取此資料來源的人員**]，則必須進一步選擇 Jira 網站是否具有 Azure Active Directory (Azure AD) 布建的使用者或非 Azure AD 使用者。

若要識別哪個選項適合您的組織：

1. 如果 Jira 使用者的Email識別碼與 **Azure AD** 中使用者的 USERPrincipalName (UPN) **相同**，請選擇 [Azure AD] 選項。
2. 如果 Jira 使用者的電子郵件識別碼與 Azure AD 中使用者的電子郵件識別碼 **不同**，請選擇 [非 **Azure AD**] (UPN) 。

>[!NOTE]
> * 如果您選擇 Azure AD 作為身分識別來源的類型，連接器會將從 Jira 取得的使用者Email識別碼直接對應至 Azure AD 中的 UPN 屬性。
> * 如果您針對身分識別類型選擇 [非 Azure AD]，請參閱對應 [您的非 Azure AD 身](map-non-Azure AD.md) 分識別以取得對應身分識別的指示。 您可以使用此選項來提供從EMAIL識別碼到 UPN 的對應正則運算式。

## <a name="step-5-assign-property-labels"></a>步驟 5：指派屬性標籤

請遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-6-manage-schema"></a>步驟 6：管理架構

請遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-7-choose-refresh-settings"></a>步驟 7：選擇重新整理設定

Atlassian Jira 連接器支援完整和增量編目的重新整理排程。
累加編目的建議排程為一小時，而完整編目則為一天。

## <a name="step-8-review-connection"></a>步驟 8：檢閱連線

請遵循一般 [設定指示](./configure-connector.md)。

發佈連線之後，您必須自訂搜尋結果頁面。 若要瞭解如何自訂搜尋結果，請參閱 [自訂搜尋結果頁面](/microsoftsearch/configure-connector#next-steps-customize-the-search-results-page)。

## <a name="step-9-set-up-search-result-page"></a>步驟 9：設定搜尋結果頁面

發佈連線之後，您必須使用垂直和結果類型來自訂搜尋結果頁面。 若要瞭解如何自訂搜尋結果，請檢閱如何 [管理垂直](manage-verticals.md) 和 [結果類型](manage-result-types.md)。
您也可以使用 Jira 連接器的 [範例結果配置](jira-connector-result-layout.md) 。 只要複製並貼上結果配置 JSON 即可開始使用。

## <a name="troubleshooting"></a>疑難排解

以下是在設定連接器或編目期間觀察到的常見錯誤清單，以及其可能的原因。

| 步驟 | 錯誤訊息 | 可能的原因 ()  |
| ------------ | ------------ | ------------ |
| 連線設定 | 要求格式不正確或不正確。 | 不正確的 Jira 網站 URL。 |
| 連線設定 | 無法連線到 Jira 網站的 Jira 雲端服務。 | 不正確的 Jira 網站 URL。 |
| 連線設定 | 用戶端沒有執行動作的許可權。 | 為基本驗證提供的 API 權杖無效。 |
| 連線設定 | OAuth 快顯視窗中發生「發生錯誤」錯誤。 | 授與 OAuth 應用程式的範圍不相符。 不相符的範圍會列在快顯視窗中。 |
| 連接器設定後 (編目時間)  | 無法使用資料來源進行驗證。 確認與此資料來源相關聯的認證正確無誤。 | 使用者沒有編目 Jira 所需的一或多個許可權。 |
| 連接器設定後 (編目時間)  | 您沒有存取此資料來源的許可權。 您可以連絡此資料來源的擁有者以要求許可權。 | 如果您使用 OAuth，應用程式範圍可能已變更，或應用程式可能已過期或已刪除。 <br> 如果您使用基本驗證，API 權杖可能已過期或已刪除。 |

## <a name="limitations"></a>限制

以下是 Atlassian Jira 連接器的已知限制：

* 不支援 Jira Server 和資料中心版本。

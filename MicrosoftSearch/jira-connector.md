---
title: Atlassian Jira Graph connector for Microsoft 搜尋
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
description: 設定 Microsoft 搜尋的 Atlassian Jira Graph 連接器
ms.openlocfilehash: 1edc5adec820aea9a3cb9b1a23dec0791b291495
ms.sourcegitcommit: d2bb36b6d3102b08ced93faa5e102bdb7e7e1e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2021
ms.locfileid: "60720621"
---
# <a name="atlassian-jira-graph-connector-preview"></a>Atlassian Jira Graph connector (preview) 

Atlassian Jira Graph connector 可讓您的組織建立 Jira 問題的索引。 在您設定 Jira 網站的連接器和索引內容之後，使用者就可以在 Microsoft 搜尋中搜尋這些專案。

> [!NOTE]
> * 請閱讀 [**Graph 連接器**](configure-connector.md)文章的設定，以瞭解一般 Graph 連接器設定指示。
> * Atlassian Jira Graph connector 位於預覽中。 如果您想要取得儘早的試用權，請使用 [<b> 此表單 </b>](https://forms.office.com/r/kVZAvpn6YP)註冊。

本文適用于任何設定、執行及監控 Atlassian Jira Graph connector 的使用者。 它會補充一般設定程式，並顯示只適用于 Atlassian Jira Graph connector 的指示。

>[!IMPORTANT]
>Atlassian Jira Graph connector 只支援 Jira 雲端主控的實例。 此連接器不支援 Jira Server 和 Jira 資料中心版本。

## <a name="before-you-get-started"></a>開始之前

您必須是組織之 M365 租使用者的系統管理員，以及組織之 Jira 網站的管理員。

您必須將下列許可權授與在設定連接器時使用其認證的使用者帳戶：

| 許可權名稱 | 許可權類型 | 需要的 |
| ------------ | ------------ | ------------ |
| 流覽專案 | [Project 許可權](https://support.atlassian.com/jira-cloud-administration/docs/manage-project-permissions/) | 編目 Jira 問題。 此許可權對於需要編制索引的專案是 **必要** 的。 |
| 問題層級安全性許可權 | [問題層級安全性](https://support.atlassian.com/jira-cloud-administration/docs/configure-issue-security-schemes/) | 編目不同的問題類型。 這是 **選用** 的許可權。 |
| 流覽使用者和群組   | [通用權限](https://support.atlassian.com/jira-cloud-administration/docs/manage-global-permissions/) | 搜尋結果的 ACL 修整。 此許可權是 **選用** 的，而且必須選取 `Only people with access to this data source` 下列步驟4中的選項。 |
| 管理 Jira | [通用權限](https://support.atlassian.com/jira-cloud-administration/docs/manage-global-permissions/) | 搜尋結果的 ACL 修整。 此許可權是 **選用** 的，而且必須選取 `Only people with access to this data source` 下列步驟4中的選項。 |

## <a name="step-1-add-a-graph-connector-in-the-microsoft-365-admin-center"></a>步驟1：在 Microsoft 365 系統管理中心中新增 Graph 連接器
遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-2-name-the-connection"></a>步驟2：命名連線
遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-3-configure-the-connection-settings"></a>步驟3：設定連接設定
若要連線到您的 Jira 網站，請使用您的 Jira 網站 URL。 Jira 雲端網站 URL 的外觀通常如 *HTTPs://<organization_name> atlassian.net/*。 您可以選擇 [基本驗證] 或 OAuth 2.0 (建議) ，以驗證您的 Jira 網站。

### <a name="basic-auth"></a>基本驗證
輸入您的帳戶的使用者名稱 (通常是透過基本身分驗證來驗證的電子郵件 ID) 和 API 權杖。若要深入瞭解如何產生 API 權杖，請參閱 Atlassian 的檔，以瞭解如何為 [您的 Atlassian 帳戶管理 API 權杖](https://support.atlassian.com/atlassian-account/docs/manage-api-tokens-for-your-atlassian-account/)。

### <a name="oauth-20"></a>OAuth 2。0
在 Atlassian Jira 中註冊應用程式，讓 Microsoft 搜尋應用程式可以存取實例。 若要深入瞭解，請參閱 Atlassian 支援檔，以瞭解如何 [啟用 OAuth 2.0](https://developer.atlassian.com/cloud/jira/platform/oauth-2-3lo-apps/#enabling-oauth-2-0--3lo-)。

下列步驟提供如何註冊應用程式的指導方針：

1. 使用您的 Atlassian Jira 系統管理員帳戶登入 [Atlassian 開發人員主控台](https://developer.atlassian.com/console/myapps/) 。
2. 按一下 `Create` 並選取 `OAuth 2.0 integration`
3. 為應用程式提供適當的名稱，並建立新的應用程式。
4. `Permissions`從左側的功能窗格流覽至。 按一下 [是] `Add` `Jira platform REST API` 。 新增後，按一下 `Configure` 並新增下列範圍- `View Jira issue data` 、 `Manage Jira global settings` 和 `View user profiles` 。
5. `Authorization`從左側的功能窗格流覽至。 新增回撥 URL `https://gcs.office.com/v1.0/admin/oauth/callback` 並儲存變更。
6. `Settings`從左側的功能窗格流覽至。 您將會收到 `Client ID` 及 `Secret` 至此頁面。

在註冊具有上述詳細資料的應用程式時，您將取得 **用戶端識別碼** 和 **密碼**。 完成 [連線設定] 步驟，使用這些步驟。

### <a name="step-3a-configure-data-select-projects"></a>步驟3a：設定資料：選取專案

您可以選擇連接為整個 Jira 網站或特定專案的索引。

* 如果您選擇為整個 Jira 網站編制索引，網站中的所有專案的 Jira 問題都會取得索引。 在建立新專案及問題之後，會在下一次編目期間編制索引。
* 如果您選擇個別專案，則只有那些專案中的 Jira 問題會編制索引。

> [!NOTE]
> 當您授與 _流覽專案_ Jira 專案的許可權時，會列出該專案，而且可以進行編目。 如果專案遺失，請檢查您的帳戶許可權。

您可以進一步選擇篩選將以兩種方式編制索引的 Jira 問題。

* 指定 **問題的修改時間週期**。 這只會針對根據目前編目所 **選取的時間** 週期建立或修改的 Jira 問題進行索引。
* 指定 **JQL**。 這只會為根據提供的 Jira 查詢語言 (JQL) 所傳回的 Jira 問題建立索引。 若要深入瞭解如何使用 JQL，請參閱 Atlassian Support 檔， [使用具有 Jira 查詢語言的高級搜尋](https://support.atlassian.com/jira-service-management-cloud/docs/use-advanced-search-with-jira-query-language-jql/)

> [!TIP]
> 您可以使用 JQL 篩選，只使用「*issueType in (Bug，提高)*"來編制特定 Jira 問題類型的索引。

### <a name="step-3b-configure-data-select-properties"></a>步驟3b：設定資料：選取屬性

在繼續之前，請選取您要連線索引及預覽這些欄位中資料的欄位。 有些欄位已經預設已選取，無法移除。

Atlassian Jira Graph connector 可以編制預設發貨欄位及自訂已建立的問題欄位。

> [!NOTE]
> 如果選取的自訂建立的欄位不存在於某些 Jira 發貨類型中 (s) ，此欄位將會 ingested 為 *Null* (空白) 。

## <a name="step-4-manage-search-permissions"></a>步驟4：管理搜尋許可權

Atlassian Jira Graph connector 可對  **所有人** 或 **只有存取此資料來源的人員顯示的** 搜尋許可權。 如果您選擇 [ **任何人**]，索引資料將會出現在所有使用者的搜尋結果中。 如果您只選擇可 **存取此資料來源的人員**，則具有存取權的使用者可在搜尋結果中顯示索引的資料。 在 Atlassian Jira 中，安全性許可權是使用包含網站層級群組和專案角色的專案許可權架構來定義的。 您也可以使用問題層級許可權方案來定義問題層級安全性。

如果您只選擇可 **存取此資料來源的人員**，您需要進一步選擇您的 Jira 網站是否有 Azure Active Directory (AAD) 已布建的使用者或非 AAD 的使用者。

若要找出適合您組織的選項：

1. 如果 Jira 使用者的電子郵件識別碼與 AAD 中使用者的 UserPrincipalName (UPN) **相同**，請選擇 **AAD** 選項。
2. 如果 Jira 使用者的電子郵件識別碼 **不同** 于 AAD 中使用者的 UserPrincipalName (UPN) ，請選擇 [**非 AAD** ] 選項。

>[!NOTE]
> * 如果您選擇 AAD 做為身分識別來源的類型，連接器會將從 Jira 取得的使用者電子郵件 IDs 直接對應至 AAD 中的 UPN 屬性。
> * 如果您為身分識別類型選擇「非 AAD」，請參閱[對應您的非 Azure AD](map-non-aad.md)身分識別，以取得對應身分識別的指示。 您可以使用此選項，提供從電子郵件識別碼到 UPN 的對應正則運算式。

## <a name="step-5-assign-property-labels"></a>步驟5：指派屬性標籤

遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-6-manage-schema"></a>步驟6：管理架構

遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-7-choose-refresh-settings"></a>步驟7：選擇重新整理設定

Atlassian Jira Graph connector 支援完整和累加編目的更新排程。
建議的排程為一小時用於增量編目，而一天則是完整編目。

## <a name="step-8-review-connection"></a>步驟8：檢查連線

遵循一般 [設定指示](./configure-connector.md)。

## <a name="troubleshooting"></a>疑難排解
以下是設定連接器或編目時所看到的常見錯誤清單，以及可能的原因。

| 步驟 | 錯誤訊息 | 可能的原因 (s)  |
| ------------ | ------------ | ------------ |
| 連接設定 | 要求格式錯誤或不正確。 | 不正確的 Jira 網站 URL |
| 連接設定 | 無法到達 Jira 網站的 Jira 雲端服務。 | 不正確的 Jira 網站 URL |
| 連接設定 | 用戶端沒有執行該動作的許可權。 | 針對基本驗證提供的 API 權杖無效 |
| 連接設定 | OAuth 快顯視窗中的「發生錯誤」錯誤。 | 授與 OAuth 應用程式的範圍不相符。 快顯視窗中會列出不匹配的範圍。 |
|  (後置後設定) 的編目時間 | 無法使用資料來源進行驗證。 驗證與此資料來源相關聯的認證是否正確。 | 使用者沒有編目 Jira 所需的一或多個許可權。 |
|  (後置後設定) 的編目時間 | 您沒有存取此資料來源的許可權。 您可以聯繫此資料來源的擁有者以要求許可權。 | 在 OAuth 的情況下，應用程式範圍可能已變更，或應用程式可能已到期或已刪除。 <br> 若為基本驗證，API 權杖可能已到期或已刪除。 |

## <a name="limitations"></a>限制
下列為 Atlassian Jira Graph connector 的已知限制：
* 不支援 Jira Server 和資料中心版本。
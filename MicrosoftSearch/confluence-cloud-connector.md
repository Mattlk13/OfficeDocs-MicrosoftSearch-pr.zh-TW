---
title: Confluence Cloud Microsoft Graph連接器
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
description: 設定適用于 Microsoft 搜尋 的 Confluence Cloud Graph 連接器
ms.openlocfilehash: 34cc78def0534cd0e7778fe2b69d4791fb251823
ms.sourcegitcommit: d267711f8e1c68849c99a4aad2bd387214825416
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2022
ms.locfileid: "65645953"
---
<!---Previous ms.author: kam1 --->

# <a name="confluence-cloud-microsoft-graph-connector"></a>Confluence Cloud Microsoft Graph連接器

Confluence Cloud Microsoft Graph連接器可讓您的組織為 Confluence 內容編制索引。 設定連接器並從 Confluence 網站編制資料索引之後，使用者就可以在Microsoft 搜尋中搜尋這些內容。

本文適用于Microsoft 365系統管理員或設定、執行及監視 Confluence Cloud 連接器的任何人。 它補充Microsoft 365 系統管理中心文章中設定[Microsoft Graph 連接器中提供的一](configure-connector.md)般指示。 如果您尚未這麼做，請閱讀整篇文章以瞭解一般設定程式。

安裝程式中的每個步驟如下所列，並附上一個附注，指出您應該遵循一般設定指示或僅適用于 Confluence Cloud 連接器的其他指示，包括 [疑難排解](#troubleshooting) 和 [限制的相關](#limitations)資訊。

## <a name="before-you-get-started"></a>開始之前

您必須是組織Microsoft 365租使用者的系統管理員，以及組織 Confluence 網站的系統管理員。

## <a name="step-1-add-a-connector-in-the-microsoft-365-admin-center"></a>步驟 1：在Microsoft 365 系統管理中心中新增連接器

請遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-2-name-the-connection"></a>步驟 2：命名連線

請遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-3-configure-the-connection-settings"></a>步驟 3：設定連線設定

若要連線到您的 Confluence 網站，請使用您的網站 URL。 Confluence 雲端網站 URL 通常看起來像 *HTTPs：//<organization_name>.atlassian.net/*。 您可以選擇 [基本驗證] 或 [OAuth 2.0]， (建議) 向您的 Confluence 網站進行驗證。

>[!TIP]
>請確定服務帳戶具有您想要編制索引之 Confluence 內容的檢 **視存取權** 。

### <a name="basic-auth"></a>基本驗證

輸入您帳戶的使用者名稱 (通常是電子郵件識別碼) 和 API 權杖，以使用基本驗證進行驗證。若要深入瞭解如何產生 API 權杖，請參閱 Atlassian 的檔，以瞭解如何 [管理 Atlassian 帳戶的 API 權杖](https://support.atlassian.com/atlassian-account/docs/manage-api-tokens-for-your-atlassian-account/)。

### <a name="oauth-20-recommended"></a>OAuth 2.0 (建議) 

在 Confluence Cloud 中註冊應用程式，讓Microsoft 搜尋應用程式可以存取實例。 若要深入瞭解，請參閱 Atlassian 支援檔，以瞭解如何 [啟用 OAuth 2.0](https://developer.atlassian.com/cloud/confluence/oauth-2-3lo-apps/#enabling-oauth-2-0--3lo-)。

下列步驟提供如何註冊應用程式的指引：

1. 使用您的 Atlassian Confluence 系統管理員帳戶登入 [Atlassian Developer 主控台](https://developer.atlassian.com/console/myapps/) 。
2. 按一下 [ **建立** ]，然後選取 `OAuth 2.0 integration` 。
3. 為應用程式提供適當的名稱，並建立新的應用程式。
4. 從左側的流覽窗格巡覽至 `Permissions` 。 針對 按一下 **[新增** ] `Confluence API` 。 新增之後，按一下 [ **設定**]、[ **編輯範圍]** ，然後選取下列範圍。

| **範圍名稱** | **代碼** | **描述** |
| ------------ | ------------ | ------------ |
| 檢視內容詳細資料 | `read:content-details:confluence` | 符合準則的編目內容
| 檢視群組 | `read:group:confluence` | 若要存取內容的群組許可權
| 檢視使用者詳細資料 | `read:user:confluence` | 存取個別使用者詳細資料以支援許可權

5. 按一下 **儲存**。
6. 從左側的流覽窗格巡覽至 `Authorization` 。 新增回呼 URL `https://gcs.office.com/v1.0/admin/oauth/callback` 並儲存變更。
7. 從左側的流覽窗格巡覽至 `Settings` 。 您會從此頁面取得 `Client ID` 和 `Secret` 。

使用上述詳細資料註冊應用程式時，您會取得 **用戶端識別碼** 和 **秘密**。 使用下列專案完成連線設定步驟。

## <a name="step-4-select-properties-and-filter-data"></a>步驟 4：選取屬性並篩選資料

在此步驟中，您可以從 Confluence 資料來源新增或移除可用的屬性。 Microsoft 365預設已經選取幾個屬性。

使用 Confluence 查詢語言 (CQL) 字串，您可以指定同步頁面的條件。 它就像 SQL **Select** 語句中的 **Where** 子句。 例如，您可以選擇只為過去兩年中修改的頁面編制索引。 若要瞭解如何建立您自己的查詢字串，請參閱 [使用 CQL 進行進階搜尋](https://developer.atlassian.com/server/confluence/advanced-searching-using-cql/)。 根據預設，連接器會編制所有部落格和頁面的索引。

>[!TIP]
>您可以使用 CQL 篩選來編制 **在特定時間之後修改的內容** 索引， *lastModified >= 「2018/12/31」*

使用 [預覽結果] 按鈕來驗證所選屬性和 CQL 字串的範例值。

## <a name="step-5-manage-search-permissions"></a>步驟 5：管理搜尋許可權

Confluence Cloud Microsoft Graph連接器支援可讓  **任何** 使用者或 **只有具有此資料來源存取權的人員** 看見的搜尋許可權。 如果您選擇 [ **所有人**]，已編制索引的資料會出現在所有使用者的搜尋結果中。 如果您選擇 **[僅限可存取此資料來源的人員**]，則已編制索引的資料會出現在可存取此資料來源之使用者的搜尋結果中。

在 Confluence Cloud 中，使用者和群組的安全性許可權是使用空間許可權和頁面限制來定義。 如果沒有任何頁面限制，Confluence Cloud 連接器會套用空間許可權。 如果存在頁面層級限制，則優先于空間許可權。

如果您選擇 **[僅限可存取此資料來源的人員**]，您必須進一步選擇 Confluence 網站是否Azure Active Directory (AAD) 布建的使用者或非 AAD 使用者。

若要識別哪個選項適合您的組織：

1. 如果 Confluence 使用者的電子郵件識別碼與 **AAD** 中使用者的 UPN) UserPrincipalName (**相同** ，請選擇 [AAD] 選項。
2. 如果 Confluence 使用者的電子郵件識別碼 **不同** 于 UserPrincipalName (AAD 中使用者的 UPN) ，請選擇 [**非** AAD] 選項。

>[!NOTE]
>
> * 如果您選擇 AAD 作為身分識別來源的類型，連接器會將從 Confluence 取得的使用者電子郵件識別碼直接對應至 AAD 的 UPN 屬性。
> * 如果您針對身分識別類型選擇 [非 AAD]，請參閱對應 [您的非 Azure AD 身](map-non-aad.md) 分識別以取得對應身分識別的指示。 您可以使用此選項來提供從電子郵件識別碼到 UPN 的正則運算式對應。

## <a name="step-6-assign-property-labels"></a>步驟 6：指派屬性標籤

請遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-7-manage-schema"></a>步驟 7：管理架構

請遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-8-choose-refresh-settings"></a>步驟 8：選擇重新整理設定

請遵循一般 [設定指示](./configure-connector.md)。

>[!NOTE]
>針對存取權限更新，只會套用完整編目排程。

## <a name="step-9-review-connection"></a>步驟 9：檢閱連線

請遵循一般 [設定指示](./configure-connector.md)。

發佈連線之後，您必須自訂搜尋結果頁面。 若要瞭解如何自訂搜尋結果，請參閱 [自訂搜尋結果頁面](/microsoftsearch/configure-connector#next-steps-customize-the-search-results-page)。

## <a name="troubleshooting"></a>疑難排解

設定連接器時觀察到的常見錯誤及其可能的原因如下所示。

| 設定步驟 | 錯誤訊息 | 可能的原因 ()  |
| ------------ | ------------ | ------------ |
| 連線設定 | 要求格式不正確或不正確。 | 不正確的 Confluence 網站 URL |
| 連線設定 | 無法連線到 Confluence 網站的 Confluence 雲端服務。 | 不正確的 Confluence 網站 URL |
| 連線設定 | 用戶端沒有執行動作的許可權。 | 為基本驗證提供的 API 權杖無效 |
| 選取屬性 | 沒有錯誤訊息，也沒有預覽結果 | 檢查您的 CQL 查詢是否有效 |

## <a name="limitations"></a>限制

Confluence Cloud 連接器在其最新版本中有下列已知限制：

* Confluence Cloud 連接器不會為附件檔案和批註編制索引。
* 索引伺服器和資料中心部署將會以個別連接器的形式發行。

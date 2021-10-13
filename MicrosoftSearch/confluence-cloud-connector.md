---
title: Confluence Cloud Graph connector for Microsoft 搜尋
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
description: 設定 Microsoft 搜尋的 Confluence Cloud Graph connector
ms.openlocfilehash: 88fb53098a7c1ab7678fb051413da73add8c083a
ms.sourcegitcommit: f945096a91c3a9c2a007f72f21a3a039ee02d66d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2021
ms.locfileid: "60275419"
---
<!---Previous ms.author: kam1 --->

# <a name="confluence-cloud-graph-connector-preview"></a>Confluence Cloud Graph Connector (Preview) 

Confluence Cloud Graph connector 可讓您的組織為 Confluence 內容編制索引。 在您設定 Confluence 網站的連接器與索引資料之後，使用者就可以在 Microsoft 搜尋中搜尋這些內容。

>[!NOTE]
>Confluence Cloud Graph Connector 位於預覽中。 如果您想要取得儘早的試用權，請使用 [<b> 此表單 </b>](https://forms.office.com/r/duLxv8Nf8U)註冊。  

本文適用于 Microsoft 365 系統管理員或任何設定、執行及監視 Confluence Cloud Graph connector 的人員。 它會補充[設定 Graph 連接器](configure-connector.md)文章中提供的一般指示。 若尚未這麼做，請閱讀整個設定 Graph 連接器文章，以瞭解一般的設定程式。

安裝程式中的每個步驟都會列在下表中，也就是指出應該遵循一般設定指示或僅適用于 Confluence 雲端 Graph 連接器的其他指示，包括[疑難排解](#troubleshooting)及[限制](#limitations)的相關資訊。


## <a name="before-you-get-started"></a>開始之前
您必須是組織之 M365 租使用者的系統管理員，以及組織之 Confluence 網站的管理員。

## <a name="step-1-add-a-graph-connector-in-the-microsoft-365-admin-center"></a>步驟1：在 Microsoft 365 系統管理中心中新增 Graph 連接器
遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-2-name-the-connection"></a>步驟2：命名連線
遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-3-configure-the-connection-settings"></a>步驟3：設定連接設定
若要連接到您的 Confluence 網站，請使用您的網站 URL。 Confluence 雲端網站 URL 的外觀通常如 *HTTPs://<organization_name> atlassian.net/*。 您可以選擇 [基本驗證] 或 OAuth 2.0 (建議) ，以驗證您的 Confluence 網站。 

>[!TIP]
>請確定服務帳戶具有您要編制索引之 Confluence 內容的 **view 存取權** 。
### <a name="basic-auth"></a>基本驗證
輸入您的帳戶的使用者名稱 (通常是透過基本身分驗證來驗證的電子郵件 ID) 和 API 權杖。若要深入瞭解如何產生 API 權杖，請參閱 Atlassian 的檔，以瞭解如何為 [您的 Atlassian 帳戶管理 API 權杖](https://support.atlassian.com/atlassian-account/docs/manage-api-tokens-for-your-atlassian-account/)。

### <a name="oauth-20-recommended"></a>OAuth 2.0 (建議) 
在 Confluence 雲端中註冊應用程式，讓 Microsoft 搜尋應用程式可以存取實例。 若要深入瞭解，請參閱 Atlassian 支援檔，以瞭解如何 [啟用 OAuth 2.0](https://developer.atlassian.com/cloud/confluence/oauth-2-3lo-apps/#enabling-oauth-2-0--3lo-)。

下列步驟提供如何註冊應用程式的指導方針：

1. 使用您的 Atlassian Confluence 系統管理員帳戶登入 [Atlassian 開發人員主控台](https://developer.atlassian.com/console/myapps/) 。
2. 按一下 `Create` 並選取 `OAuth 2.0 integration`
3. 為應用程式提供適當的名稱，並建立新的應用程式。
4. `Permissions`從左側的功能窗格流覽至。 按一下 [是] `Add` `Confluence API` 。 新增後，按一下 `Configure` 並新增下列範圍-、、、、、 `Read Confluence space summary` `Read Confluence content properties` `Read Confluence detailed content` `Read Confluence content summary` `Read content permission in Confluence` `Read user` `Read user groups` 和 `Search Confluence content and space summaries` 。
5. `Authorization`從左側的功能窗格流覽至。 新增回撥 URL `https://gcs.office.com/v1.0/admin/oauth/callback` 並儲存變更。
6. `Settings`從左側的功能窗格流覽至。 您將會收到 `Client ID` 及 `Secret` 至此頁面。

在註冊具有上述詳細資料的應用程式時，您將取得 **用戶端識別碼** 和 **密碼**。 完成 [連線設定] 步驟，使用這些步驟。

## <a name="step-4-select-properties-and-filter-data"></a>步驟4：選取屬性和篩選資料

在這個步驟中，您可以在 Confluence 資料來源中新增或移除可用的屬性。 Microsoft 365 已經預設會選取一些屬性。

使用 Confluence 查詢語言 (CQL) 字串，您可以指定同步處理頁面的條件。 就像 **SQL Select** 語句中的 **Where** 子句。 例如，您可以選擇只為最近兩年修改的頁面編制索引。 若要瞭解如何建立您自己的查詢字串，請參閱 [使用 CQL 的高級搜尋](https://developer.atlassian.com/server/confluence/advanced-searching-using-cql/)。 依預設，所有的博客及頁面都會由連接器編制索引。

>[!TIP]
>您可以使用 CQL 篩選來索引在特定時間（使用、 *lastModified >= "2018/12/31"* ）**後修改的內容**。

使用 [預覽結果] 按鈕，檢查所選屬性和 CQL 字串的範例值。

## <a name="step-5-manage-search-permissions"></a>步驟5：管理搜尋許可權

Confluence Cloud Graph connector 可對  **所有人** 或 **只有存取此資料來源的人員顯示的** 搜尋許可權。 如果您選擇 [ **任何人**]，索引資料將會出現在所有使用者的搜尋結果中。 如果您只選擇可 **存取此資料來源的人員**，則具有存取權的使用者可在搜尋結果中顯示索引的資料。

在 Confluence 雲端中，使用者和群組的安全性許可權是透過空間許可權和頁面限制來定義的。 Confluence 雲端 Graph 連接器會在沒有頁面限制時，套用空間許可權。 頁面層級限制（若有的話）將優先于空間許可權。

如果您只選擇可 **存取此資料來源的人員**，您需要進一步選擇您的 Confluence 網站是否有 Azure Active Directory (AAD) 已布建的使用者或非 AAD 的使用者。

若要找出適合您組織的選項：

1. 如果 Confluence 使用者的電子郵件識別碼與 AAD 中使用者的 UserPrincipalName (UPN) **相同**，請選擇 **AAD** 選項。
2. 如果 Confluence 使用者的電子郵件識別碼 **不同** 于 AAD 中使用者的 UserPrincipalName (UPN) ，請選擇 [**非 AAD** ] 選項。 

>[!NOTE]
> * 如果您選擇 AAD 做為身分識別來源的類型，連接器會將從 Confluence 取得的使用者電子郵件 IDs 直接對應至 AAD 中的 UPN 屬性。
> * 如果您為身分識別類型選擇「非 AAD」，請參閱[對應您的非 Azure AD](map-non-aad.md)身分識別，以取得對應身分識別的指示。 您可以使用此選項，提供從電子郵件識別碼到 UPN 的對應正則運算式。

## <a name="step-6-assign-property-labels"></a>步驟6：指派屬性標籤

遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-7-manage-schema"></a>步驟7：管理架構

遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-8-choose-refresh-settings"></a>步驟8：選擇重新整理設定

遵循一般 [設定指示](./configure-connector.md)。

>[!NOTE]
>若為存取權更新，只會套用完整編目計畫。

## <a name="step-9-review-connection"></a>步驟9：檢查連線

遵循一般 [設定指示](./configure-connector.md)。

在發佈連線後，您必須自訂搜尋結果頁面。 若要瞭解如何自訂搜尋結果，請參閱 [自訂搜尋結果頁面](/microsoftsearch/configure-connector#next-steps-customize-the-search-results-page)。

## <a name="troubleshooting"></a>疑難排解
下表是設定連接器時所觀察到的常見錯誤，以及可能的原因。

| 設定步驟 | 錯誤訊息 | 可能的原因 (s)  |
| ------------ | ------------ | ------------ |
| 連接設定 | 要求格式錯誤或不正確。 | 不正確的 Confluence 網站 URL |
| 連接設定 | 無法到達 Confluence 網站的 Confluence 雲端服務。 | 不正確的 Confluence 網站 URL |
| 連接設定 | 用戶端沒有執行該動作的許可權。 | 針對基本驗證提供的 API 權杖無效 |
| 選取屬性 | 無錯誤訊息和預覽結果 | 檢查您的 CQL 查詢是否有效 |

## <a name="limitations"></a>限制
Confluence Cloud Graph connector 在其最新版本中有下列已知限制：

- Confluence 雲端連接器不會索引附件檔案和批註。
- 索引伺服器和資料中心部署會以個別的連接器發行。
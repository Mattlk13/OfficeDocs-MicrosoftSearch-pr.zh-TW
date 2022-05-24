---
title: 'Confluence 內部部署 Microsoft Graph 連接器 (Preview) '
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
description: 針對 Microsoft 搜尋 設定 Confluence 內部部署Graph Microsoft 連接器
ms.openlocfilehash: 3ed48d8f49dedaaf53d68f939b3cf64c06b89e19
ms.sourcegitcommit: d267711f8e1c68849c99a4aad2bd387214825416
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2022
ms.locfileid: "65645962"
---
<!---Previous ms.author: kam1 --->

# <a name="confluence-on-premises-microsoft-graph-connector-preview"></a>Confluence 內部部署 Microsoft Graph 連接器 (Preview) 

Confluence 內部部署 Microsoft Graph連接器可讓您的組織為 Confluence 伺服器或資料中心內容編制索引。 設定連接器並從 Confluence 網站編制資料索引之後，使用者就可以在Microsoft 搜尋中搜尋這些內容。

>[!NOTE]
>Confluence 內部部署連接器處於預覽狀態。 如果您想要搶先存取以試用，請使用 [<b> 此表單 </b>](https://forms.office.com/r/JniPmK5bzm)註冊。

本文適用于Microsoft 365系統管理員或設定、執行及監視 Confluence 內部部署連接器的任何人。 它補充了在Microsoft 365 系統管理中心中 [**設定 Microsoft Graph 連接器中提供的一**](configure-connector.md)般指示。

安裝程式中的每個步驟都列在下方，並附上一個附注，指出您應該遵循一般設定指示或僅適用于 Confluence 內部部署Graph連接器的其他指示，包括[疑難排解](#troubleshooting)和[限制的相關](#limitations)資訊。

## <a name="before-you-get-started"></a>開始之前

### <a name="install-the-microsoft-graph-connector-agent"></a>安裝 Microsoft Graph 連接器代理程式

若要為 Confluence 伺服器或資料中心內容編制索引，您必須安裝並註冊連接器代理程式。 如需詳細資訊，請參閱[安裝 Microsoft Graph 連接器代理](./graph-connector-agent.md)程式。

您必須是組織Microsoft 365租使用者的系統管理員，以及組織 Confluence 網站的系統管理員。

## <a name="step-1-add-a-connector-in-the-microsoft-365-admin-center"></a>步驟 1：在Microsoft 365 系統管理中心中新增連接器

請遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-2-name-the-connection"></a>步驟 2：命名連線

請遵循一般 [設定指示](./configure-connector.md)。

## <a name="step-3-configure-the-connection-settings"></a>步驟 3：設定連線設定

### <a name="step-31-select-deployment-type"></a>步驟 3.1：選取部署類型

選 *取 [伺服器] 或 [資料中心* ] 選項以編制 Confluence 內部部署內容的索引，然後選取 [下一步]。

### <a name="step-32-enter-confluence-instance-url"></a>步驟 3.2：輸入 Confluence 實例 URL

若要連線到您的 Confluence 網站，請使用您的網站 URL。

### <a name="step-33-select-the-microsoft-graph-connector-agent"></a>步驟 3.3：選取 Microsoft Graph 連接器代理程式

從下拉式清單中選取連接器代理程式。 代理程式會安全地將 Confluence 內部部署內容傳送至 Microsoft Graph索引。

### <a name="step-34-select-authentication-type"></a>步驟 3.4：選取驗證類型

您可以選擇 [基本驗證] 或 [OAuth 1.0a] (建議) 向您的 Confluence 網站進行驗證。

>[!TIP]
>請確定服務帳戶具有您想要編制索引之 Confluence 內容的檢 **視存取權** 。

#### <a name="basic-authentication"></a>基本驗證

輸入服務帳戶的使用者名稱 (通常是電子郵件識別碼) 和密碼，以使用基本驗證進行驗證。

#### <a name="oauth-10a-recommended"></a>OAuth 1.0a (建議) 

產生公開/私密金鑰組，並在 Confluence 內部部署網站中建立應用程式連結，讓連接器代理程式可以存取實例。 若要深入瞭解，請參閱 [Atlassian 開發人員檔中](https://developer.atlassian.com/server/jira/platform/oauth/#step-1--configure-jira) 有關如何設定 OAuth 1.0a 的步驟 1。

#### <a name="step-341-generate-an-rsa-publicprivate-key-pair"></a>步驟 3.4.1 產生 RSA 公開/私密金鑰組

在內部部署機器終端機中執行下列 openssl 命令。

步驟 | 命令
--- | ---
產生 1024 位私密金鑰 |```openssl genrsa -out confluence_privatekey.pem 1024```
建立 X509 憑證 |```openssl req -newkey rsa:1024 -x509 -key confluence_privatekey.pem -out confluence_publickey.cer -days 365```
將私密金鑰 (PKCS8 格式) 解壓縮 `confluence_privatekey.pcks8` 至檔案 |```openssl pkcs8 -topk8 -nocrypt -in confluence_privatekey.pem -out confluence_privatekey.pcks8```
將公開金鑰從憑證擷取至 `confluence_publickey.pem` 檔案 |```openssl x509 -pubkey -noout -in confluence_publickey.cer > confluence_publickey.pem```

#### <a name="step-342-create-an-application-link"></a>步驟 3.4.2 建立應用程式連結

1. 在 Confluence 中，流覽至側邊窗格) > [**一般**  >  設定][應用程式 **連結**] (齒輪圖示的 [系統 **管理**]。

2. 在 [ **輸入您要連結的應用程式 URL** ] 文字方塊中，輸入任何 URL。 例如， `https://example.com` 然後選取 **[建立新連結]**。 忽略 *[未從您輸入的 URL 收到任何回應* ] 警告，然後選取 [ **繼續]**。

3. 在 [ **連結應用程式** ] 對話方塊的第一個畫面上，提供 [應用程式 **名稱** ]，然後選取 [ **一般應用程式** 類型]。 選取 [ **建立傳入連結] 複** 選框。 其他所有欄位皆為選用。 選取 **[繼續]**。

![[連結應用程式] 對話方塊](media/confluence-connector/confluence-onpremises-applications-link-1.png)

4. 在 [ **連結應用程式** ] 對話方塊的第二個畫面上，輸入範例用戶端的取用者詳細資料：

欄位 | 建議值
--- | ---
**取用者金鑰** | `OAuthkey`
**取用者名稱** | `Microsoft Graph Connector App`
**公開金鑰** | 從 `confluence_publickey.pem` *步驟 3.4.1* 產生的檔案複製公開金鑰，並將它貼到此欄位 (例如， `iuasge87awegrq3...`) 。

5. 選取 **[繼續]**。 成功建立之後，應用程式連結會顯示如下列畫面。

![連結應用程式建立後](media/confluence-connector/confluence-onpremises-applications-link-2.png)

#### <a name="step-343-enter-consumer-key-and-private-key-to-sign-in"></a>步驟 3.4.3 輸入取用者金鑰和私密金鑰以登入

在 Microsoft 365 系統管理中心 的連線建立組態助理中，輸入 *步驟 3.4.2* 期間建立的取用者 **金鑰**，以及 *步驟 3.4.1* 中檔案中的 **私密金鑰** `confluence_privatekey.pcks8` 。 在瀏覽器中啟用Microsoft 365 系統管理中心的快顯，然後選取 [**登入]**。

#### <a name="step-344-enter-verification-code-to-finish-sign-in"></a>步驟 3.4.4 輸入驗證碼以完成登入

在 [Confluence 登入] 畫面中，輸入服務帳戶認證。 成功登入之後，您會收到類似下列畫面的驗證碼。

![驗證碼](media/confluence-connector/confluence-onpremises-applications-link-3.png)

在連線建立設定助理中輸入 **驗證碼** ，然後選取 **[完成登入]**。 成功登入之後，選取 [ **下一步]**。

## <a name="step-4-select-properties"></a>步驟 4：選取屬性

在此步驟中，您可以從 Confluence 資料來源新增或移除可用的屬性。 Microsoft 365預設已經選取幾個屬性。

使用 Confluence 查詢語言 (CQL) 字串，您可以指定同步頁面的條件。 它就像 SQL **Select** 語句中的 **Where** 子句。 例如，您可以選擇只為過去兩年中修改的頁面編制索引。 若要瞭解如何建立您自己的查詢字串，請參閱 [使用 CQL 進行進階搜尋](https://developer.atlassian.com/server/confluence/advanced-searching-using-cql/)。 根據預設，連接器會編制所有頁面的索引。

>[!TIP]
>您可以使用 CQL 篩選來編制 **在特定時間之後修改的內容** 索引， *lastModified >= 「2018/12/31」*

使用 [預覽結果] 按鈕來驗證所選屬性和 CQL 字串的範例值。

## <a name="step-5-manage-search-permissions"></a>步驟 5：管理搜尋許可權

Confluence 內部部署連接器支援 **「所有人** 」或 **「僅限具有此資料來源存取權的人員」可見的搜尋許可權**。 如果您選擇 [ **所有人**]，已編制索引的資料會出現在所有使用者的搜尋結果中。 如果您選擇 **[僅限可存取此資料來源的人員**]，則已編制索引的資料會出現在可存取此資料來源之使用者的搜尋結果中。

在 Confluence 內部部署中，使用者和群組的安全性許可權是使用空間許可權和頁面限制來定義。 Confluence 內部部署連接器會套 *用*[內容限制 API](https://docs.atlassian.com/ConfluenceServer/rest/7.15.0/#api/content/{id}/restriction)所提供的有效許可權。

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

設定連接器時可以看到的常見錯誤及其可能的原因如下所示。

| 設定步驟 | 錯誤訊息 | 可能的原因 ()  |
| ------------ | ------------ | ------------ |
| 連線設定 | 要求格式不正確或不正確。 | 不正確的 Confluence 網站 URL |
| 連線設定 | 無法連線到 Confluence 網站的 Confluence 內部部署服務。 | 不正確的 Confluence 網站 URL |
| 連線設定 | 用戶端沒有執行動作的許可權。 | 為基本驗證提供的密碼無效 |
| 選取屬性 | 沒有預覽結果 | 檢查您的 CQL 查詢是否有效，並符合要編目的內容 |

## <a name="limitations"></a>限制

Confluence 內部部署連接器在其最新版本中具有下列已知限制：

* Confluence 內部部署連接器不會為部落格、附件檔案和批註編制索引。

---
title: 企業網站 Microsoft Graph 連接器
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
description: 設定 Microsoft Search 的企業網站 Graph 連接器
ms.openlocfilehash: d0a77bd7e85869935af7601be64146bd93b86886
ms.sourcegitcommit: 2032add1816919c2cbf6acf9fa7682e9ad36f859
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2022
ms.locfileid: "67461213"
---
<!---Previous ms.author: monaray --->

<!-- markdownlint-disable no-inline-html -->

# <a name="enterprise-websites-microsoft-graph-connector"></a>企業網站 Microsoft Graph 連接器

企業網站 Microsoft Graph 連接器可讓您的組織 **從公司擁有的網站** 為文章和內容編制索引。 設定連接器並從網站同步處理內容之後，使用者就可以從任何 Microsoft Search 用戶端搜尋該內容。

> [!NOTE]
> 請閱讀Microsoft 365 系統管理中心文章 [**中的設定 Microsoft Graph 連接器**](configure-connector.md)一文，以瞭解一般連接器設定指示。

本文適用于設定、執行及監視企業網站連接器的任何人。 它會補充一般設定程式，並顯示僅適用于企業網站連接器的指示。 本文也包含 [疑難排解的相關](#troubleshooting)資訊。

<!---## Before you get started-->

<!---Insert "Before you get started" recommendations for this data source-->

## <a name="step-1-add-a-connector-in-the-microsoft-365-admin-center"></a>步驟 1：在Microsoft 365 系統管理中心中新增連接器

請遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## <a name="step-2-configure-the-connection-settings"></a>步驟 2：設定連線設定

若要連線到您的資料來源，請填入網站的根 URL，然後選取結果的自訂垂直。 完成這項資訊之後，請選取 [測試連線] 以驗證您的設定。

### <a name="connection-id"></a>連線識別碼

此資料來源的唯一連接識別碼名稱。 若要變更此名稱，請移至 [進階設定]

### <a name="website-url"></a>網站 URL

指定您想要編目之網站的根目錄。 企業網站連接器會使用此 URL 作為起點，並遵循此 URL 中的所有連結進行編目。

> [!NOTE]
> 您可以在單一連線中為最多 20 個不同的網站 URL 編制索引。 在 [URL] 欄位中，輸入以逗號分隔的網站 URL (，) 。 例如，`https://www.contoso.com,https://www.contosoelectronics.com`。

### <a name="use-sitemap-for-crawling"></a>使用網站圖進行編目

選取時，連接器只會編目網站映射中所列的 URL。 如果未選取或找不到網站地圖，連接器會對網站根 URL 上找到的所有連結進行深層編目。

## <a name="step-2-advanced-settings"></a>步驟 2：進階設定

使用進階設定來啟用動態編目程式、選取編目模式，以及您想要使用的驗證類型：無、基本驗證、網站管理員或 OAuth 2.0 搭配 [Azure Active Directory (Azure AD) ](/azure/active-directory/)。

### <a name="dynamic-site-configuration"></a>動態網站設定

如果您的網站包含動態內容，例如，位於 Confluence 或 Unily 等內容管理系統中的網頁，您可以啟用動態編目程式。 若要開啟它，請選取 **[啟用動態網站的編目]**。 編目程式會先等候動態內容轉譯，再開始編目。

> [!div class="mx-imgBorder"]
> ![企業 Web 連線器的 [連線設定] 窗格螢幕擷取畫面。](media/enterprise-web-connector/connectors-enterpriseweb-connectionsettings-dynamicconfig-small.png)

除了核取方塊之外，還有三個選擇性欄位可供使用：

1. **DOM 就緒**：輸入編目程式應該使用的 DOM 元素，作為完整轉譯內容且應該開始編目的訊號。
1. **要新增的標頭**：指定編目程式在傳送該特定 Web URL 時應包含哪些 HTTP 標頭。 您可以為不同的網站設定多個標頭。 我們建議包含驗證權杖值。
1. **要略過的標頭**：指定任何應該從動態編目要求中排除的不必要標頭。

> [!NOTE]
> 只有代理程式編目模式才支援動態編目。

### <a name="crawl-mode-cloud-or-on-premises"></a>編目模式：雲端或內部部署

編目模式會決定您想要編制索引的網站類型，包括雲端或內部部署。 針對您的雲端網站，選取 **[雲端** ] 作為編目模式。

此外，連接器現在支援對內部部署網站進行編目。 若要存取內部部署資料，您必須先安裝並設定連接器代理程式。 若要深入瞭解，請參閱 [Microsoft Graph 連接器代理程式](./graph-connector-agent.md)。

針對您的內部部署網站，選取 **[代理** 程式] 作為編目模式，然後在 [ **內部部署代理** 程式] 欄位中，選擇您稍早安裝並設定的 Graph 連接器代理程式。  

### <a name="authentication"></a>驗證

**無** 不需要驗證

**基本** 需要使用者名稱和密碼。

搭配 [Azure AD](/azure/active-directory/)的 **OAuth 2.0** 需要資源識別碼、用戶端識別碼和用戶端密碼。 OAuth 2.0 僅適用于雲端模式。

資源識別碼、用戶端識別碼和用戶端密碼值將取決於您針對 Azure Active Directory (Azure AD) 型驗證的設定方式：

1. 如果您使用應用程式作為識別提供者和用戶端應用程式來存取網站，用戶端識別碼和資源識別碼將會是應用程式的應用程式識別碼，而用戶端密碼將會是您在應用程式中產生的密碼。
    
    > [!NOTE]
    > 如需將用戶端應用程式設定為身分識別提供者的詳細步驟，請參閱[快速入門：向Microsoft 身分識別平臺註冊應用程式和設定您的App Service或Azure Functions應用程式以使用 Azure AD 登入](/azure/app-service/configure-authentication-provider-aad)。

    設定用戶端應用程式之後，請務必前往應用程式的 [憑 **證&秘密** ] 區段來建立新的用戶端密碼。 複製頁面中顯示的用戶端密碼值，因為它不會再顯示。

    在下列螢幕擷取畫面中，如果您要自行建立應用程式，您可以看到取得用戶端識別碼、用戶端密碼及設定應用程式的步驟。
    
    * 品牌區段上的設定檢視：
    
      > [!div class="mx-imgBorder"]
      > [![顯示品牌頁面上 [設定] 區段的影像。 ](media/enterprise-web-connector//connectors-enterpriseweb-branding.png) ](media/enterprise-web-connector//connectors-enterpriseweb-branding.png#lightbox)
    
    * 驗證區段上的設定檢視：
    
      > [!div class="mx-imgBorder"]
      > [![顯示驗證頁面上設定區段的影像。 ](media/enterprise-web-connector/connectors-enterpriseweb-authentication.png) ](media/enterprise-web-connector/connectors-enterpriseweb-authentication.png#lightbox)
    
      > [!NOTE]
      > 您的網站中不需要有上述指定的重新導向 URI 路由。 只有當您在網站中使用 Azure 所傳送的使用者權杖進行驗證時，您才需要有路由。
    
    * 在 [基本資訊] 區段上檢視用戶端標識 **符** ：
    
      > [!div class="mx-imgBorder"]
      > [![顯示 [基本資訊] 區段上用戶端識別碼的影像。 ](media/enterprise-web-connector/connectors-enterpriseweb-clientapp-clientidresource-Id.png) ](media/enterprise-web-connector/connectors-enterpriseweb-clientapp-clientidresource-Id.png#lightbox)
    
    * 在 [憑 **證&秘密** ] 區段上檢視用戶端密碼：
    
      > [!div class="mx-imgBorder"]
      > [![顯示用戶端密碼的影像。 ](media/enterprise-web-connector/connectors-enterpriseweb-client-secret.png) ](media/enterprise-web-connector/connectors-enterpriseweb-client-secret.png#lightbox)
    
2. 如果您使用應用程式作為網站的識別提供者做為資源，而使用不同的應用程式來存取網站，則用戶端識別碼會是第二個應用程式的應用程式識別碼，而用戶端密碼將會是在第二個應用程式中設定的秘密。 不過，資源識別碼會是您第一個應用程式的識別碼。

    > [!NOTE]
    > 如需將用戶端應用程式設定為識別提供者的步驟，請參閱[快速入門：向Microsoft 身分識別平臺註冊](/azure/active-directory/develop/quickstart-register-app)應用程式和設定[您的App Service或Azure Functions應用程式以使用 Azure AD 登入](/azure/app-service/configure-authentication-provider-aad)。

    您不需要在此應用程式中設定用戶端密碼，但您必須在應用程式的 [ **應用程式角色** ] 區段中新增應用程式角色，稍後會指派給您的用戶端應用程式。 請參閱影像以瞭解如何新增應用程式角色。

    * 建立新的應用程式角色：
    
      > [!div class="mx-imgBorder"]
      > [![顯示建立應用程式角色選項的影像。 ](media/enterprise-web-connector/connectors-enterpriseweb-new-app-role.png) ](media/enterprise-web-connector/connectors-enterpriseweb-new-app-role.png#lightbox)
    
    * 編輯新的應用程式角色：
    
      > [!div class="mx-imgBorder"]
      > [![顯示編輯應用程式角色區段的影像。 ](media/enterprise-web-connector/connectors-enterpriseweb-new-app-role2.png) ](media/enterprise-web-connector/connectors-enterpriseweb-new-app-role2.png#lightbox)
    
      設定資源應用程式之後，請建立用戶端應用程式，並藉由在用戶端應用程式的 API 許可權中新增上述設定的應用程式角色，為其授與存取資源應用程式的許可權。 
    
      > [!NOTE]
      > 若要瞭解如何將許可權授與用戶端應用程式，請 [參閱快速入門：設定用戶端應用程式以存取 Web API](/azure/active-directory/develop/quickstart-configure-app-access-web-apis)。
    
    下列螢幕擷取畫面顯示將許可權授與用戶端應用程式的區段。
    
    * 新增許可權：
    
      > [!div class="mx-imgBorder"]
      > [![顯示新增許可權選項的影像。 ](media/enterprise-web-connector/connectors-enterpriseweb-adding-permissions.png) ](media/enterprise-web-connector/connectors-enterpriseweb-adding-permissions.png#lightbox)
    
    * 選取許可權：
    
      > [!div class="mx-imgBorder"]
      > [![顯示區段以選取 API 的影像。 ](media/enterprise-web-connector/connectors-enterpriseweb-adding-permissions2.png) ](media/enterprise-web-connector/connectors-enterpriseweb-adding-permissions2.png#lightbox)
    
    * 新增許可權：
 
      > [!div class="mx-imgBorder"]
      > [![顯示所選許可權的影像。 ](media/enterprise-web-connector/connectors-enterpriseweb-adding-permissions3.png) ](media/enterprise-web-connector/connectors-enterpriseweb-adding-permissions3.png#lightbox)
    
    指派許可權之後，您必須移至 [憑證&秘密] 區段，為此應用程式建立新的用戶端密碼。
    複製頁面中顯示的用戶端密碼值，因為它不會再次顯示。 使用此應用程式的應用程式識別碼作為用戶端識別碼、使用此應用程式的秘密作為用戶端密碼，並使用第一個應用程式的應用程式識別碼作為資源識別碼。

**SiteMinder** 需要格式正確的 URL、 ```https://custom_siteminder_hostname/smapi/rest/createsmsession``` 使用者名稱和密碼。

**Windows** 驗證只能在代理程式模式中使用。 它需要使用者名稱、網域和密碼。 您必須在 [使用者名稱] **欄位中** 提供使用者名稱和網域，格式如下：domain\username 或 username@domain。 密碼必須在 [ **密碼] 字** 段中輸入。 針對Windows 驗證，提供的使用者名稱也必須是安裝代理程式之伺服器中的系統管理員。

## <a name="step-2a-meta-tag-settings"></a>步驟 2a：中繼標籤設定

連接器會擷取根 URL 可能擁有的任何中繼標籤，並顯示它們。 您可以選取要包含哪些標籤以進行編目。 

:::image type="content" source="media/enterprise-web-connector/connectors-enterpriseweb-meta-tags-settings.png" alt-text="已選取作者、地區設定和其他標籤的元標記設定。":::

選取的中繼標記也會顯示在 [架構] 頁面上，您可以在其中進一步管理它們 (可查詢、可搜尋、可擷取、可精簡) 。

## <a name="step-2b-add-urls-to-exclude-optional-crawl-restrictions"></a>步驟 2b：新增 URL 以排除 (選擇性編目限制) 

有兩種方式可以防止頁面編目：不允許在robots.txt檔案中編目頁面，或將它們新增至排除清單。

### <a name="support-for-robotstxt"></a>支援robots.txt

連接器會檢查根網站是否有robots.txt檔案。 如果有的話，它會遵循並遵循該檔案中找到的指示。 如果您不想讓連接器編目網站上的特定頁面或目錄，請在robots.txt檔案的 「不允許」宣告中包含頁面或目錄。

### <a name="add-urls-to-exclude"></a>新增要排除的 URL

如果內容敏感或不值得編目，您可以選擇性地建立 **排除清單** ，以排除某些 URL 不進行編目。 若要建立排除清單，請流覽根 URL。 您可以在設定程式期間，將排除的 URL 新增至清單。

## <a name="step-3-assign-property-labels"></a>步驟 3：指派屬性標籤

您可以從選項功能表中選擇，將來源屬性指派給每個標籤。 雖然此步驟並非必要，但擁有某些屬性標籤可改善搜尋相關性，並確保使用者的搜尋結果更精確。

## <a name="step-4-manage-schema"></a>步驟 4：管理架構

在 [ **管理架構** ] 畫面上，您可以變更架構屬性 (選項為 **[查詢**]、[ **搜尋**]、[擷 **取**] 和 [ **精簡**) 與屬性相關聯、新增選擇性別名，然後選擇 **Content** 屬性。

## <a name="step-5-manage-search-permissions"></a>步驟 5：管理搜尋許可權

企業網站連接器只支援每個人都能看見的搜尋權 **限**。 索引資料會出現在搜尋結果中，且組織中的所有使用者都可以看到。

## <a name="step-6-set-the-refresh-schedule"></a>步驟 6：設定重新整理排程

企業網站連接器僅支援完整重新整理。 這表示連接器會在每次重新整理期間重新編目所有網站的內容。 若要確定連接器有足夠的時間來編目內容，建議您設定大型重新整理排程間隔。 我們建議您在一到兩周之間排程重新整理。

## <a name="step-7-review-connection"></a>步驟 7：檢閱連線

請遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## <a name="troubleshooting"></a>疑難排解

讀取網站的內容時，搜耙可能會遇到一些來源錯誤，這些錯誤是由下列詳細的錯誤碼所表示。 若要取得錯誤類型的詳細資訊，請在選取連線之後移至 **錯誤詳細** 資料頁面。 選取 **錯誤碼** 以查看更詳細的錯誤。 另請參閱 [監視您的連線](./manage-connector.md) 以深入瞭解。

 詳細的錯誤碼 | 錯誤訊息
 --- | ---
 6001 | 無法連線到嘗試編制索引的網站
 6005 | 嘗試編制索引的來源頁面已根據robots.txt組態封鎖。
 6008 | 無法解析 DNS
 6009 | 如需 HTTP 404、408) 以外的所有用戶端錯誤 (，請參閱 HTTP 4xx 錯誤碼以取得詳細資料。
 6013 | 找不到嘗試編制索引的來源頁面。  (HTTP 404 錯誤) 
 6018 | 來源頁面沒有回應，且要求已逾時。 (HTTP 408 錯誤) 
 6021 | 嘗試編制索引的來源頁面在頁面上沒有文字內容。
 6023 | 不支援嘗試編制索引的來源頁面， (不支援 HTML 頁面) 
 6024 | 嘗試編制索引的來源頁面具有不支援的內容。

* 當因網路問題而無法連線到資料來源，或資料來源本身遭到刪除、移動或重新命名時，就會發生錯誤 6001-6013。 檢查提供的資料來源詳細資料是否仍然有效。
* 當資料來源在頁面上包含非文字內容，或頁面不是 HTML 時，就會發生錯誤 6021-6024。 檢查資料來源，並在排除清單中新增此頁面，或忽略錯誤。

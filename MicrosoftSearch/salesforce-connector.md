---
title: Microsoft 搜尋的 Salesforce Graph 連接器
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
description: 設定 Microsoft 搜尋的 Salesforce Graph 連接器
ms.openlocfilehash: f2e7eb500e83ba996122a78a9593fca475d58317
ms.sourcegitcommit: 2fc1bc29249d6342a10d85bca291a1bec8bc125c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2022
ms.locfileid: "62492911"
---
<!---Previous ms.author: rusamai --->

# <a name="salesforce-graph-connector"></a>Salesforce Graph 連接器

salesforce Graph connector 可讓您的組織為您的 Salesforce 實例中的連絡人、機會、潛在客戶、案例及帳戶物件編制索引。 從 Salesforce 設定連接器和索引內容之後，使用者可以從任何 Microsoft 搜尋用戶端搜尋這些專案。

> [!NOTE]
> 請閱讀 [**Graph 連接器**](configure-connector.md)文章的設定，以瞭解一般 Graph 連接器設定指示。

本文適用于任何設定、執行及監視 Salesforce Graph 連接器的人員。 它會補充一般設定程式，並顯示只適用于 Salesforce Graph 連接器的指示。 本文也包含 [限制](#limitations)的相關資訊。

>[!IMPORTANT]
>Salesforce Graph 連接器目前支援暑假 ' 19 或更新版本。

## <a name="before-you-get-started"></a>開始之前

若要連線到您的 Salesforce 實例，您需要您的 Salesforce 實例 URL、用戶端識別碼，以及 OAuth 驗證的用戶端密碼。 下列步驟會說明您或您的 Salesforce 管理員如何從您的 Salesforce 帳戶取得此資訊：

- 登入您的 Salesforce 實例，然後移至 [設定]

- 流覽至應用程式-> 應用程式管理員。

- 選取 [ **新增已連線的應用程式**]。

- 完成 API 區段，如下所示：

    - 選取 [**啟用 Oauth 設定**] 核取方塊。

    - 指定回撥 URL 做為： [https://gcs.office.com/v1.0/admin/oauth/callback](https://gcs.office.com/v1.0/admin/oauth/callback)

    - 選取這些必要的 OAuth 範圍。

        - 存取及管理您的資料 (api) 

        - 隨時以您的名義執行要求 (refresh_token、offline_access) 

    - 選取 [ **需要 web 伺服器流程的機密**] 核取方塊。

    - 儲存應用程式。
    
      > [!div class="mx-imgBorder"]
      > ![在系統管理員輸入上述所有必要設定之後，Salesforce 實例中的 API 區段。](media/salesforce-connector/sf1.png)

- 複製使用者金鑰和使用者密碼。 當您在 Microsoft 365 admin 入口網站中設定 Graph 連接器的連線設定時，會使用此資訊做為用戶端識別碼和用戶端密碼。

  > [!div class="mx-imgBorder"]
  > ![在 admin 提交所有必要設定之後，由 Salesforce 實例中 API 區段所傳回的結果。 使用者機碼位於左欄的頂端，且使用者機密位於右列頂端。](media/salesforce-connector/clientsecret.png)
  
- 在關閉您的 Salesforce 實例之前，請遵循下列步驟，以確保重新整理權杖不會到期：
    - 移至應用程式-> 應用程式管理員
    - 找到您已建立的應用程式，然後選取右邊的下拉式清單。 選取 [ **管理**
    - 選取 **編輯原則**
    - 針對重新整理權杖原則，選取重新整理 **權杖有效直到撤銷**

  > [!div class="mx-imgBorder"]
  > ![選取名為 "Refresh token 有效直到撤銷" 的重新整理權杖原則。](media/salesforce-connector/oauthpolicies.png)

您現在可以使用[Microsoft 365 系統管理中心](https://admin.microsoft.com/)完成 Graph 連接器的其餘設定程式。

## <a name="step-1-add-a-graph-connector-in-the-microsoft-365-admin-center"></a>步驟1：在 Microsoft 365 系統管理中心中新增 Graph 連接器

遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## <a name="step-2-name-the-connection"></a>步驟2：命名連線

遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## <a name="step-3-configure-the-connection-settings"></a>步驟3：設定連接設定

若為實例 URL，請使用 HTTPs：//[網域]. my .com，其中網域是您組織的 Salesforce 網域。

輸入您從 Salesforce 實例取得的用戶端識別碼和用戶端密碼，然後選取 [登入]。

您第一次嘗試使用這些設定登入時，您會看到一個快顯視窗，要求您使用您的系統管理員使用者名稱和密碼登入 Salesforce。 下列螢幕擷取畫面顯示快顯功能表。 輸入您的認證，然後選取 [登入]。

  ![登入快顯視窗要求輸入使用者名稱和密碼。](media/salesforce-connector/sf4.png)

  >[!NOTE]
  >如果快顯視窗未出現，則可能是您的瀏覽器遭到封鎖，所以您必須允許快顯視窗和重新導向。

搜尋綠色橫幅（如下列螢幕擷取畫面所示）中的 [連線成功]，以檢查連線是否成功。

  > [!div class="mx-imgBorder"]
  > ![成功登入的螢幕擷取畫面。 [連線成功] 的綠色旗標位於您的 Salesforce 實例 URL 的欄位底下。](media/salesforce-connector/salesforce-connector-connection-settings.png)

## <a name="step-4-select-properties"></a>步驟4：選取屬性

選取您要連接線進行編目及包含在搜尋結果中的 Salesforce 物件。 如果選取 [連絡人]，系統也會自動選取帳戶。

>[!NOTE]
>如果欄位具有欄位層級安全性 (FLS) 設定設定檔，連接器將不會為該 Salesforce 組織中的任何設定檔攝取該欄位。因此，使用者將無法搜尋這些欄位的值，也不會顯示在結果中。

## <a name="step-5-manage-search-permissions"></a>步驟5：管理搜尋許可權

您必須選擇哪一使用者會看到來自此資料來源的搜尋結果。 如果只允許特定 Azure Active Directory (Azure AD) 或非 Azure AD 使用者看到搜尋結果，請確定您對應的是識別碼。

### <a name="step-5a-select-permissions"></a>步驟5：選取許可權

您可以選擇從您的 Salesforce 實例中 (ACLs) 來攝取存取控制清單，或允許組織中的每個人都看到來自此資料來源的搜尋結果。 ACLs 可以包含 Azure Active Directory (AAD) 身分 (的使用者，Azure AD 從) 到 Salesforce Azure AD 的使用者、非 (的身分識別，Azure AD 在) 中具有對應身分身分識別的原生使用者，或兩者。

>[!NOTE]
>如果您使用的協力廠商身分識別提供者（如 Ping 識別碼或 secureAuth），則應該選取「非 AAD」做為身分識別類型。

> [!div class="mx-imgBorder"]
> ![選取由系統管理員已完成的 [許可權] 畫面。管理員已選取 [只有存取此資料來源的人員] 選項，而且已從識別類型的下拉式功能表中選取「AAD」。](media/salesforce-connector/sf6.png)

如果您選擇從您的 Salesforce 實例中攝取 ACL，並為身分識別類型選取 [非 AAD]，請參閱[對應您的非 Azure AD](map-non-aad.md)身分識別，以取得對應身分識別的指示。

### <a name="step-5b-map-aad-identities"></a>步驟5： b：對應 AAD 身分識別

如果您選擇從 Salesforce 實例中攝取一個 ACL，並為身分識別類型選取「AAD」，請參閱[對應您的 Azure AD](map-aad.md)身分識別，以取得對應身分識別的指示。 若要瞭解如何設定 Salesforce 的 Azure AD SSO，請參閱本[教學](/azure/active-directory/saas-apps/salesforce-tutorial)課程。

### <a name="apply-user-mapping-to-sync-your-salesforce-identities-to-azure-ad-identities"></a>套用使用者對應，將您的 Salesforce 身分識別同步處理 Azure AD 身分識別

在此影片中，您可以看到對您的 salesforce 實例進行驗證的程式、將非 Azure Active Directory 身分同步處理至您的 Azure Active Directory 身分識別，以及套用適當的安全性 trimmings 至您的 salesforce 專案。

> [!VIDEO https://www.youtube-nocookie.com/embed/SZYiFxZMKcM]

## <a name="step-6-assign-property-labels"></a>步驟6：指派屬性標籤

您可以從選項的功能表中選擇，將 source 屬性指派給每個標籤。 這個步驟不是必要的，具有一些屬性標籤會提升搜尋相關性，並確保使用者的更好搜尋結果。 根據預設，有些標籤（如 "Title"、"URL"、"CreatedBy"、"LastModifiedBy"）已被指派來源屬性。

## <a name="step-7-manage-schema"></a>步驟7：管理架構

您可以選取應該編制索引的來源屬性，使其顯示在搜尋結果中。 依預設，連接嚮導會根據一組來源屬性選取搜尋架構。 您可以在 [搜尋架構] 頁面中選取每個屬性和屬性的核取方塊，以加以修改。 搜尋架構屬性包括搜尋、查詢、檢索及精煉。
精煉功能可讓您定義以後可用作自訂精簡器或篩選搜尋體驗的屬性。  

> [!div class="mx-imgBorder"]
> ![選取每個來源屬性的架構。 選項包括查詢、搜尋、檢索及精煉。](media/salesforce-connector/sf9.png)

## <a name="step-8-set-the-refresh-schedule"></a>步驟8：設定重新整理排程

Salesforce 連接器只支援目前完全編目的重新整理排程。

>[!IMPORTANT]
>完整編目會找出先前同步處理至 Microsoft 搜尋索引的已刪除物件和使用者。

建議的排程為一周完整編目。

## <a name="step-9-review-connection"></a>步驟9：檢查連線

遵循一般 [設定指示](./configure-connector.md)。

>[!TIP]
>**預設結果類型**
>* 在發佈連接器之後，Salesforce 連接器會自動註冊 [結果類型](./customize-search-page.md#step-2-create-result-types) 。 結果類型會根據在步驟3中選取的欄位，使用動態產生的 [結果版面](./customize-results-layout.md) 配置。
>* 您可以流覽至 [Microsoft 365 系統管理中心](https://admin.microsoft.com)中的 [**結果類型**](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/resulttypes)來管理結果類型。 預設結果類型將命名為 " `ConnectionId` default"。 例如，如果您的連線識別碼為 `Salesforce` ，您的結果版面配置將會命名為： "SalesforceDefault"
>* 此外，您也可以視需要選擇建立您自己的結果類型。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

<!---## Troubleshooting-->
<!---Insert troubleshooting recommendations for this data source-->

## <a name="limitations"></a>限制

- Graph 連接器目前不支援 Apex 基礎、區域型共用及從 Salesforce 使用個人群組共用。
- Graph 連接器所使用的 Salesforce API 有已知的缺陷，在此情況下，潛在客戶的私人組織範圍預設值目前不會生效。  
- 如果欄位具有欄位層級安全性 (FLS) 設定設定檔，Graph 連接器將不會為該 Salesforce 組織中的任何設定檔攝取該欄位。因此，使用者將無法搜尋這些欄位的值，也不會顯示在結果中。  
- 在 [管理架構] 畫面中，這些通用的標準屬性名稱會列出一次，這些選項為 **查詢**、 **搜尋**、 **檢索** 及 **精煉**，並套用至 all 或 none。
    - 姓名
    - URL
    - 描述
    - 傳真
    - Phone
    - MobilePhone
    - 電子郵件
    - 類型
    - 標題
    - AccountId
    - AccountName
    - AccountUrl
    - AccountOwner
    - AccountOwnerUrl
    - 擁有者
    - OwnerUrl
    - CreatedBy
    - CreatedByUrl
    - LastModifiedBy
    - LastModifiedByUrl
    - LastModifiedDate
    - ObjectName

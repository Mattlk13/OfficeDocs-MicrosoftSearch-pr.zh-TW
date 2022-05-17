---
title: 適用于 Microsoft 搜尋 的 Azure Data Lake Microsoft Graph連接器
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
description: 設定適用于 Microsoft 搜尋 的 Azure Data Lake Storage Gen2 Microsoft Graph 連接器
ms.openlocfilehash: d3c3799c8482a00f84ca6ad5d16ed45b8bad0235
ms.sourcegitcommit: 6ff032e46055eacf0f7f77c753965b6433f50117
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/17/2022
ms.locfileid: "65442529"
---
<!---Previous ms.author: monaray --->

# <a name="azure-data-lake-storage-gen2-microsoft-graph-connector"></a>Azure Data Lake Storage Gen2 Microsoft Graph 連接器

Azure Data Lake Storage Gen2 Microsoft Graph 連接器可讓組織中的使用者搜尋儲存在[Azure Blob 儲存體](/azure/storage/blobs/storage-blobs-introduction)和[Azure Data Lake Gen 2 儲存體](/azure/storage/blobs/data-lake-storage-introduction)帳戶中的檔案。

> [!NOTE]
> 請閱讀 [**設定您的 Microsoft Graph 連接器**](configure-connector.md)一文，以瞭解一般連接器設定指示。

本文適用于設定、執行及監視Azure Data Lake Storage Gen2連接器的任何人。 它會補充一般設定程式，並顯示僅適用于Azure Data Lake Storage Gen2連接器的指示。 本文也包含限制 [的相關](#limitations)資訊。

在本文中，我們會使用 *Azure 儲存體* 作為 [Azure Blob 儲存體](/azure/storage/blobs/storage-blobs-introduction)和 [Azure Data Lake Gen 2 儲存體](/azure/storage/blobs/data-lake-storage-introduction)的泛型詞彙。

## <a name="step-1-add-a-connector-in-the-microsoft-365-admin-center"></a>步驟 1：在Microsoft 365 系統管理中心中新增連接器

請遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## <a name="step-2-name-the-connection"></a>步驟 2：命名連線

請遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## <a name="step-3-configure-the-connection-settings"></a>步驟 3：設定連線設定

輸入您的主要儲存體連接字串。 需要此字串才能允許存取您的儲存體帳戶。 若要尋找您的連接字串，請移至 [Azure 入口網站](https://ms.portal.azure.com/#home)，並流覽至相關Azure 儲存體帳戶的 **[金鑰**] 區段。

如果您不想在主要儲存體連接字串) 中提供 **AccountKey** (參數，請為下列角色授與 Microsoft Graph 連接器服務的存取權：

* 儲存體 Blob 資料讀取器
* 儲存體佇列資料參與者
* 儲存體 Blob 委派者

流覽至Azure 儲存體帳戶的 **[存取控制**] 索引標籤，並遵循該處的指示來授與下列應用程式的存取權：

* **第一方應用程式識別碼：** 56c1da01-2129-48f7-9355-af6d59d42766
* **第一方應用程式名稱：** Graph連接器服務

### <a name="storage-account-and-queue-notifications-optional"></a>儲存體帳戶和佇列通知 (選擇性) 

未來可能會新增在 Graph 連接器服務中即時處理變更的支援。 在此情況下，我們將監視Azure 儲存體佇列中儲存的變更通知。 您必須在與Azure 儲存體帳戶相同的帳戶中建立佇列。

建立佇列之後，請移至佇列頁面上的 [ **事件** ] 索引標籤，以設定 **事件訂閱**。 選擇佇列將接收的所有 Blob 事件，並將佇列連線到Azure 儲存體帳戶。

### <a name="test-the-connection"></a>測試連線

按一下 [測試連線] 按鈕來 **測試連線**

> [!NOTE]
> **測試連線** 必須成功，您才能移至下一個組態區段。 已啟用 ADLS gen 2 的儲存體帳戶 **至少必須** 有一個容器 **和** 一個檔案， **測試聯** 機才能成功。 如果內容不存在，將會引發連線錯誤。

## <a name="step-4-assign-property-labels"></a>步驟 4：指派屬性標籤

您可以從選項功能表中選擇，將來源屬性指派給每個標籤。 雖然此步驟並非必要，但擁有某些屬性標籤可改善搜尋相關性，並確保使用者的搜尋結果更好。

## <a name="step-5-manage-schema"></a>步驟 5：管理架構

在 [ **管理架構** ] 畫面上，您可以變更與屬性相關聯的架構屬性，這些選項為 **[查詢**]、[ **搜尋**]、[擷 **取**] 和 [ **精簡]**。 您也可以新增選擇性別名，然後選擇 **Content** 屬性。

## <a name="step-6-manage-search-permissions"></a>步驟 6：管理搜尋許可權

### <a name="azure-data-lake-gen-2"></a>Azure Data Lake Gen 2

您可以選擇從[Azure Data Lake Gen 2](/azure/storage/blobs/data-lake-storage-introduction)儲存體 帳戶擷取存取控制清單 (ACL) 。 設定這些搜尋許可權時，會根據登入Azure Active Directory使用者的權[限](/azure/active-directory/)來修剪搜尋內容。 或者，您可以選擇讓組織中的每個人都能看見從儲存體帳戶編制索引的所有內容。 在此情況下，組織中的每個人都可以存取儲存體帳戶中的所有資料。

Azure Data Lake Storage Gen2連接器支援 **每個人都** 能看見的搜尋許可權，或 **只支援具有此資料來源存取權的人員**。 組織中可存取每個專案的使用者，可以看見出現在搜尋結果中的索引資料。

### <a name="azure-blob-storage"></a>Azure Blob 儲存體

若要連線到[Azure Blob 儲存體](/azure/storage/blobs/storage-blobs-introduction)，您組織中的每個人都可以看到從已設定來源編制索引的所有內容。 Azure Blob 儲存體中的 Blob 層級不支援存取控制清單。

## <a name="step-7-set-the-refresh-schedule"></a>步驟 7：設定重新整理排程

在 [**重新整理設定**] 畫面上，您可以設定累加編目間隔和完整編目間隔。 Azure Data Lake Storage Gen2連接器的預設間隔為 15 分鐘，累加編目為 15 分鐘，完整編目為一周。

## <a name="step-8-review-connection"></a>步驟 8：檢閱連線

請遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

<!---## Troubleshooting-->
<!---Insert troubleshooting recommendations for this data source-->

## <a name="limitations"></a>限制

Azure Blob 儲存體的已發行連線無法針對Azure Data Lake Storage Gen2來源重新設定，相反地。 在這種情況下，建議您設定新的連線。

此外，檔案的大小必須是 4 MB 或更少，才能進行編目。 目前支援的檔案類型如下：

* Word (docx、.docm、.dotx、.dotm) 
* PowerPoint (.pptm、.pptx、.potm、.potx、.ppam、.ppsm、.ppsx) 
* Excel (.xlsx、.xlsm) 
* 舊版Office格式 (.doc、.dot 等) 
* 文字 (.txt) 
* HTML
* PDF

不支援影像 (.jpg、.bmp等二進位檔案) 。 例如，如果.docx檔案只包含影像，可能會因為未傳回任何內容而略過。

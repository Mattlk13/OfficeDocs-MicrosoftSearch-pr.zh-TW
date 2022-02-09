---
title: Azure Data Lake Graph connector for Microsoft 搜尋
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
description: 為 Microsoft 搜尋設定 Azure Data Lake 儲存體 Gen2 Graph connector
ms.openlocfilehash: d9df82addafe6d112e2306e76dd73f522da57b15
ms.sourcegitcommit: 2fc1bc29249d6342a10d85bca291a1bec8bc125c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2022
ms.locfileid: "62491994"
---
<!---Previous ms.author: monaray --->

# <a name="azure-data-lake-storage-gen2-graph-connector"></a>Azure Data Lake 儲存體 Gen2 Graph connector

azure data lake 儲存體 Gen2 Graph connector 可讓組織中的使用者搜尋[azure Blob 儲存體](/azure/storage/blobs/storage-blobs-introduction)和[azure Data Lake Gen 2 儲存體](/azure/storage/blobs/data-lake-storage-introduction)帳戶中儲存的檔案。

> [!NOTE]
> 請閱讀 [**設定 Graph 連接器**](configure-connector.md)文章，以瞭解一般 Graph 連接器設定指示。

本文適用于設定、執行及監視 Azure Data Lake 儲存體 Gen2 connector 的任何人。 它會補充一般安裝程式，並顯示只適用于 Azure Data Lake 儲存體 Gen2 connector 的指令。 本文也包含 [限制](#limitations)的相關資訊。

在本文中，我們使用 *Azure 儲存體* 作為 [azure Blob 儲存體](/azure/storage/blobs/storage-blobs-introduction)和 [azure Data Lake Gen 2 儲存體](/azure/storage/blobs/data-lake-storage-introduction)的一般字詞。

## <a name="step-1-add-a-graph-connector-in-the-microsoft-365-admin-center"></a>步驟1：在 Microsoft 365 系統管理中心中新增 Graph 連接器

遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## <a name="step-2-name-the-connection"></a>步驟2：命名連線

遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## <a name="step-3-configure-the-connection-settings"></a>步驟3：設定連接設定

輸入您的主要儲存體連接字串。 此字串是允許存取您的儲存體帳戶所需的字串。 若要尋找您的連接字串，請移至 [Azure 入口網站](https://ms.portal.azure.com/#home)並流覽至相關 Azure 儲存體帳戶的 [機 **碼**] 區段。

如果您不想要在主要儲存連接字串) 中提供 **AccountKey** (參數，請將存取權授與下列角色的 Graph 連接器服務：

* 儲存體 Blob 資料讀取器
* 儲存體佇列資料參與者
* 儲存體 Blob Delegator

流覽至您 Azure 儲存體帳戶的 [**存取控制**] 索引標籤，然後依照其中的指示授與下列應用程式的存取權：

* **第一方應用程式 ID:** 56c1da01-2129-48f7-9355-af6d59d42766
* **第一方應用程式名稱：** Graph 連接器服務

### <a name="storage-account-and-queue-notifications-optional"></a>儲存體帳戶和佇列通知 (選用) 

在未來可能會新增 Graph 連接器服務中即時處理變更的支援。 在此情況下，我們會監視儲存在佇列中 Azure 儲存體變更通知。 您必須使用與 Azure 儲存體帳戶相同的帳戶建立佇列。

建立佇列之後，請移至佇列頁面上的 [ **事件** ] 索引標籤，以設定 **事件訂閱**。 選擇佇列將要接收的所有 Blob 事件，並將該佇列連接至 Azure 儲存體帳戶。

## <a name="step-4-assign-property-labels"></a>步驟4：指派屬性標籤

您可以從選項的功能表中選擇，將 source 屬性指派給每個標籤。 這個步驟不是必要的，具有一些屬性標籤會提升搜尋相關性，並確保使用者的更好搜尋結果。

## <a name="step-5-manage-schema"></a>步驟5：管理架構

在 [ **管理架構** ] 畫面上，您可以變更與屬性相關聯的架構屬性、選項為 **查詢**、 **搜尋**、 **檢索** 及 **精煉**。 您也可以新增選擇性別名，並選擇 **Content** 屬性。

## <a name="step-6-manage-search-permissions"></a>步驟6：管理搜尋許可權

### <a name="azure-data-lake-gen-2"></a>Azure Data Lake Gen 2

您可以選擇從您的[Azure Data Lake Gen 2 儲存體](/azure/storage/blobs/data-lake-storage-introduction)帳戶中 (ACLs) 上插入存取控制清單。 當您設定這些搜尋許可權時，會根據[Azure Active Directory](/azure/active-directory/)使用者登入的許可權來裁切搜尋內容。 或者，您也可以選擇讓組織中的所有人都可以看到從您的儲存體帳戶索引的所有內容。 在此情況下，您組織中的每個人都可以存取您儲存體帳戶中的所有資料。

Azure Data Lake 儲存體 Gen2 Graph connector 支援 **所有人都** 可以看到的搜尋許可權，或是 **只有存取此資料來源的人員**。 可以存取每個專案的組織中的使用者看不見搜尋結果中顯示的索引資料。

### <a name="azure-blob-storage"></a>Azure Blob 儲存體

若要連線至[Azure Blob 儲存體](/azure/storage/blobs/storage-blobs-introduction)，您組織中的所有人都會看到所有從設定之來源編制索引的內容。 Azure Blob 儲存體的 Blob 層級不支援存取控制清單。

## <a name="step-7-set-the-refresh-schedule"></a>步驟7：設定重新整理排程

在 [重新整理 **設定**] 畫面上，您可以設定增量編目間隔和完整編目間隔。 Azure Data Lake 儲存體 Gen2 連接器的預設間隔是15分鐘的增量編目，而一周用於完整編目。

## <a name="step-8-review-connection"></a>步驟8：檢查連線

遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

<!---## Troubleshooting-->
<!---Insert troubleshooting recommendations for this data source-->

## <a name="limitations"></a>限制

無法針對 Azure Data Lake 儲存體 Gen2 來源及另一種方式，重新設定 Azure Blob 儲存體的已發佈連線。 在這種情況下，建議您設定新的連線。

此外，檔案的大小必須為 4 MB 或更少的時間，才能進行編目。 目前支援的檔案類型包括：

* Word (.docx、.docm、dotx、normal.dotm) 
* PowerPoint ( pptm、.pptx、potm、potx、ppam、ppsm、. ppsx) 
* Excel (.xlsx xlsm) 
* 舊版 Office 格式 (.doc、.dot 等 ) 
* 文字 (.txt) 
* HTML
* PDF

不支援諸如影像 (.jpg、.bmp 等的二進位檔案 ) 。 例如，如果 .docx 檔只包含影像，它可能會略過，因為它未傳回任何內容。
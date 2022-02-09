---
title: Microsoft 搜尋的 Oracle SQL Graph 連接器
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
ROBOTS: NoIndex
description: 為 Microsoft 搜尋設定 Oracle SQL Graph 連接器。
ms.openlocfilehash: 5efc834c0c393094114f7ea81741ee1a0632b020
ms.sourcegitcommit: 2fc1bc29249d6342a10d85bca291a1bec8bc125c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2022
ms.locfileid: "62489881"
---
<!---Previous ms.author:vivg --->

# <a name="oracle-sql-graph-connector"></a>Oracle SQL Graph 連接器

Oracle SQL Graph 連接器可讓您的組織探索內部部署 Oracle 資料庫中的資料並為其編制索引。 連接器會將指定的內容索引至 Microsoft 搜尋。 若要讓索引保持在最新的來來源資料中，它支援定期完整和累加編目。 透過 Oracle SQL 連接器，您也可以限制特定使用者對搜尋結果的存取。

> [!NOTE]
> 請閱讀 [**Graph 連接器**](configure-connector.md)文章的設定，以瞭解一般 Graph 連接器設定指示。

本文適用于設定、執行及監視 Oracle SQL Graph 連接器的任何人。 它會補充一般設定程式，並顯示只適用于 Oracle SQL Graph 連接器的指示。 本文也包含 [疑難排解](#troubleshooting) 及 [限制](#limitations)的相關資訊。

## <a name="before-you-get-started"></a>開始之前

### <a name="install-the-graph-connector-agent"></a>安裝 Graph 連接器代理程式

為了存取您的內部部署協力廠商資料，您必須安裝及設定 Graph 連接器代理程式。 請參閱[Install the Graph connector agent](graph-connector-agent.md)以深入瞭解。  

## <a name="step-1-add-a-graph-connector-in-the-microsoft-365-admin-center"></a>步驟1：在 Microsoft 365 系統管理中心中新增 Graph 連接器

遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## <a name="step-2-name-the-connection"></a>步驟2：命名連線

遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## <a name="step-3-configure-the-connection-settings"></a>步驟3：設定連接設定

若要將您的 Oracle SQL 連接器連線至資料來源，您必須設定要編目的資料庫伺服器和內部部署 Graph 連接器代理程式。 然後，您就可以使用必要的驗證方法來連接至資料庫。

對於 Oracle SQL 連接器，您必須指定主機名稱、埠和服務 (資料庫) 名稱，以及偏好的驗證方法、使用者名稱和密碼。

> [!NOTE]
> 您的資料庫必須執行 Oracle 資料庫的11g 或更新版本，連接器才能夠連線。 此連接器支援在 Windows、Linux 和 Azure VM 平臺上裝載的 Oracle 資料庫。

若要搜尋資料庫內容，您必須在設定連接器時指定 SQL 查詢。 這些 SQL 查詢必須針對所有要編制索引的資料庫資料行命名 (也就是 [來源屬性]) ，包括要取得所有欄所需執行的任何 SQL 聯接。 若要限制存取搜尋結果，您必須在設定連接器時，指定 (ACLs) SQL 查詢中的存取控制清單。

## <a name="step-3a-full-crawl-required"></a>步驟3a：必要的完整編目 () 

在這個步驟中，您會設定執行資料庫完整編目的 SQL 查詢。 完整編目會選取所有欄或屬性，以選取 [ **查詢**]、[ **搜尋**] 或 [ **取得**] 選項。 您也可以指定 ACL 欄，以限制搜尋結果對特定使用者或群組的存取。

> [!Tip]
> 若要取得所需的所有欄，您可以加入多個表格。

![腳本顯示 OrderTable 及 AclTable，具有範例屬性。](media/MSSQL-fullcrawl.png)

### <a name="select-data-columns-required-and-acl-columns-optional"></a> (必要) 和 ACL 欄 (選用) 選取資料欄位

這個範例會示範五個數據列的選取範圍，其中保留搜尋的資料：「訂單」、「OrderTitle」、OrderDesc、CreatedDateTime 及 IsDeleted。 若要設定每個資料列的查看許可權，您可以選擇性地選取下列 ACL 欄： AllowedUsers、AllowedGroups、DeniedUsers 及 DeniedGroups。 對於所有的資料行，您可以選取要 **查詢**、 **搜尋** 或 **檢索** 的選項。

選取下列範例查詢所示的資料行： `SELECT OrderId, OrderTitle, OrderDesc, AllowedUsers, AllowedGroups, DeniedUsers, DeniedGroups, CreatedDateTime, IsDeleted`

若要管理搜尋結果的存取權，您可以在查詢中指定一或多個 ACL 欄。 SQL 連接器可讓您控制每個記錄層級的存取。 您可以選擇對資料表中的所有記錄使用相同的存取控制。 如果 ACL 資訊儲存在不同的資料表中，您可能必須在查詢中使用這些資料表進行聯接。

在上述查詢中使用每個 ACL 欄的描述如下。 下列清單說明四種 **存取控制機制**。

* **AllowedUsers**：此選項會指定可以存取搜尋結果的使用者 IDs 清單。 在下列範例中，使用者清單為： john@contoso.com、keith@contoso.com 和 lisa@contoso.com 只有具有「訂單 Id」的記錄存取權 = 12。
* **AllowedGroups**：此選項會指定可以存取搜尋結果的使用者群組。 在下列範例中，group sales-team@contoso.com 只會具有「訂單 Id = 12」的記錄存取權。
* **DeniedUsers**：此選項會 **指定沒有搜尋** 結果存取權的使用者清單。 在下列範例中，使用者 john@contoso.com 及 keith@contoso.com 無法存取具有「訂單 Id」的記錄，而其他所有人都可以存取這筆記錄。
* **DeniedGroups**：此選項會 **指定沒有搜尋** 結果存取權的使用者群組。 在下列範例中，群組 engg-team@contoso.com 及 pm-team@contoso.com 沒有具有「訂單 Id」的記錄存取權，而其他所有人都可以存取這筆記錄。  

![使用範例屬性顯示 OrderTable 及 AclTable 的範例資料。](media/MSSQL-ACL1.png)

### <a name="supported-data-types"></a>支援的資料類型

下表摘要 Oracle SQL 連接器所支援的資料類型。 該表也會摘要列出支援的 SQL 資料類型的索引資料類型。 若要深入瞭解 Microsoft Graph 連接器支援的索引資料類型，請參閱[屬性資源類型](/graph/api/resources/property?preserve-view=true&view=graph-rest-beta#properties)的檔。

| 類別 | 來源資料類型 | 索引資料類型 |
| ------------ | ------------ | ------------ |
| 數位資料類型 | 數位 (p，0)  | p <的 int64 (= 18)  <br> p > 18) 的雙 ( |
| 浮點數字資料類型 | 數位 (p，s)  <br> 浮動 (p)  | double |
| Date datatype | 日期 <br> 時間 戳 <br> TIMESTAMP (n)  | datetime |
| 字元資料類型 | CHAR (n)  <br> VARCHAR <br> VARCHAR2 <br> 長 <br> CLOB <br> NCLOB | 字串 |
| Unicode 字元資料類型 | NCHAR <br> NVARCHAR | 字串 |
| RowID 資料類型 | ROWID <br> UROWID | 字串 |

對於目前不是直接支援的任何其他資料類型，此資料行必須明確地轉換成支援的資料類型。

### <a name="watermark-required"></a>浮水印 (必要) 

若要防止資料庫超載，連接器會批次並繼續完整編目的查詢。 使用 [浮水印] 資料行的值，每個後續的批次都會取得，而查詢會從最後一個檢查點繼續。 本質上，這是一種機制，用來控制完整編目的資料重新整理。

建立浮水印的查詢程式碼片段，如下列範例所示：

* `WHERE (CreatedDateTime > @watermark)`. 使用保留的關鍵字 `@watermark` 來引用浮水印欄名稱。 您只能以遞增順序排序浮水印欄。
* `ORDER BY CreatedDateTime ASC`. 在 [浮水印] 欄上以遞增順序排序。

在下一個影像所示的設定中， `CreatedDateTime` 是選取的 [浮水印] 欄。 若要取得第一批列，請指定 [浮水印] 資料行的資料類型。 在此情況下，資料類型為 `DateTime` 。

![浮水印欄設定。](media/MSSQL-watermark.png)

第 **一個查詢** 會使用： "CreatedDateTime > 1753 年1月1日，00:00:00" (最小值 DateTime 的資料類型) 。 提取第一個批次之後，如果資料列是以遞增順序排序，則會將批次中傳回的最高值 `CreatedDateTime` 儲存為檢查點。 範例是 03:00:00 2019 年3月1日。 然後，在查詢中使用「CreatedDateTime > 三月份1，2019 03:00:00」提取下一批 **N** 列。

### <a name="skipping-soft-deleted-rows-optional"></a>跳過虛刪除的列 (選用) 

若要排除資料庫中虛刪除的列的索引，請指定虛刪除的列名稱和值，以指出刪除列的資料行。

![虛刪除設定：「Soft delete column」和「虛刪除」欄位的值，表示已刪除的資料列。](media/MSSQL-softdelete.png)

### <a name="full-crawl-manage-search-permissions"></a>完整編目：管理搜尋許可權

選取 [ **管理許可權** ]，以選擇用來指定存取控制機制 (ACL) 欄的各種存取控制。 選取您在 [完整編目 SQL] 查詢中指定的欄名。

每個 ACL 欄都應該是多重值欄。 您可以使用分隔符號（如分號 (; ) 、逗號 (、) 等等）來分隔這些多個 ID 值。 您必須在 [ **值分隔符號** ] 欄位中指定此分隔符號。

下列識別碼類型可供使用 ACLs：

* **使用者主體名稱 (upn)**：使用者主要名稱 (upn) 是以電子郵件地址格式的系統使用者名稱。 UPN (例如： john.doe@domain.com) 會包含 (登入名稱) 、分隔符號 (@ 符號) 和功能變數名稱 (UPN 尾碼) 的使用者名稱。
* **Azure Active Directory (AAD) 識別碼**：在 Azure AD 中，每個使用者或群組都有一個類似 ' e0d3ad3d-0000-1111-2222-3c5f5c52ab9b ' 的物件識別碼。
* **Active Directory (AD) 安全性** 識別碼：在內部部署 AD 安裝程式中，每個使用者和群組都有一個無法變化的唯一安全性識別碼，看起來像是-1-5-21-3878594291-2115959936-132693609-65242。 '

![搜尋許可權設定，以設定存取控制清單。](media/MSSQL-ACL2.png)

## <a name="step-3b-incremental-crawl-optional"></a>步驟3b：增量編目 (選用) 

在此選用的步驟中，提供 SQL 查詢，以執行資料庫的累加編目。 在此查詢中，SQL 連接器會決定自上次累加編目以來對資料所做的任何變更。 在完整編目中，選取 [選項] [ **查詢**]、[ **搜尋**] 或 [ **取得**]。 指定您在完整編目查詢中指定的相同 ACL 欄集。

下列映射中的元件類似于完整編目元件，但有一個例外。 在此情況下，"ModifiedDateTime" 是選取的浮水印欄。 查看 [完整編目步驟](#step-3a-full-crawl-required) ，以瞭解如何撰寫累加編目查詢，並以範例顯示下列影像。

![新增編目腳本，顯示可使用的 OrderTable、AclTable 和範例屬性。](media/MSSQL-incrcrawl.png)

## <a name="step-4-assign-property-labels"></a>步驟4：指派屬性標籤

遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## <a name="step-5-manage-schema"></a>步驟5：管理架構

遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## <a name="step-6-manage-search-permissions"></a>步驟6：管理搜尋許可權

您可以選擇使用完整編目 [畫面中所指定的 ACLs](#full-crawl-manage-search-permissions) ，也可以覆寫它們，讓每個人都能看到您的內容。

## <a name="step-7-choose-refresh-settings"></a>步驟7：選擇重新整理設定

Oracle SQL 連接器支援完整和累加編目的更新排程。 我們建議您同時設定兩者。

完整編目排程會找到先前同步處理至 Microsoft 搜尋索引的已刪除資料列，以及移出同步篩選的任何列。 當您第一次連線至資料庫時，會執行完整編目，以同步處理所有從完整編目查詢檢索到的資料列。 若要同步處理新的資料列並進行更新，您必須排程累加編目。

## <a name="step-8-review-connection"></a>步驟8：檢查連線

遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

<!--- ## Next steps: Customize the search results page

Create your own verticals and result types, so end users can view search results from new connections. Without this step, data from your connection won't show up on the search results page.

To learn more about how to create your verticals and MRTs, see [Search results page customization](customize-search-page.md). -->

## <a name="troubleshooting"></a>正在疑難排解

下表是設定連接器時所觀察到的常見錯誤，以及可能的原因。

| 設定步驟 | 錯誤訊息 | 可能的原因 (s)  |
| ------------ | ------------ | ------------ |
| 資料庫設定 | 來自資料庫伺服器的錯誤：連接要求超時 | 不正確主機名稱 <br> 無法到達主機 |
| 資料庫設定 | 來自資料庫伺服器的錯誤： ORA-12541： TNS：沒有攔截器 | 不正確埠 |
| 資料庫設定 | 來自資料庫伺服器的錯誤： ORA-12514： TNS：攔截器目前不知道連接器描述項中所要求的服務 | 不正確服務 (資料庫) 名稱 |
| 資料庫設定 | 來自資料庫伺服器的錯誤：使用者 ' `user` ' 的登入失敗。 | 不正確使用者名稱或密碼 |

## <a name="limitations"></a>限制

Oracle SQL 連接器在預覽版本中有這些限制：

* 內部部署資料庫必須執行 Oracle 資料庫11g 或更新版本。
* 只有使用使用者主要名稱 (UPN) 、Azure Active Directory (Azure AD) ，或 Active Directory 安全性才能支援 ACLs。
* 不支援在資料庫欄中編制豐富內容的索引。 這類內容的範例為 HTML、JSON、XML、blob 及檔 parsings，以資料庫資料欄中的連結形式存在。
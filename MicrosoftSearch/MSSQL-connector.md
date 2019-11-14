---
title: Microsoft Search 的 Microsoft SQL 連接器
ms.author: v-pamcn
author: monaray
manager: mnirkhe
ms.date: 11/04/2019
ms.audience: Admin
ms.topic: article
ms.service: mssearch
localization_priority: Normal
search.appverid:
- BFB160
- MET150
- MOE150
description: 為 Microsoft Search 設定 Microsoft SQL 連接器。
ms.openlocfilehash: a5e0b26277345814ed095b54583ea635341295ad
ms.sourcegitcommit: bfcab9d42e93addccd1e3875b41bc9cc1b6986cc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/04/2019
ms.locfileid: "37949653"
---
# <a name="microsoft-sql-server-connector"></a>Microsoft SQL server 連接器

Microsoft SQL server 連接器，您的組織可以探索和索引資料從內部部署 SQL Server 資料庫。 連接器索引指定成 Microsoft 搜尋的內容。 若要保留最新的來源資料的索引，它所支援定期完整和累加編目。 使用 SQL Server 連接器，您也可以限制存取搜尋結果提供給特定使用者。

本文適用於 Microsoft 365 系統管理員或人設定、 執行，並監視的 Microsoft SQL server 連接器。 本文說明如何設定連接器，連接器功能、 限制和疑難排解技巧。

## <a name="install-a-data-gateway"></a>安裝資料閘道
若要存取您的協力廠商資料，您必須安裝及設定 Microsoft Power BI 閘道。 請參閱[安裝與內部部署閘道](https://docs.microsoft.com/data-integration/gateway/service-gateway-install)若要了解更多。  

## <a name="connect-to-a-data-source"></a>連線至資料來源
若要連接您的 Microsoft SQL server 連接器至資料來源，您必須設定您要編目的資料庫伺服器和內部部署閘道。 您可以再連線到資料庫所需的驗證方法。

> [!NOTE]
> 2008 或更新版本，您的資料庫必須執行 SQL server 版本。

若要搜尋您資料庫的內容，您必須指定 SQL 查詢，當您設定連接器。 下列 SQL 查詢必須命名為所有要索引 （亦即來源的屬性），包括任何不需要執行若要取得所有的資料行的 SQL 聯結的資料庫資料行。 若要限制存取權的搜尋結果，您必須指定存取控制清單 (Acl) 與 SQL 查詢時您設定 Microsoft SQL server 連接器。

## <a name="full-crawl-required"></a>（必要） 的完整編目
在此步驟中，您可以設定執行完整編目資料庫的 SQL 查詢。 完整編目會選取所有的資料行或您想要進行的屬性**設為可查詢**、**可搜尋**，或**可擷取**。 您也可以指定限制對特定使用者或群組存取搜尋結果的 ACL 欄。

> [!Tip]
> 若要取得您需要的所有資料行，您可以加入多個資料表。

![指令碼顯示 OrderTable 和 AclTable 與範例屬性](media/MSSQL-fullcrawl.png)

### <a name="select-data-columns-required-and-acl-columns-optional"></a>選取的資料行 （必要） 和 ACL 資料行 （選用）
此範例將示範如何選取項目保留搜尋的資料的五個資料欄的： OrderId、 OrderTitle、 OrderDesc、 CreatedDateTime 及 IsDeleted。 若要設定檢視權限的每一列資料，您可以選擇性地選取這些 ACL 欄： AllowedUsers、 AllowedGroups、 DeniedUsers 及 DeniedGroups。 您可以進行所有這些資料行**設為可查詢**、**可搜尋**，或**可擷取**。

此範例會查詢中所示，請選取的資料行：`SELECT OrderId, OrderTitle, OrderDesc, AllowedUsers, AllowedGroups, DeniedUsers, DeniedGroups, CreatedDateTime, IsDeleted`

### <a name="watermark-required"></a>浮水印 （必要）
若要防止多載資料庫，連接器批次，而且會繼續具有完整編目浮水印資料行的完整編目查詢。 藉由使用浮水印資料行的值，會擷取每一個後續的批次，並查詢從最後一個的檢查點繼續執行。 基本上，這是一種機制可控制的完整編目的資料重新整理。

建立查詢程式碼片段的浮水印，如以下範例所示：
* `WHERE (CreatedDateTime > @watermark)`. 引用浮水印資料行名稱與保留的關鍵字`@watermark`。 如果浮水印資料行的排序順序遞增，使用`>`;否則，請使用`<`。
* `ORDER BY CreatedDateTime ASC`. 浮水印欄，以遞增或遞減順序排序。

在下列影像所示設定`CreatedDateTime`是所選取的浮水印資料行。 若要擷取的資料列的第一個批次，指定浮水印欄的資料類型。 在此例中的資料類型是`DateTime`。

![](media/MSSQL-watermark.png)

第一個查詢擷取資料列的第一個**N**量使用: 「 CreatedDateTime > 1753 年 1 月 1 日 00:00:00 」 （最小值的日期時間資料類型）。 第一個批次會擷取的最高值之後`CreatedDateTime`中傳回批次會儲存為檢查點，如果資料列會以遞增順序排序。 例如，2019 年 3 月 1 日 03:00:00。 然後**N**個資料列的下一個批次會擷取使用 「 CreatedDateTime > 2019 年 3 月 1 日 03:00:00 」 在查詢中。

### <a name="skipping-soft-deleted-rows-optional"></a>略過虛刪除的資料列 （選用）
若要排除在編製索引的虛刪除資料庫中的資料列，請指定虛刪除資料行名稱和值，指出刪除資料列。

![虛刪除的設定: 「 虛刪除資料行 」 和 「 值的虛刪除會指出刪除的資料列資料行 」](media/MSSQL-softdelete.png)

## <a name="incremental-crawl-optional"></a>累加編目 （選用）
在此選用的步驟中，提供執行累加編目資料庫的 SQL 查詢。 此查詢中，與 Microsoft SQL server 連接器任何對資料進行變更自上次的累加編目。 如同完整編目]，選取您想要進行的所有欄**設為可查詢**、**可搜尋**，或**可擷取**。 指定相同的完整編目查詢中指定的 ACL 欄集合。

下圖中的元件與類似有一個例外狀況的完整編目元件。 在此情況下，「 ModifiedDateTime 」 是所選取的浮水印資料行。 檢閱[完整編目的步驟](#full-crawl-required)，以了解如何撰寫累加編目查詢，並查看下圖為例。

![顯示可用的 OrderTable、 AclTable 及範例內容的累加編目指令碼。](media/MSSQL-incrcrawl.png)

## <a name="limitations"></a>限制
Microsoft SQL server 連接器已在預覽中的釋放這些限制：
* 內部部署資料庫必須執行 SQL server 版本，2008年或更新版本。
* 使用使用者主要名稱 (UPN)、 Azure Active Directory (Azure AD) 或 Active Directory 安全性只支援 Acl。
* 不支援資料庫資料行內的豐富內容編製索引。 這類內容的範例為 HTML、 JSON、 XML、 blob，與文件 parsings 在於做為內的資料庫資料行的連結。
